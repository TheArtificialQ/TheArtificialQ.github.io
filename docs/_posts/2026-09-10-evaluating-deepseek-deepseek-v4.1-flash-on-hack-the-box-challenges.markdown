---
layout: post
title:  "Evaluating DeepSeek V4.1 Flash on Hack The Box Challenges"
date:   2026-09-11 11:18:00 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

DeepSeek V4 has been a strange story for me. The original Flash model impressed me in [my Strix tests back in April]({% post_url 2026-04-25-deepseek-v4-with-strix-a-quick-test %}), but [V4 Flash 0731]({% post_url 2026-08-11-solving-htb-challenges-with-deepseek-deepseek-v4-flash-0731 %}) then gave me one of the most disappointing results in this benchmark. The [original V4 Pro]({% post_url 2026-08-12-solving-htb-challenges-with-deepseek-deepseek-v4-pro %}) and [updated Pro 0813]({% post_url 2026-08-18-evaluating-deepseek-deepseek-v4-pro-0813-on-hack-the-box-challenges %}) did better, but neither got close to the leaders. So I was curious whether **DeepSeek V4.1 Flash** would finally change that.

It did. DeepSeek is back.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

V4.1 Flash solved 15 out of 16 challenges, including three of the four Hard ones. Just as importantly, it didn't repeat the previous Flash model's habit of submitting incorrect flags. This is the DeepSeek result I had been waiting for.

Not quite a new champion, though. [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}) still scored higher and needed far fewer steps, although it costs more. [GLM 5.3 Flash]({% post_url 2026-08-27-evaluating-z-ai-glm-5.3-flash-on-hack-the-box-challenges %}) solved exactly the same challenges as V4.1 Flash at a lower median cost. Their scores were practically identical, and I wouldn't read too much into such a small gap.

It is easily the strongest DeepSeek run I've seen on this benchmark. If I want strong autonomous problem-solving without paying Sol prices, V4.1 Flash is finally a DeepSeek model I can seriously consider again.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/deepseek-deepseek-v4.1-flash-20260910-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/deepseek-deepseek-v4.1-flash-20260910-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/deepseek-deepseek-v4.1-flash-20260910-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 15
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 1
- **Benchmark score:** 80.9%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 26 | 537 |
| Model cost | $0.05 | $1.25 |
| Duration | 00:07:50 | 03:08:24 |
| Number of input tokens | 0.90M | 17.98M |
| Number of output tokens | 0.05M | 1.36M |
| Number of `read_file` tool calls | 1.0 | 69 |
| Number of `write_file` tool calls | 2.0 | 59 |
| Number of `execute_command` tool calls | 27.5 | 564 |
| Number of `web_search` tool calls | 0.0 | 10 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 3 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 1 |
| Benchmark score | 95.5% | 90.0% | 88.0% | 67.4% |
| **Median per challenge** | | | | |
| Model steps | 17.5 | 27.5 | 34 | 26 |
| Model cost | $0.01 | $0.03 | $0.05 | $0.10 |
| Duration | 00:01:31 | 00:08:37 | 00:08:50 | 00:12:45 |
| Number of input tokens | 0.41M | 0.70M | 1.31M | 1.03M |
| Number of output tokens | 0.01M | 0.04M | 0.04M | 0.09M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 0.5 | 4.0 |
| Number of `write_file` tool calls | 0.5 | 3.0 | 4.0 | 2.0 |
| Number of `execute_command` tool calls | 18.0 | 17.5 | 33.5 | 30.0 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
