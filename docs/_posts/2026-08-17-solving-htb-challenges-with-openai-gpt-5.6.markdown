---
layout: post
title:  "Evaluating GPT-5.6 on Hack The Box Challenges"
date:   2026-08-17 06:10:31 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

Until now, I had tested only the GPT-5.6 Luna model because the two more advanced GPT-5.6 models, Terra and Sol, rejected my test prompts, flagging them as a "possible cybersecurity risk." Fortunately, this issue turned out to have an easy solution, so I could finally spend a couple of days testing the whole GPT-5.6 family for my {% include htb-challenger-benchmark-term.html %}.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

## Trusted Access for Cyber program

When I started testing a week or so ago, I couldn't run my test harness with the GPT-5.6 Terra or Sol models - I kept getting this error: `This content was flagged for possible cybersecurity risk. If this seems wrong, try rephrasing your request. To get authorized for security work, join the Trusted Access for Cyber program: https://chatgpt.com/cyber`. At first, I gave up. Trying to join the Trusted Access for Cyber program seemed pointless to me. I was sure the whole program had been created just to give desperate OpenAI users some hope and that my application would end up in `/dev/null`.

But then I discovered [some articles](https://ai.georgeliu.com/p/chatgpt-codex-flagged-my-security) that gave me real hope, so I clicked on the [https://chatgpt.com/cyber](https://chatgpt.com/cyber) link. As it turned out, joining the Trusted Access for Cyber program only involved going through a KYC process similar to the one required when opening a new bank account. After I joined the program, only one of my prompts was rejected, which was a significant improvement.


## Tested models

I tested the following GPT-5.6 models. Click on a model name to see its detailed test results:

- [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %})
- [GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %})
- [GPT-5.6 Terra]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-terra %})
- [GPT-5.6 Terra Pro]({% post_url 2026-08-14-solving-htb-challenges-with-openai-gpt-5.6-terra-pro %})
- [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %})

> **GPT-5.6 Luna Pro** and **GPT-5.6 Terra Pro** are models hosted on [OpenRouter.io](https://openrouter.ai), and they are simply the **Luna** and **Terra** models served with `reasoning.mode` set to `pro`.

I also tested the **GPT-5.6 Sol Pro** model, but the results were, well, weird. The **Sol Pro** version generated a lot of tokens and took a long time on each step, but that did not always translate into better results. I also have a hard limit of $15 on the cost of a single test run, and this model hit that limit quite often. I'm not sure if "overthinking" is the best technical term here, but that's what it looked like to me.

In the end, I decided not to include this model version in my results, but if there is one thing I can say based on my partial testing, it is that **GPT-5.6 Sol Pro** is much more expensive than **GPT-5.6 Sol**.

## Results

Let's start with this chart. The five GPT-5.6 models tested for this post are highlighted in gold, so you can see their results in the context of the other models I have tested. The vertical axis shows the score on my {% include htb-challenger-benchmark-term.html %}, while the horizontal axis shows the median cost per test (mind you, this axis uses a logarithmic scale).

<object data="{{ "/assets/images/cost-vs-benchmark-score-gpt-5.6.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart (GPT 5.6)">
  <img src="{{ "/assets/images/cost-vs-benchmark-score-gpt-5.6.svg" | relative_url }}" alt="Cost vs. Benchmark Score (GPT 5.6)" width="800" height="550">
</object>

Before I start interpreting these results, let me also show you a table with more statistics for each model.

| Metric | Luna | Luna Pro | Terra | Terra Pro | Sol |
| --- | ---: | ---: | ---: | ---: | ---: |
| **Results** | | | | | |
| Number of challenges | 16 | 16 | 16 | 16 | 16 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 8 | 11 | 12 | 14 | 15 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 | 1 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 8 | 4 | 4 | 1 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 1 | 0 | 0 | 0 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 | 0 |
| Benchmark score | 31.6% | 51.3% | 64.6% | 75.1% | 87.2% |
| **Median per challenge** | | | | | |
| Model steps | 17.5 | 21.5 | 16.5 | 11 | 8.5 |
| Model cost | $0.02 | $0.10 | $0.24 | $0.91 | $0.29 |
| Duration | 00:04:38 | 00:08:55 | 00:03:16 | 00:08:22 | 00:02:05 |
| Number of input tokens | 0.34M | 1.50M | 0.23M | 0.64M | 0.09M |
| Number of output tokens | 0.02M | 0.07M | 0.01M | 0.03M | 0.00M |
| Number of `read_file` tool calls | 1.0 | 4.0 | 0.0 | 0.0 | 0.5 |
| Number of `write_file` tool calls | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| Number of `execute_command` tool calls | 28.0 | 36.5 | 15.5 | 13.5 | 8.5 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |

## What I take from these results

At the low-cost end, **Luna** is in a category of its own. A median challenge run cost just $0.02, which is remarkably cheap even by LLM standards. Its 31.6% benchmark score was the lowest in this comparison, but that doesn't tell the whole story: it still found the correct flag in seven of the eight Very Easy and Easy challenges. I see it as an ideal first-pass model - let **Luna** take a shot at the task, and bring in something more powerful only when it reaches its limits.

And then there is **Sol**. With a score of 87.2%, **GPT-5.6 Sol achieved the best score in my benchmark so far**. It solved 15 of 16 challenges, including three out of four Hard ones. What makes this result even more impressive is that its median cost was only $0.29 per challenge - just $0.05 more than **Terra** and less than one-third of **Terra Pro**'s $0.91. It was also the fastest model in this comparison, with a median of 8.5 steps and 2 minutes and 5 seconds per challenge. The only blemish in its results was a false positive on the remaining Hard challenge, which no model in my benchmark has solved so far. But this was not a random or nonsensical guess: the submitted flag was plausible and differed only slightly from the correct one. So even **Sol**'s only failure was actually a near miss.

The results of the Pro variants are a bit more complicated. Setting `reasoning.mode` to `pro` improved both underlying models: **Luna Pro** gained 19.7 percentage points over **Luna**, and **Terra Pro** gained 10.5 points over **Terra**. But this extra reasoning came at a price. **Luna Pro** was five times more expensive than **Luna**, while **Terra Pro** was almost four times more expensive than **Terra**. Both Pro variants also used roughly three to four times as many input tokens per challenge and took around two to three times as long. And in both cases, the next model tier still performed better than the Pro version of the lower tier: **Terra** beat **Luna Pro**, and **Sol** beat **Terra Pro**.

The differences become most visible as the challenges get harder. Every model scored at least 97% on Very Easy challenges, so paying for the most powerful model there doesn't make much sense. On Medium challenges, however, the scores ranged from 24.7% for **Luna** to 97.6% for **Sol**. On Hard challenges, they ranged from 0% for **Luna** to 71.8% for **Sol**.

So my practical conclusion is quite simple. If I had a straightforward task or wanted to run a large number of inexpensive experiments, I would start with **Luna**. If the task were difficult and getting the correct result mattered more than saving every last cent, I would choose **Sol**. **Luna Pro** is still an interesting and affordable middle ground, but **Terra** is difficult to recommend when **Sol** costs only slightly more and performs much better. **Terra Pro** makes even less sense to me: in these tests, **Sol** was more capable, faster, and much cheaper.
