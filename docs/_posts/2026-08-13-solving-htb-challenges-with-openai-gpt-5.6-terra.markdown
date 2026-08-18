---
layout: post
title:  "Evaluating GPT-5.6 Terra on Hack The Box Challenges"
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

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-terra-20260709-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/openai-gpt-5.6-terra-20260709-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/openai-gpt-5.6-terra-20260709-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 12
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 4
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 64.6%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 16.5 | 428 |
| Model cost | $0.24 | $10.38 |
| Duration | 00:03:16 | 02:29:17 |
| Number of input tokens | 0.23M | 16.61M |
| Number of output tokens | 0.01M | 0.26M |
| Number of `read_file` tool calls | 0.0 | 18 |
| Number of `write_file` tool calls | 0.0 | 6 |
| Number of `execute_command` tool calls | 15.5 | 418 |
| Number of `web_search` tool calls | 0.0 | 6 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 3 | 3 | 2 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 1 | 1 | 2 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 98.9% | 73.8% | 72.1% | 45.9% |
| **Median per challenge** | | | | |
| Model steps | 6 | 13 | 23.5 | 32 |
| Model cost | $0.05 | $0.14 | $0.45 | $0.89 |
| Duration | 00:00:39 | 00:02:52 | 00:05:19 | 00:08:06 |
| Number of input tokens | 0.03M | 0.12M | 0.70M | 1.59M |
| Number of output tokens | 0.00M | 0.01M | 0.02M | 0.02M |
| Number of `read_file` tool calls | 0.5 | 0.5 | 0.0 | 0.5 |
| Number of `write_file` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
| Number of `execute_command` tool calls | 4.5 | 11.0 | 22.5 | 35.5 |
| Number of `web_search` tool calls | 0.0 | 0.5 | 0.0 | 0.0 |
