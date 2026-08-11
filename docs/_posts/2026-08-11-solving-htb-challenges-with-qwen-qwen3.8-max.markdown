---
layout: post
title:  "Solving Hack The Box Challenges with Qwen3.8 Max"
date:   2026-08-11 12:46:34 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

Qwen3.8 Max was released recently, but it didn't create much buzz. I was wondering if it was simply overshadowed by [Kimi K3]({% post_url 2026-08-09-solving-htb-challenges-with-moonshotai-kimi-k3 %}), which was released just a few days earlier, or if its performance wasn't strong enough to raise any eyebrows.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

I know this model has a relatively big fan base among software developers, but based on my results, I bet it won't win many fans among pentesters and red teamers.

Put simply, it's by far the most expensive model I've tested so far, while its results are only mediocre. It solved 9 of 16 challenges and scored 47.5%. For comparison, [GPT 5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}) scored a similar 55.0%, but its median cost per challenge was only $0.10 - one-twentieth of Qwen3.8 Max's $2.00.

Of course, this benchmark covers self-contained HTB challenges, not full pentests or red-team engagements. Still, the price-to-performance ratio for this kind of offensive security task is hard to justify.

I'm really not sure what the use case for this model is. If you already use it for coding and are happy with it, you can also try it on CTF-style offensive security tasks. It solved six of the eight Very Easy and Easy challenges, so the results there were pretty good. But if cost matters or you need better performance on harder challenges, there are better options available.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/qwen-qwen3.8-max-20260803-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **Number of solved challenges:** 9
- **Number of false positives:** 0
- **Runs where the model gave up:** 3
- **Runs that reached the step or cost limit:** 3
- **Benchmark score:** 47.5%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 29 | 547 |
| Model cost | $2.00 | $38.65 |
| Duration | 00:15:32 | 06:28:29 |
| Number of input tokens | 0.93M | 17.85M |
| Number of output tokens | 0.03M | 0.94M |
| Number of `read_file` tool calls | 1.0 | 36 |
| Number of `write_file` tool calls | 1.5 | 50 |
| Number of `execute_command` tool calls | 25.5 | 507 |
| Number of `web_search` tool calls | 0.0 | 7 |

## Results by challenge difficulty

### Very Easy challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 3
- **Number of false positives:** 0
- **Runs where the model gave up:** 0
- **Runs that reached the step or cost limit:** 1
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 16 | 96 |
| Model cost | $0.34 | $5.79 |
| Duration | 00:04:16 | 00:23:59 |
| Number of input tokens | 0.18M | 2.97M |
| Number of output tokens | 0.01M | 0.05M |
| Number of `read_file` tool calls | 1.0 | 4 |
| Number of `write_file` tool calls | 1.5 | 10 |
| Number of `execute_command` tool calls | 12.5 | 90 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Easy challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 3
- **Number of false positives:** 0
- **Runs where the model gave up:** 1
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 27.5 | 143 |
| Model cost | $1.50 | $8.10 |
| Duration | 00:13:24 | 01:34:22 |
| Number of input tokens | 0.74M | 3.73M |
| Number of output tokens | 0.03M | 0.23M |
| Number of `read_file` tool calls | 1.0 | 16 |
| Number of `write_file` tool calls | 5.5 | 20 |
| Number of `execute_command` tool calls | 21.5 | 112 |
| Number of `web_search` tool calls | 1.0 | 4 |

### Medium challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 2
- **Number of false positives:** 0
- **Runs where the model gave up:** 2
- **Runs that reached the step or cost limit:** 0
- **Benchmark score:** 50.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 35 | 140 |
| Model cost | $2.71 | $10.72 |
| Duration | 00:22:41 | 02:33:35 |
| Number of input tokens | 0.99M | 4.46M |
| Number of output tokens | 0.06M | 0.42M |
| Number of `read_file` tool calls | 0.5 | 4 |
| Number of `write_file` tool calls | 1.0 | 7 |
| Number of `execute_command` tool calls | 33.5 | 140 |
| Number of `web_search` tool calls | 0.0 | 2 |

### Hard challenges

- **Number of challenges:** 4
- **Number of solved challenges:** 1
- **Number of false positives:** 0
- **Runs where the model gave up:** 0
- **Runs that reached the step or cost limit:** 2
- **Benchmark score:** 25.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 39 | 168 |
| Model cost | $3.58 | $14.04 |
| Duration | 00:23:36 | 01:56:33 |
| Number of input tokens | 1.67M | 6.70M |
| Number of output tokens | 0.05M | 0.25M |
| Number of `read_file` tool calls | 2.5 | 12 |
| Number of `write_file` tool calls | 2.0 | 13 |
| Number of `execute_command` tool calls | 37.0 | 165 |
| Number of `web_search` tool calls | 0.0 | 1 |
