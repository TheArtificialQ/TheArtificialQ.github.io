---
layout: post
title:  "Case Study: Combining GPT-5.6 Luna and Sol for Cost-Efficient AI"
date:   2026-08-24 10:40:18 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

So far, I have used my {% include htb-challenger-benchmark-term.html %} to test how well more than 15 LLMs can solve Hack The Box challenges, and two have become personal favorites.

The first is [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}). Its overall score was not high, but it was solid on simpler tasks and, most importantly, it was extremely cheap.

My other favorite sits at the opposite end of the performance ranking and is also from OpenAI: [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}). It is the best-performing model I have tested so far, but that performance comes at a price. Its overall median cost per challenge was about 16 times higher than Luna's, although the ratio varied substantially by difficulty.

So I wondered: wouldn't it be great if you could use both models in one workflow and reduce the cost by automatically switching between them when a task becomes too difficult for Luna? You could start with Luna and bring in Sol only when the task exceeds Luna's capabilities. In theory, this should deliver almost Sol-level performance at a much lower cost.

After a few dead ends, I found a solution that worked for my use case and that I could use to solve Hack The Box challenges. In this post, I briefly explain what I did and what the results were.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

## Building model escalation into the harness

The first question is how to switch from a cheaper, less capable model to a more capable, expensive one at the right moment.

I won't waste your time talking about the unsuccessful solutions I tried or considered, such as manually switching models with a human in the loop, OpenRouter's [Auto Router model](https://openrouter.ai/openrouter/auto), and various open-source tools.

In the end, I realized something. I run my tests with a simple harness that gives models a standard set of tools (see the [methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) page for more details). One of these tools is `give_up`: the model can call it when it runs out of productive ideas and continuing the test would not be worthwhile. Most models don't have enough self-reflection to use this tool at all, but all OpenAI models are great at using it, including the Luna model.


So what if, I wondered, I gave the model another tool that allowed it to escalate the problem to a more capable model instead of giving up? I added a new tool called `hand_over_to_more_capable_model` with this description:

```
Hand the current investigation and its complete conversation history to the next, 
more capable configured model when this task appears too difficult for you to 
solve productively. Use this instead of give_up when a more capable model should 
continue the work.
```

And this simple solution worked very well. The Luna model turned out to be really good at detecting the right moment to hand over the task to its more capable sibling, and the whole harness, including switching to the Sol model, worked like a charm.

## The results

The most important result is shown in this graph. The model's position is determined by its median cost per challenge on the x-axis and its benchmark score on the y-axis:

<object data="{{ "/assets/images/openai-gpt-5.6-luna-20260709%3Bopenai-gpt-5.6-sol-20260709-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/openai-gpt-5.6-luna-20260709%3Bopenai-gpt-5.6-sol-20260709-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

The **GPT-5.6 Luna + GPT-5.6 Sol** combination scored lower than **GPT-5.6 Sol** alone (74.5% versus 87.2%) but much higher than **GPT-5.6 Luna** alone (31.6%). The two-model system stood out most clearly on median cost per challenge, especially when you switch the scale from logarithmic to linear. Its median cost was $0.07, about 4.4 times lower than Sol's $0.29. [Grok 4.6]({% post_url 2026-08-12-solving-htb-challenges-with-x-ai-grok-4.6 %}) and [Kimi K3]({% post_url 2026-08-09-solving-htb-challenges-with-moonshotai-kimi-k3 %}) achieved broadly similar benchmark scores, but their median costs were much higher at $0.23 and $0.46, respectively.

In summary, if your use case and harness allow you to combine models and escalate between them using a simple new tool, this approach is worth testing. Technically, it is a simple solution, and I'm sure it could be improved further, so the final gains could be even greater for you.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/openai-gpt-5.6-luna-20260709%3Bopenai-gpt-5.6-sol-20260709-model-card.svg" | relative_url }})


## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 14
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 1
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 1
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 74.5%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 20 | 372 |
| Model cost | $0.07 | $6.87 |
| Duration | 00:06:02 | 01:41:36 |
| Number of input tokens | 0.59M | 14.64M |
| Number of output tokens | 0.02M | 0.24M |
| Number of `read_file` tool calls | 0.0 | 31 |
| Number of `write_file` tool calls | 0.0 | 23 |
| Number of `execute_command` tool calls | 24.0 | 512 |
| Number of `web_search` tool calls | 0.0 | 5 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 2 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 1 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 1 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 97.2% | 94.7% | 94.8% | 43.4% |
| **Median per challenge** | | | | |
| Model steps | 7.5 | 22 | 21 | 34.5 |
| Model cost | $0.01 | $0.03 | $0.31 | $0.35 |
| Duration | 00:01:18 | 00:04:24 | 00:05:21 | 00:12:33 |
| Number of input tokens | 0.07M | 0.44M | 0.59M | 1.96M |
| Number of output tokens | 0.00M | 0.01M | 0.02M | 0.02M |
| Number of `read_file` tool calls | 0.0 | 1.0 | 0.0 | 3.0 |
| Number of `write_file` tool calls | 0.0 | 0.0 | 0.0 | 0.5 |
| Number of `execute_command` tool calls | 10.0 | 19.0 | 24.5 | 48.5 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
