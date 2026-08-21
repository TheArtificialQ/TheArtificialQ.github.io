---
layout: post
title:  "Evaluating Ox Alpha on Hack The Box Challenges"
date:   2026-08-21 14:16:04 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

A new model called **Ox Alpha** landed on OpenRouter last night, and you can use it for free through Monday, August 24. Today, I tested it on my {% include htb-challenger-benchmark-term.html %}, and hear me out: **stop what you're doing, cancel your weekend plans, and test it!** If you need to cancel all your meetings, your child's birthday party, or your romantic weekend for two, do it. It's worth it! Just don't tell my wife I said that 😉

But really, do it.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

The model was released as a "stealth model," i.e., we don't know what model it actually is or who created it. If you're interested in speculation, quickly search Reddit, but you probably won't be much wiser afterward.

As I already wrote above, it's free for a limited time. This typically means the model provider is collecting your entire communication and may use it for their own purposes, so be careful. There is also a 1,000-request limit on free models, with a 20 RPM limit if you're an OpenRouter user with at least $10 in credits.

Anyway, the most interesting thing about this model is that it's freaking good. After recent disappointments from models hyped by their marketing teams (looking at you [GLM 5.3]({% post_url 2026-08-19-evaluating-z-ai-glm-5.3-on-hack-the-box-challenges %}), and especially you [DeepSeek V4 Pro 0813]({% post_url 2026-08-18-evaluating-deepseek-deepseek-v4-pro-0813-on-hack-the-box-challenges %})), I didn't expect much from a model that came out of nowhere.

That's why, when I started my test harness for the {% include htb-challenger-benchmark-term.html %}, I was pleasantly surprised to see it crack one HTB challenge after another at a steady pace. In the end, it solved 15 out of 16 challenges, the same number as [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}), the best model I've tested so far.

In terms of score, it landed a few percentage points behind Sol (81.4% vs. 87.2%) because it was less efficient at solving the challenges. It needed a higher median number of steps (25 vs. 8.5) and tokens (0.54M vs. 0.09M).

But hey, who cares if it takes more tokens when it's free? 😄 The important part is that you now have three days of free access to a Sol-level model.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/stealth-ox-alpha-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 15
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 81.4%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 25 | 562 |
| Model cost | $0.00 | $0.00 |
| Duration | 00:10:13 | 06:37:20 |
| Number of input tokens | 0.52M | 16.69M |
| Number of output tokens | 0.02M | 0.67M |
| Number of `read_file` tool calls | 1.0 | 27 |
| Number of `write_file` tool calls | 2.5 | 70 |
| Number of `execute_command` tool calls | 21.5 | 521 |
| Number of `web_search` tool calls | 0.0 | 2 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 3 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 1 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 95.2% | 94.3% | 90.5% | 64.8% |
| **Median per challenge** | | | | |
| Model steps | 18 | 18.5 | 19 | 57.5 |
| Model cost | $0.00 | $0.00 | $0.00 | $0.00 |
| Duration | 00:03:03 | 00:06:10 | 00:17:41 | 00:23:49 |
| Number of input tokens | 0.18M | 0.27M | 0.42M | 2.32M |
| Number of output tokens | 0.01M | 0.01M | 0.02M | 0.03M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 0.5 | 1.5 |
| Number of `write_file` tool calls | 2.0 | 2.5 | 3.0 | 4.5 |
| Number of `execute_command` tool calls | 16.0 | 14.0 | 16.0 | 62.5 |
| Number of `web_search` tool calls | 0.0 | 0.5 | 0.0 | 0.0 |
