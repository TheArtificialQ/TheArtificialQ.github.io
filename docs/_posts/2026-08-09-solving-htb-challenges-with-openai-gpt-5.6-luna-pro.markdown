---
layout: post
title:  "Solving Hack The Box Challenges with GPT-5.6 Luna Pro"
date:   2026-08-10 16:51:46 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

What the heck is **GPT-5.6 Luna Pro**, I hear you asking. That's a very good question! To answer it, let me quote its [description on OpenRouter.ai](https://openrouter.ai/openai/gpt-5.6-luna-pro): "***GPT-5.6 Luna Pro** is the same underlying model as **GPT-5.6 Luna**, served with `reasoning.mode` set to `pro` for higher-quality responses on complex tasks.*"

Okay, so how much better, and how much more expensive, is it compared with **GPT-5.6 Luna**, I hear you asking now. And that's exactly what I can tell you.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

I tested **GPT-5.6 Luna** in my [previous post]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}), so I have the numbers ready. In a nutshell:

- **Luna Pro** is approximately five times more expensive than **Luna**. It may sound dramatic, but **Luna** is such a cheap model that **Luna Pro** is still very cheap.
- In this benchmark run, **Luna Pro** performed much better than **Luna**. If you look below at the results for the more difficult challenges, you can see that **Luna Pro** solved some Medium and Hard challenges, while **Luna** solved only one Medium challenge and no Hard challenges.

I believe the main use case for **Luna Pro** is if you are tied to the OpenAI ecosystem and need a model for offensive-security or CTF-style tasks. In my tests, **GPT-5.6 Terra** and **GPT-5.6 Sol** refused to respond to most offensive-security requests, so **GPT-5.6 Luna Pro** was the most useful OpenAI option for this kind of work.


---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-luna-pro-20260709-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 11
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 4
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 55.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 21.5 | 554 |
| Model cost | $0.10 | $3.05 |
| Duration | 00:08:55 | 03:48:35 |
| Number of input tokens | 1.50M | 42.93M |
| Number of output tokens | 0.07M | 1.63M |
| Number of `read_file` tool calls | 4.0 | 186 |
| Number of `write_file` tool calls | 0.0 | 18 |
| Number of `execute_command` tool calls | 36.5 | 865 |
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
| Model steps | 6 | 38 |
| Model cost | $0.01 | $0.14 |
| Duration | 00:01:43 | 00:12:53 |
| Number of input tokens | 0.16M | 1.89M |
| Number of output tokens | 0.01M | 0.08M |
| Number of `read_file` tool calls | 0.5 | 7 |
| Number of `write_file` tool calls | 0.0 | 1 |
| Number of `execute_command` tool calls | 6.0 | 73 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 21.5 | 80 |
| Model cost | $0.09 | $0.34 |
| Duration | 00:08:46 | 00:37:25 |
| Number of input tokens | 1.38M | 4.94M |
| Number of output tokens | 0.06M | 0.22M |
| Number of `read_file` tool calls | 1.5 | 12 |
| Number of `write_file` tool calls | 0.0 | 0 |
| Number of `execute_command` tool calls | 26.5 | 99 |
| Number of `web_search` tool calls | 0.5 | 3 |

### Medium challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 2
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 2
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 50.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 33 | 175 |
| Model cost | $0.16 | $1.02 |
| Duration | 00:13:37 | 01:10:21 |
| Number of input tokens | 2.30M | 14.23M |
| Number of output tokens | 0.10M | 0.54M |
| Number of `read_file` tool calls | 8.5 | 75 |
| Number of `write_file` tool calls | 0.5 | 3 |
| Number of `execute_command` tool calls | 47.5 | 265 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Hard challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 1
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 2
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 25.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 73.5 | 261 |
| Model cost | $0.45 | $1.55 |
| Duration | 00:28:35 | 01:47:55 |
| Number of input tokens | 6.36M | 21.87M |
| Number of output tokens | 0.22M | 0.79M |
| Number of `read_file` tool calls | 16.5 | 92 |
| Number of `write_file` tool calls | 2.5 | 14 |
| Number of `execute_command` tool calls | 121.0 | 428 |
| Number of `web_search` tool calls | 0.0 | 0 |
