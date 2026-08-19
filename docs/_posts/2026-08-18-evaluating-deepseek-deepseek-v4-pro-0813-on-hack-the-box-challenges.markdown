---
layout: post
title:  "Evaluating DeepSeek V4 Pro 0813 on Hack The Box Challenges"
date:   2026-08-18 17:15:50 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

The release of **DeepSeek V4 Pro** back in April got a lot of attention - so DeepSeek decided to release it again! The new version is called **DeepSeek V4 Pro 0813**, and it is not exactly clear what changed. Reading its [release page](https://api-docs.deepseek.com/news/news260813/), you can almost feel the marketing team's desperation to put at least something there. The few concrete details are that it uses the same core V4 Pro architecture with approximately 1.6T total and 49B active parameters, adds a DSpark speculative-decoding module (whatever that is), and supports a 1M-token context.

DeepSeek reports large improvements across several agent benchmarks, although those are the developer's own results. I had finished testing the previous Pro version, now called [DeepSeek V4 Pro 0423]({% post_url 2026-08-12-solving-htb-challenges-with-deepseek-deepseek-v4-pro %}), shortly before the new version appeared (sic!). I therefore ran 0813 through my {% include htb-challenger-benchmark-term.html %} to see whether it performed better on cybersecurity tasks.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

The new model achieved a slightly higher benchmark score than the old one, 38.8% versus 36.2%, and solved nine challenges instead of eight. Given the small test set and normal run-to-run variability, I would still call the performance result a draw.

The clearest improvement was efficiency. The median run used far fewer steps (12.5 versus 62.5), tokens (0.25M versus 1.94M), and money ($0.20 versus $0.35) than the older model. That is a good reason to upgrade if you still use the older version.

If you are not specifically committed to DeepSeek, however, there are better choices for this kind of cybersecurity work. [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}) scored 51.3% at a lower median cost of $0.10, while [Grok 4.6]({% post_url 2026-08-12-solving-htb-challenges-with-x-ai-grok-4.6 %}) and [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}) achieved much higher scores at broadly similar median costs.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/deepseek-deepseek-v4-pro-20260813-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/deepseek-deepseek-v4-pro-20260813-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/deepseek-deepseek-v4-pro-20260813-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 9
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 5
- **Benchmark score:** 38.8%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 12.5 | 456 |
| Model cost | $0.20 | $7.97 |
| Duration | 00:07:17 | 06:46:42 |
| Number of input tokens | 0.24M | 16.32M |
| Number of output tokens | 0.01M | 0.98M |
| Number of `read_file` tool calls | 1.0 | 121 |
| Number of `write_file` tool calls | 0.5 | 43 |
| Number of `execute_command` tool calls | 13.0 | 434 |
| Number of `web_search` tool calls | 0.0 | 12 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 3 | 2 | 0 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 1 | 1 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 1 | 1 | 3 |
| Benchmark score | 94.4% | 73.1% | 49.2% | 0.0% |
| **Median per challenge** | | | | |
| Model steps | 10.5 | 12.5 | 27 | 19 |
| Model cost | $0.05 | $0.22 | $1.08 | $0.40 |
| Duration | 00:03:09 | 00:09:19 | 00:34:12 | 00:10:44 |
| Number of input tokens | 0.07M | 0.18M | 0.47M | 0.75M |
| Number of output tokens | 0.00M | 0.02M | 0.11M | 0.02M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 1.5 | 0.0 |
| Number of `write_file` tool calls | 0.0 | 4.0 | 1.0 | 0.0 |
| Number of `execute_command` tool calls | 10.0 | 8.5 | 22.5 | 13.0 |
| Number of `web_search` tool calls | 0.0 | 1.0 | 0.0 | 0.0 |
