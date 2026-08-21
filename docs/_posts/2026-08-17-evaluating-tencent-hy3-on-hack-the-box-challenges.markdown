---
layout: post
title:  "Evaluating Hy3 on Hack The Box Challenges"
date:   2026-08-18 05:00:18 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

**Tencent's Hy3** belongs to the category of "interesting LLM models you may never have heard of." It appeared to be quite popular on [OpenRouter.ai](https://openrouter.ai/tencent/hy3) at the start of the summer, when a free version was available, and it seemed to have earned a good reputation. So I thought it might be worth including in the {% include htb-challenger-benchmark-term.html %}.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

In the end, I was a bit disappointed. In terms of performance, **Hy3** sits near the bottom of my benchmark score ladder: its 34.8% score was the third-lowest among the all tested models. In terms of cost, it's cheap, but not exceptionally so: its median cost per challenge was more than four times that of [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}), which achieved a similar benchmark score.

The biggest issue with this model was that it got stuck on more than half of the tested challenges. In these runs, it started producing long, repetitive reasoning outputs in which it argued with itself about potential solutions, and it did not recover after the test harness asked it to shorten its response. Nine of its 16 runs ended this way.

The same behavior is visible in the output-token statistics. Hy3 generated more output than any other model. Its median was 101,509 output tokens per challenge, about 51% above the next-highest model, [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}), at 67,298. Its total of 1.79 million output tokens was also the highest overall. Its output-to-input ratio was an extreme outlier: output tokens equaled 11.72% of input tokens across the run, while the next-highest model, [Qwen3.8 Max]({% post_url 2026-08-11-solving-htb-challenges-with-qwen-qwen3.8-max %}), reached only 4.56%. These figures are consistent with the repetitive responses visible in the run logs.

In summary, this model may have valid use cases, but cybersecurity is not one of them.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/tencent-hy3-20260706-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/tencent-hy3-20260706-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/tencent-hy3-20260706-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 6
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 9
- **Benchmark score:** 34.8%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 18.5 | 471 |
| Model cost | $0.08 | $1.92 |
| Duration | 00:15:21 | 04:41:55 |
| Number of input tokens | 0.32M | 15.25M |
| Number of output tokens | 0.10M | 1.79M |
| Number of `read_file` tool calls | 1.5 | 73 |
| Number of `write_file` tool calls | 0.5 | 44 |
| Number of `execute_command` tool calls | 10.5 | 400 |
| Number of `web_search` tool calls | 0.0 | 5 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 1 | 2 | 2 | 1 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 1 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 2 | 2 | 2 | 3 |
| Benchmark score | 24.9% | 49.4% | 48.1% | 20.0% |
| **Median per challenge** | | | | |
| Model steps | 10.5 | 10.5 | 38 | 42 |
| Model cost | $0.06 | $0.06 | $0.18 | $0.18 |
| Duration | 00:12:16 | 00:17:03 | 00:15:24 | 00:18:06 |
| Number of input tokens | 0.15M | 0.14M | 1.22M | 1.37M |
| Number of output tokens | 0.08M | 0.08M | 0.14M | 0.12M |
| Number of `read_file` tool calls | 1.0 | 3.0 | 1.0 | 4.0 |
| Number of `write_file` tool calls | 3.0 | 0.0 | 3.5 | 0.5 |
| Number of `execute_command` tool calls | 7.5 | 7.0 | 23.5 | 48.0 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
