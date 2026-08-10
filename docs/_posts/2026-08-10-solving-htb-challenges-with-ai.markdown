---
layout: post
title:  "Introducing HTB-Challenger: Benchmarking LLM models on Hack The Box Challenges"
date:   2026-08-10 14:30:47 +0000
image:  /assets/images/htb-challenger-benchmark-logo-full.png
author: TheArtificialQ
hn_id:  
---

Choosing an LLM model for offensive security work is difficult. Public benchmarks can help compare model capabilities, but they rarely show how much it costs to complete a task from start to finish. The price per million tokens does not tell the whole story: different models may require vastly different numbers of tokens and tool calls before they solve a problem - or fail to solve it.

On top of that, as Winston Churchill allegedly said, “The only statistics you can trust are those you falsified yourself.”

I previously spent a lot of time evaluating new LLMs on offensive security tasks with [Strix](https://github.com/usestrix/strix). I am still enthusiastic about Strix, and it remains my go-to tool for penetration testing, but it is no longer the best fit for the repeated model comparisons I want to run.

Strix performs autonomous security testing against complex applications, so a single run can require many steps, tool calls, and tokens. That makes repeated testing expensive. Strix is also evolving rapidly and [improving with each version]({% post_url 2026-06-29-how-much-better-is-strix-1-0-results-from-a-small-rerun %}). Results produced with different versions are therefore not directly comparable: changes in the agent could be mistaken for changes in model performance. A fair comparison would require pinning one Strix version and rerunning every model against it.

I therefore revived an older idea and turned it into my new testing approach: the [HTB-Challenger Benchmark]({{ "/htb-challenger-benchmark" | relative_url }}).

<!--more-->

## What HTB-Challenger measures

The idea is simple: let an LLM-driven agent attempt [Hack The Box Challenges](https://help.hackthebox.com/en/articles/5185436-how-to-play-challenges), then record its success rate, cost per task, number of steps, and other execution metrics. The reported cost covers the model usage for an entire challenge attempt, making it more meaningful for this benchmark than token pricing alone.

This is a challenge benchmark, not a proxy for a full penetration test or a red-team engagement. It measures performance on isolated tasks with clearly defined objectives and verifiable flags. Its purpose is to provide a repeatable indication of hands-on security problem-solving ability under controlled conditions.

The project sounded like something I could finish in a weekend. As the meme goes, I did it not because it was easy, but because I thought it would be easy. It took far longer than anticipated, but I am happy with the result. For details about the challenge set, run limits, scoring, and test harness, see the [HTB-Challenger Benchmark Methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) page.

## Initial model results

The initial release includes three model configurations, each covered in a separate short post:

- [Solving Hack The Box Challenges with GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %})
- [Solving Hack The Box Challenges with GPT-5.6 Luna Pro]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %})
- [Solving Hack The Box Challenges with Kimi K3]({% post_url 2026-08-09-solving-htb-challenges-with-moonshotai-kimi-k3 %})

If you want to jump straight to the overall results, visit the [HTB-Challenger Benchmark]({{ "/htb-challenger-benchmark" | relative_url }}) page.

This is an ongoing project, and I will continue adding results for new models. If you find it useful, subscribe to the RSS feed linked at the bottom of the page to be notified about new posts or [follow me on X](https://x.com/TheArtificialQ).
