---
layout: post
title:  "Solving Hack The Box Challenges with Kimi K3"
date:   2026-08-10 16:52:46 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

Kimi K3 landed with a big splash just three weeks ago, and the initial reviewers seemed to agree on one thing: it's very good, but it's also quite expensive. So here I am, the late reviewer, with my own numbers. Let's see if they line up with the prevailing opinion.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

In short, my numbers line up pretty well with what you may have already read or heard about **Kimi K3**.

So far, I can compare it only with [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}) and [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}), and the difference is clear. **Kimi K3** achieved an XP-weighted benchmark score of 75%, well ahead of **Luna** at 32.5% and **Luna Pro** at 55%. That was more or less what I expected based on the initial reviews.

The difference also shows up where it matters for harder offensive-security tasks. **Kimi K3** solved all four Medium challenges and two of the four Hard ones. **Luna Pro** solved two Medium challenges and one Hard challenge, while **Luna** solved only one Medium challenge and no Hard challenges.

But that extra capability is costly. Based on the median model cost per challenge, **Kimi K3** was almost five times more expensive than **GPT-5.6 Luna Pro** and about 23 times more expensive than **GPT-5.6 Luna**.

Anyway, if your budget is not tight and you need a high-performance model for offensive-security or CTF-style tasks, **Kimi K3** is the strongest of the three models I have tested so far.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/moonshotai-kimi-k3-20260715-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 13
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 1
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 22 | 489 |
| Model cost | $0.46 | $26.58 |
| Duration | 00:07:34 | 05:54:08 |
| Number of input tokens | 0.33M | 15.40M |
| Number of output tokens | 0.02M | 0.72M |
| Number of `read_file` tool calls | 1.0 | 53 |
| Number of `write_file` tool calls | 3.5 | 59 |
| Number of `execute_command` tool calls | 15.5 | 440 |
| Number of `web_search` tool calls | 0.0 | 3 |

## Results by challenge difficulty

### Very Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 16.5 | 61 |
| Model cost | $0.43 | $1.37 |
| Duration | 00:04:31 | 00:16:59 |
| Number of input tokens | 0.15M | 0.64M |
| Number of output tokens | 0.01M | 0.04M |
| Number of `read_file` tool calls | 0.5 | 3 |
| Number of `write_file` tool calls | 2.5 | 13 |
| Number of `execute_command` tool calls | 9.5 | 51 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 3
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 18.5 | 102 |
| Model cost | $0.44 | $6.11 |
| Duration | 00:06:11 | 01:08:46 |
| Number of input tokens | 0.28M | 2.29M |
| Number of output tokens | 0.02M | 0.22M |
| Number of `read_file` tool calls | 1.0 | 11 |
| Number of `write_file` tool calls | 1.5 | 10 |
| Number of `execute_command` tool calls | 13.0 | 88 |
| Number of `web_search` tool calls | 0.0 | 3 |

### Medium challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 16.5 | 101 |
| Model cost | $1.42 | $5.76 |
| Duration | 00:22:12 | 01:45:50 |
| Number of input tokens | 0.39M | 3.59M |
| Number of output tokens | 0.03M | 0.18M |
| Number of `read_file` tool calls | 1.5 | 13 |
| Number of `write_file` tool calls | 2.0 | 10 |
| Number of `execute_command` tool calls | 15.0 | 92 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Hard challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 2
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 1
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 50.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 49.5 | 225 |
| Model cost | $3.51 | $13.33 |
| Duration | 00:30:14 | 02:42:32 |
| Number of input tokens | 1.93M | 8.88M |
| Number of output tokens | 0.06M | 0.29M |
| Number of `read_file` tool calls | 7.5 | 26 |
| Number of `write_file` tool calls | 6.5 | 26 |
| Number of `execute_command` tool calls | 46.0 | 209 |
| Number of `web_search` tool calls | 0.0 | 0 |
