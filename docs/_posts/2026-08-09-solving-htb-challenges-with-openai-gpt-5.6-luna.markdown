---
layout: post
title:  "Evaluating GPT-5.6 Luna on Hack The Box Challenges"
date:   2026-08-10 15:30:47 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

My first thought was: let's kick off the {% include htb-challenger-benchmark-term.html %} with some state-of-the-art models. Let's see what these Fables, Opuses, Terras and Sols can do with offensive security challenges. As it turned out, not much - sooner or later, all of them refused to continue with the HTB challenge-solving workflow, with messages like “This content was flagged for possible cybersecurity risk.” So I was left with just GPT-5.6 Luna. And it was not so bad after all.

> **Update (17 August 2026):** I have since solved the refusal issue with GPT-5.6 Terra and Sol by joining OpenAI's Trusted Access for Cyber program. You can read about the solution and see my [test results for the full GPT-5.6 family]({% post_url 2026-08-17-solving-htb-challenges-with-openai-gpt-5.6 %}).

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

The main quality of GPT-5.6 Luna is its price - it's unbelievably cheap! The median model cost per HTB challenge was $0.02, which is virtually free. Its results were not the best: it solved all Very Easy challenges and three out of four Easy ones, but only one Medium challenge and no Hard challenges. It clearly started to lose its breath as the difficulty increased.

Still, for simple, clearly scoped CTF-style tasks, I would always try this model first. If it doesn't produce useful results, I would move to a more capable (and more expensive) model. This should save you a lot of money in the long term.

Also check out the results for [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}). It is slightly more expensive, but it also performed better.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-luna-20260709-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/openai-gpt-5.6-luna-20260709-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/openai-gpt-5.6-luna-20260709-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 8
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 8
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 31.6%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 17.5 | 431 |
| Model cost | $0.02 | $0.58 |
| Duration | 00:04:38 | 02:03:31 |
| Number of input tokens | 0.34M | 16.84M |
| Number of output tokens | 0.02M | 0.32M |
| Number of `read_file` tool calls | 1.0 | 39 |
| Number of `write_file` tool calls | 0.0 | 12 |
| Number of `execute_command` tool calls | 28.0 | 609 |
| Number of `web_search` tool calls | 0.0 | 3 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 3 | 1 | 0 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 1 | 3 | 4 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 97.8% | 72.1% | 24.7% | 0.0% |
| **Median per challenge** | | | | |
| Model steps | 11.5 | 15.5 | 25 | 40 |
| Model cost | $0.01 | $0.01 | $0.05 | $0.06 |
| Duration | 00:01:56 | 00:05:04 | 00:09:07 | 00:13:30 |
| Number of input tokens | 0.11M | 0.27M | 0.96M | 1.93M |
| Number of output tokens | 0.00M | 0.01M | 0.03M | 0.03M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 0.5 | 2.0 |
| Number of `write_file` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
| Number of `execute_command` tool calls | 11.5 | 24.5 | 33.0 | 60.0 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
