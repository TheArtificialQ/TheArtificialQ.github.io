---
layout: post
title:  "Solving Hack The Box Challenges with GPT-5.6 Luna"
date:   2026-08-10 15:30:47 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

My first thought was: let's kick off the [HTB-Challenger Benchmark]({{ "/htb-challenger-benchmark" | relative_url }}) with some state-of-the-art models. Let's see what these Fables, Opuses, Terras and Sols can do with offensive security challenges. As it turned out, not much - sooner or later, all of them refused to continue with the HTB challenge-solving workflow, with messages like “This content was flagged for possible cybersecurity risk.” So I was left with just GPT-5.6 Luna. And it was not so bad after all.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

The main quality of GPT-5.6 Luna is its price - it's unbelievably cheap! The median model cost per HTB challenge was $0.02, which is virtually free. Its results were not the best: it solved all Very Easy challenges and three out of four Easy ones, but only one Medium challenge and no Hard challenges. It clearly started to lose its breath as the difficulty increased.

Still, for simple, clearly scoped CTF-style tasks, I would always try this model first. If it doesn't produce useful results, I would move to a more capable (and more expensive) model. This should save you a lot of money in the long term.

Also check out the results for [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}). It is slightly more expensive, but it also performed better.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-luna-20260709-model-card.svg" | relative_url }})

## Total metrics

- **Number of challenges:** 16
- **Number of solved challenges:** 8
- **Number of false positives:** 0
- **Runs where the model gave up:** 8
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 32.5%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 17.5 | 431 |
| Model cost | $0.02 | $0.58 |
| Duration | 00:04:38 | 02:03:31 |
| Number of input tokens | 0.34M | 16.84M |
| Number of output tokens | 0.02M | 0.32M |
| Number of `read_file` tool calls | 1.0 | 39 |
| Number of `write_file` tool calls | 0.0 | 12 |
| Number of `execute_command` tool calls | 28.0 | 609 |
| Number of `web_search` tool calls | 0.0 | 3 |

## Results by challenge difficulty

### Very Easy challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 4
- **Number of false positives:** 0
- **Runs where the model gave up:** 0
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 11.5 | 46 |
| Model cost | $0.01 | $0.05 |
| Duration | 00:01:56 | 00:08:54 |
| Number of input tokens | 0.11M | 1.24M |
| Number of output tokens | 0.00M | 0.02M |
| Number of `read_file` tool calls | 0.5 | 6 |
| Number of `write_file` tool calls | 0.0 | 0 |
| Number of `execute_command` tool calls | 11.5 | 77 |
| Number of `web_search` tool calls | 0.0 | 2 |

### Easy challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 3
- **Number of false positives:** 0
- **Runs where the model gave up:** 1
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 15.5 | 75 |
| Model cost | $0.01 | $0.05 |
| Duration | 00:05:04 | 00:21:14 |
| Number of input tokens | 0.27M | 1.26M |
| Number of output tokens | 0.01M | 0.05M |
| Number of `read_file` tool calls | 1.0 | 8 |
| Number of `write_file` tool calls | 0.0 | 2 |
| Number of `execute_command` tool calls | 24.5 | 101 |
| Number of `web_search` tool calls | 0.0 | 1 |

### Medium challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 1
- **Number of false positives:** 0
- **Runs where the model gave up:** 3
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 25.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 25 | 144 |
| Model cost | $0.05 | $0.22 |
| Duration | 00:09:07 | 00:38:38 |
| Number of input tokens | 0.96M | 6.21M |
| Number of output tokens | 0.03M | 0.15M |
| Number of `read_file` tool calls | 0.5 | 11 |
| Number of `write_file` tool calls | 0.0 | 4 |
| Number of `execute_command` tool calls | 33.0 | 170 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Hard challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 0
- **Number of false positives:** 0
- **Runs where the model gave up:** 4
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 0.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 40 | 166 |
| Model cost | $0.06 | $0.25 |
| Duration | 00:13:30 | 00:54:46 |
| Number of input tokens | 1.93M | 8.13M |
| Number of output tokens | 0.03M | 0.11M |
| Number of `read_file` tool calls | 2.0 | 14 |
| Number of `write_file` tool calls | 0.0 | 6 |
| Number of `execute_command` tool calls | 60.0 | 261 |
| Number of `web_search` tool calls | 0.0 | 0 |
