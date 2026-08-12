---
layout: post
title:  "Solving Hack The Box Challenges with DeepSeek V4 Pro"
date:   2026-08-12 09:11:15 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

DeepSeek V4 Pro was the best (and most expensive) LLM I tested with [Strix a few months ago]({% post_url 2026-04-25-deepseek-v4-with-strix-a-quick-test %}). After the heartbreaking results of its smaller sibling, [DeepSeek V4 Flash 0731]({% post_url 2026-08-11-solving-htb-challenges-with-deepseek-deepseek-v4-flash-0731 %}), in my HTB-Challenger tests, I was curious to see how the Pro version would handle the new challenges.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

The results of **DeepSeek V4 Pro** in my testing were, well, not great and not terrible. On the one hand, it didn't have the basic flaws I observed when testing **DeepSeek V4 Flash 0731**: it didn't submit any incorrect flags, and it used the available tools without any issues. On the other hand, its final score was comparable to that of [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}), whose median cost per test was 17 times lower.

The performance gap between **DeepSeek V4 Pro** and the leaders of my benchmark was also quite large. I'm afraid that's a sign of just how quickly things have progressed over the last few months. DeepSeek V4 Pro was released four months ago, which feels like an eternity now that we're getting better and better models almost every month.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/deepseek-deepseek-v4-pro-20260423-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 8
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 8
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 37.5%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 62.5 | 938 |
| Model cost | $0.35 | $11.84 |
| Duration | 00:06:19 | 03:34:35 |
| Number of input tokens | 1.93M | 39.64M |
| Number of output tokens | 0.01M | 0.35M |
| Number of `read_file` tool calls | 1.5 | 55 |
| Number of `write_file` tool calls | 1.0 | 92 |
| Number of `execute_command` tool calls | 26.5 | 821 |
| Number of `web_search` tool calls | 0.0 | 102 |

## Results by challenge difficulty

### Very Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 3
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 24.5 | 158 |
| Model cost | $0.11 | $1.19 |
| Duration | 00:03:51 | 00:27:35 |
| Number of input tokens | 0.28M | 4.28M |
| Number of output tokens | 0.01M | 0.05M |
| Number of `read_file` tool calls | 1.5 | 8 |
| Number of `write_file` tool calls | 0.0 | 7 |
| Number of `execute_command` tool calls | 15.5 | 149 |
| Number of `web_search` tool calls | 2.0 | 10 |

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
| Model steps | 21.5 | 155 |
| Model cost | $0.09 | $2.09 |
| Duration | 00:04:05 | 00:49:04 |
| Number of input tokens | 0.22M | 5.02M |
| Number of output tokens | 0.01M | 0.07M |
| Number of `read_file` tool calls | 2.0 | 10 |
| Number of `write_file` tool calls | 2.0 | 41 |
| Number of `execute_command` tool calls | 15.5 | 79 |
| Number of `web_search` tool calls | 4.5 | 32 |

### Medium challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 2
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 50.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 56.5 | 225 |
| Model cost | $0.61 | $3.78 |
| Duration | 00:09:55 | 01:11:26 |
| Number of input tokens | 2.44M | 10.07M |
| Number of output tokens | 0.02M | 0.11M |
| Number of `read_file` tool calls | 0.5 | 17 |
| Number of `write_file` tool calls | 0.5 | 5 |
| Number of `execute_command` tool calls | 52.5 | 231 |
| Number of `web_search` tool calls | 0.0 | 8 |

### Hard challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 0
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 4
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 0.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 100 | 400 |
| Model cost | $1.27 | $4.78 |
| Duration | 00:16:12 | 01:06:30 |
| Number of input tokens | 5.25M | 20.27M |
| Number of output tokens | 0.02M | 0.10M |
| Number of `read_file` tool calls | 1.0 | 20 |
| Number of `write_file` tool calls | 4.0 | 39 |
| Number of `execute_command` tool calls | 93.5 | 362 |
| Number of `web_search` tool calls | 0.0 | 52 |
