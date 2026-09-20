---
layout: post
title:  "Evaluating Pareto on Hack The Box Challenges"
date:   2026-09-20 11:02:41 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

Have you ever heard of [Unbiased AI](https://unbiased.ai/) or the **Pareto** model that they are working on? Me neither. That's why I was quite surprised when this model performed very well in my testing. And I was even more surprised when I found out that Unbiased AI is not an LLM-making company and that **Pareto** is not actually an LLM.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---


Let's clear things up a bit: **Pareto** is a "blended AI model". You can read about how it works in [this article](https://unbiased.ai/how/), but basically **Pareto** is just a facade for a platform consisting of multiple (undisclosed) LLMs. You send it a message, it is processed by a few LLMs, their answers are aggregated, and the result is sent back to you. This is not a new concept; for example, OpenRouter introduced a similar [Fusion](https://openrouter.ai/openrouter/fusion) "model" some time ago, but I haven't tested it yet.

My verdict based on this testing is this: in terms of performance, **Pareto** is excellent at cracking Hack The Box challenges and achieved a score of 80.8% in my benchmark. It's not as good as [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}), which scored 87.2%, but it's on the same level as [GLM 5.3 Flash]({% post_url 2026-08-27-evaluating-z-ai-glm-5.3-flash-on-hack-the-box-challenges %}) (81.0%) and [DeepSeek V4.1 Flash]({% post_url 2026-09-10-evaluating-deepseek-deepseek-v4.1-flash-on-hack-the-box-challenges %}) (80.9%).

Its only issue is that it's relatively expensive. Its median cost per challenge was $0.37, which is not only MUCH higher than **GLM 5.3 Flash** ($0.01) and **DeepSeek V4.1 Flash** ($0.05), but also higher than **GPT-5.6 Sol** ($0.29).

So, good job on the performance, Unbiased AI, but now you need to fire a few managers and janitors to make your company more cost-effective.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/unbiased-pareto-20260917-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/unbiased-pareto-20260917-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/unbiased-pareto-20260917-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 15
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 1
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 80.8%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 25.5 | 555 |
| Model cost | $0.37 | $21.43 |
| Duration | 00:08:22 | 03:32:18 |
| Number of input tokens | 0.34M | 17.50M |
| Number of output tokens | 0.02M | 1.70M |
| Number of `read_file` tool calls | 1.0 | 31 |
| Number of `write_file` tool calls | 4.0 | 90 |
| Number of `execute_command` tool calls | 23.5 | 592 |
| Number of `web_search` tool calls | 0.0 | 1 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 3 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 1 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 95.9% | 92.0% | 91.2% | 63.6% |
| **Median per challenge** | | | | |
| Model steps | 14.5 | 23 | 29 | 52 |
| Model cost | $0.20 | $0.26 | $1.04 | $2.52 |
| Duration | 00:01:57 | 00:06:18 | 00:11:29 | 00:22:28 |
| Number of input tokens | 0.14M | 0.19M | 1.12M | 1.79M |
| Number of output tokens | 0.01M | 0.02M | 0.07M | 0.19M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 0.5 | 1.5 |
| Number of `write_file` tool calls | 1.0 | 6.0 | 4.0 | 7.5 |
| Number of `execute_command` tool calls | 12.5 | 17.0 | 28.0 | 51.0 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
