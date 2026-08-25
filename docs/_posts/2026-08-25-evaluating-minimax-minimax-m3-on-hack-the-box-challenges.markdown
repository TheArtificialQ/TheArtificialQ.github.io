---
layout: post
title:  "Evaluating MiniMax M3 on Hack The Box Challenges"
date:   2026-08-25 11:32:39 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

While we wait to see whether MiniMax releases its reported 2.7-trillion-parameter successor, [known internally as **MiniMax M3 Pro** and potentially arriving as early as the third quarter](https://www.theinformation.com/briefings/exclusive-chinas-minimax-plans-launch-2-7-trillion-parameter-model), I decided to return to **MiniMax M3**, released at the end of May, and run it through my {% include htb-challenger-benchmark-term.html %}. I know that M3 has many fans, but I had never used or tested it, so I wasn't sure what to expect.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

After trying many LLMs on cybersecurity tasks, I have repeatedly seen non-frontier models fall into loops when you ask them to do something beyond their capabilities.

These loops can take two forms:

- The model makes the exact same tool call, with the same arguments, over and over again.
- The model starts producing "never-ending" reasoning full of phrases such as *"Wait, let me re-read..."* and *"Actually, let me think about this differently"*, without making any visible progress.

A clear example of repeated identical tool calls is [DeepSeek V4 Pro 0813]({% post_url 2026-08-18-evaluating-deepseek-deepseek-v4-pro-0813-on-hack-the-box-challenges %}), which ended four of my 16 benchmark runs this way.

The second failure mode was more common. [GLM 5.3]({% post_url 2026-08-19-evaluating-z-ai-glm-5.3-on-hack-the-box-challenges %}) hit this issue in three of 16 runs. The absolute "champion" was [Hy3]({% post_url 2026-08-17-evaluating-tencent-hy3-on-hack-the-box-challenges %}), which did so in nine of 16 runs.

Well, **MiniMax M3** is unfortunately another model where this issue prevents it from finishing more difficult tasks. Half of the 16 challenges ended in never-ending loops, and as a result, its final score was poor.

Its $0.16 median cost per challenge was not especially high across the full benchmark, but the value was weak compared with nearby peers. [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}) scored 31.6% at a median cost of $0.02, while [Hy3]({% post_url 2026-08-17-evaluating-tencent-hy3-on-hack-the-box-challenges %}) scored 34.8% at $0.08. Given M3's low score and high rate of stuck runs in these tests, there is not much positive I can say about its performance in this benchmark.


---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/minimax-minimax-m3-20260531-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/minimax-minimax-m3-20260531-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/minimax-minimax-m3-20260531-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 7
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 8
- **Benchmark score:** 30.5%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 26.5 | 593 |
| Model cost | $0.16 | $3.08 |
| Duration | 00:07:45 | 02:46:11 |
| Number of input tokens | 0.36M | 13.14M |
| Number of output tokens | 0.07M | 1.57M |
| Number of `read_file` tool calls | 0.0 | 24 |
| Number of `write_file` tool calls | 0.0 | 32 |
| Number of `execute_command` tool calls | 23.5 | 615 |
| Number of `web_search` tool calls | 0.0 | 5 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 3 | 2 | 2 | 0 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 1 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 1 | 2 | 2 | 3 |
| Benchmark score | 61.7% | 47.9% | 49.0% | 0.0% |
| **Median per challenge** | | | | |
| Model steps | 61 | 19 | 12 | 27.5 |
| Model cost | $0.29 | $0.14 | $0.07 | $0.21 |
| Duration | 00:13:23 | 00:09:34 | 00:04:09 | 00:07:45 |
| Number of input tokens | 1.01M | 0.15M | 0.14M | 0.75M |
| Number of output tokens | 0.11M | 0.11M | 0.04M | 0.07M |
| Number of `read_file` tool calls | 2.0 | 2.5 | 0.0 | 0.0 |
| Number of `write_file` tool calls | 0.0 | 1.0 | 0.0 | 0.0 |
| Number of `execute_command` tool calls | 47.0 | 21.0 | 10.0 | 32.5 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
