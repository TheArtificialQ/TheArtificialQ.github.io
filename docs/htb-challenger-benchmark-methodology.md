---
layout: page
title: HTB-Challenger Benchmark Methodology
permalink: /htb-challenger-benchmark-methodology/
header_image: /assets/images/htb-challenger-benchmark-bg.png
header_alt: HTB-Challenger Benchmark
---

## Purpose of the benchmark

HTB-Challenger Benchmark measures how well large language models can solve [Hack The Box Challenges](https://help.hackthebox.com/en/articles/5185436-how-to-play-challenges): isolated, security-related tasks with a defined objective. It is intended to provide a practical view of the models' cybersecurity problem-solving capabilities in a controlled challenge environment.

The results should be interpreted with caution. The benchmark uses a relatively small challenge set, and model behavior can vary between runs. The statistical error in these measurements may therefore be substantial. Small differences between models should not be treated as conclusive evidence that one model is better than another.

## Test set

Every tested model is evaluated against the same set of 16 selected Hack The Box challenges. The set contains four challenges from each difficulty level:

- 4 Very Easy challenges
- 4 Easy challenges
- 4 Medium challenges
- 4 Hard challenges

Each model gets one run per challenge, producing 16 runs in total. The final numbers reported for a model are evaluated from all 16 runs rather than from a single challenge or difficulty level.

The selected challenges are all recent, reducing the risk that their solutions were included in the models' training data. They are also still Active on Hack The Box, so no official write-ups have been published for them.

> **Note:** The challenge set and per-run limits may change in future versions of the benchmark. Previously published and future measurements may therefore use slightly different test conditions, and the resulting numbers may change. Comparisons should take the documented benchmark version, challenge set, and limits into account.

## Run limits

Every individual challenge run is bounded by two resource limits and two safeguards against models getting stuck:

- A run may use at most 100 model steps.
- A run stops once the cumulative LLM cost reported by OpenRouter reaches or exceeds $15.
- Each LLM response is requested with a maximum output length of 32,768 tokens. If OpenRouter reports that a response ended because it reached this limit, the harness does not execute any potentially truncated tool calls and asks the model to respond more concisely. If the next response also reaches the limit, the run stops.
- If a model makes the exact same tool call - using the same tool and arguments - three times in a row, the harness warns it to change its approach. If the model repeats the call a fourth consecutive time, the run stops before that fourth call is executed.

These conditions keep tests bounded and give every model the same maximum opportunity and budget for solving a challenge. The latter two conditions prevent a stuck model from spending the rest of its budget on repetitive behavior. They apply only to consecutive responses or tool calls; a response that stays within the output limit or a different tool call resets the corresponding count.

A run also ends when the model submits a syntactically valid result or decides to give up. There is no separate overall wall-clock limit. Individual LLM requests and shell commands have timeouts, but these do not impose a fixed maximum duration on the complete run.

## Metrics

The main benchmark metric is an XP-weighted benchmark score. Unsolved challenges contribute no XP. For solved challenges, the XP earned also depends on how efficiently the model solved the challenge in terms of model steps. A solution completed in the challenge's reference (Par) number of steps earns the full XP reward, while solutions that require more steps earn progressively less, down to 70% of the XP at the 100-step limit. Solutions completed in fewer than Par steps are capped at the full XP reward.

The final benchmark score is the effective XP earned across all challenges divided by the total XP available, expressed as a percentage. The XP reward reflects challenge difficulty and ranges from 130 to 520 XP, so solving more difficult challenges still contributes more to the score than solving easier ones.

The benchmark also reports two per-task efficiency metrics:

- the number of model steps per task;
- the LLM model cost per task.

Both values are reported as the median across all 16 runs, not the arithmetic average. This reduces the effect of individual runs with unusually high or low step counts or costs.

## Models and hosting

All evaluated LLMs are accessed through OpenRouter. OpenRouter provides a common API for the tested models, while the underlying model providers, versions, and serving infrastructure may differ.

## Test harness

The benchmark uses the custom `htb-challenger` tool as its test harness. For each run, the harness supplies the challenge description, any included files, and the address of a live challenge instance when applicable.

The harness does not give the model agent skills, security playbooks, supplementary reference documents, worked examples, or challenge-specific guidance. Apart from the general-purpose web search tool, the model must rely on its built-in cybersecurity knowledge and reasoning capabilities.

### How a run works

Each test follows the same basic process:

1. The harness loads the challenge details and safely extracts any supplied archive.
2. It creates a fresh Kali Linux Docker container for the model.
3. The model inspects the inputs, probes the live instance when one is available, develops a solution, and validates a possible flag.
4. The model either submits a flag or gives up.
5. The harness checks the submitted value against the expected flag and saves the run results.

Challenge inputs are mounted read-only. The model receives a separate writable workspace, and its commands run inside the container rather than directly on the host. The container and anything installed in it are discarded after the run.

### Tools available to the model

The model receives six basic tools:

- `read_file` reads challenge inputs and files created during the run.
- `write_file` writes text files to the model's workspace.
- `execute_command` runs shell commands inside the Kali Linux container.
- `web_search` finds general technical information on the web.
- `submit_result` submits a flag and finishes the attempt.
- `give_up` finishes the attempt without a flag.

The model is prohibited from using web search to look for challenge-specific walkthroughs, write-ups, repositories, hints, or flags. It may search only for general resources such as technical documentation, standards, and vulnerability references.
