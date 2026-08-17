---
layout: post
title:  "Solving Hack The Box Challenges with DeepSeek V4 Flash 0731"
date:   2026-08-11 20:22:58 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

I tested the previous version of DeepSeek V4 Flash, now called **DeepSeek V4 Flash 0423**, with [Strix back in April]({% post_url 2026-04-25-deepseek-v4-with-strix-a-quick-test %}), and I absolutely fell in love with it. It delivered great results at a very low price and became my go-to model for most tasks that didn't require the capabilities of frontier models.

That's why I was looking forward to testing the latest, improved version on my {% include htb-challenger-benchmark-term.html %}. But the results... Oh dear, oh dear, oh dear. Where do I even start?

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

Okay, let's start with the results: they are bad. It solved just 2 out of 16 HTB challenges and scored 8.2% on my benchmark. But that's not the worst or most puzzling thing about this model.

What worried me more was the number of false positives: it reported incorrect flags in 9 challenges. Sometimes these flags were completely made up, like `HTB{...}` or `HTB{dummy}`. In other cases, it submitted a fake flag from the attached source code or a random string that seemed to come out of nowhere. To put this into perspective, not one of the other models I've tested so far has reported even a single incorrect flag.

Another worrying thing was how badly this model used tools. Multiple times, I saw it call the `execute_command` tool with an empty command or with random text instead of a command. Similarly, it called the `write_file` tool several times with no file content. Again, none of the other models I've tested did this even once.

Yes, the model was cheap. The median test cost was a fraction of a cent, but in terms of results, I got what I paid for.

## So what went wrong?

I spent quite a lot of time wondering why the results were so bad, especially after the previous version did so well in my Strix test. The best explanation I could come up with is this:

During my HTB-Challenger testing, I don't provide the model with task-specific guidance in the form of skills or special instructions for each security domain. I also don't tell it how to approach the job or validate its findings to avoid false positives. This is deliberate: the goal is to test the model's built-in offensive-security capabilities.

This is very different from how tools like [Strix](https://github.com/usestrix/strix) work. They provide the model with skills and detailed instructions that guide it through the different phases of testing and help it validate its findings. My best guess is that this extra scaffolding made the difference: DeepSeek V4 Flash can perform well within a highly structured agent, but it struggles badly when it has to plan its own approach, use tools reliably, and validate findings with much less guidance.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/deepseek-deepseek-v4-flash-20260731-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/deepseek-deepseek-v4-flash-20260731-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/deepseek-deepseek-v4-flash-20260731-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 2
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 9
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 3
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 1
- **Benchmark score:** 8.2%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 14.5 | 443 |
| Model cost | $0.00 | $0.50 |
| Duration | 00:02:29 | 03:02:54 |
| Number of input tokens | 0.10M | 11.71M |
| Number of output tokens | 0.00M | 0.44M |
| Number of `read_file` tool calls | 2.5 | 56 |
| Number of `write_file` tool calls | 0.5 | 33 |
| Number of `execute_command` tool calls | 13.5 | 360 |
| Number of `web_search` tool calls | 2.0 | 30 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 1 | 0 | 1 | 0 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 2 | 2 | 2 | 3 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 2 | 1 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 1 | 0 | 0 | 0 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 1 |
| Benchmark score | 24.9% | 0.0% | 19.1% | 0.0% |
| **Median per challenge** | | | | |
| Model steps | 34 | 12 | 16.5 | 13.5 |
| Model cost | $0.04 | $0.00 | $0.00 | $0.03 |
| Duration | 00:24:50 | 00:01:42 | 00:01:06 | 00:10:41 |
| Number of input tokens | 0.69M | 0.07M | 0.15M | 0.35M |
| Number of output tokens | 0.05M | 0.00M | 0.00M | 0.02M |
| Number of `read_file` tool calls | 3.0 | 2.0 | 2.0 | 7.0 |
| Number of `write_file` tool calls | 1.5 | 0.0 | 2.0 | 2.0 |
| Number of `execute_command` tool calls | 28.5 | 10.0 | 14.5 | 11.0 |
| Number of `web_search` tool calls | 2.5 | 2.0 | 1.0 | 1.5 |
