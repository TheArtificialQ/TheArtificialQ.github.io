---
layout: post
title:  "Evaluating GPT-5.6 Terra Pro on Hack The Box Challenges"
date:   2026-08-16 16:10:31 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hidden: true
hn_id:  
---

> For some personal observations about this model, please see the [Solving Hack The Box Challenges with GPT-5.6]({% post_url 2026-08-17-solving-htb-challenges-with-openai-gpt-5.6 %}) post.


<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-terra-pro-20260709-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/openai-gpt-5.6-terra-pro-20260709-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/openai-gpt-5.6-terra-pro-20260709-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 14
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 2
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 75.1%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 11 | 353 |
| Model cost | $0.91 | $29.93 |
| Duration | 00:08:22 | 02:30:03 |
| Number of input tokens | 0.64M | 22.53M |
| Number of output tokens | 0.03M | 0.83M |
| Number of `read_file` tool calls | 0.0 | 20 |
| Number of `write_file` tool calls | 0.0 | 18 |
| Number of `execute_command` tool calls | 13.5 | 351 |
| Number of `web_search` tool calls | 0.0 | 4 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 2 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 2 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 97.3% | 97.1% | 94.0% | 44.4% |
| **Median per challenge** | | | | |
| Model steps | 5 | 9.5 | 20.5 | 29.5 |
| Model cost | $0.16 | $0.53 | $1.95 | $2.46 |
| Duration | 00:01:10 | 00:03:35 | 00:09:53 | 00:18:01 |
| Number of input tokens | 0.08M | 0.39M | 1.39M | 1.98M |
| Number of output tokens | 0.01M | 0.02M | 0.06M | 0.07M |
| Number of `read_file` tool calls | 0.5 | 0.5 | 0.0 | 0.0 |
| Number of `write_file` tool calls | 0.0 | 0.5 | 0.0 | 0.0 |
| Number of `execute_command` tool calls | 4.0 | 9.0 | 19.5 | 31.0 |
| Number of `web_search` tool calls | 0.5 | 0.0 | 0.0 | 0.0 |
