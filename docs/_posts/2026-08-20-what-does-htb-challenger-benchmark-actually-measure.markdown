---
layout: post
title:  "What Does the HTB-Challenger Benchmark Actually Measure?"
date:   2026-08-20 10:15:50 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
---

I'm sure many of you have come to this blog, checked the {% include htb-challenger-benchmark-term.html %} results for your favorite model and wondered why they differ so much from official benchmarks or your own experience. _"DeepSeek V4 Flash is the best model I have ever used. How could this moron put it at the bottom of his benchmark?!?"_ I hear you shouting.

And fair enough. If you use the model through Cursor, Claude Code, OpenCode, or another modern application, I agree that my results may have little to do with your experience. But if you're wondering how the model would perform in your own pentesting or security testing harness, I think you should look at them carefully.

And because I realized that I had done a really poor job of explaining what my benchmark actually measures, I put together this post to clarify it.

<!--more-->

### Use Cases

The first obvious reason why scores in my benchmark may not match your experience is that my benchmark focuses on testing models' cybersecurity problem-solving capabilities, i.e., how well they solve security-related challenges. If you use the same model for coding, research, data analysis, or other types of work, your experience could be different.

### Test Harness

But there is another reason - and, I believe, a stronger one - why scores in my benchmark may surprise you: the test harness.

#### What Is a Harness?

The issue with LLMs is that they essentially do only one thing: you send them a message, and they send you a response. They cannot automatically execute a multi-step process, they do not have persistent memory, and they cannot read files from your disk or search the internet. So when you need to do any serious work with them (such as measuring their performance on a benchmark), you need to wrap them in an application that adds all this missing functionality. Such applications are typically called **harnesses**, and real-world examples include Claude Code, Codex, and Cursor (if you're a developer); Strix, Shannon, and PentestGPT (if you're a pentester) and even general-purpose web apps such as ChatGPT and Claude.ai.

A common misconception is that these harnesses are boring applications that merely provide the model with an environment, tools, and potentially additional skills without adding any real value to the final outcome. Well, this is not entirely true: the harness is crucial to the model's overall performance (see [Harness-Bench](https://arxiv.org/abs/2605.27922) and [The Scaffold Effect](https://arxiv.org/abs/2607.22585) if you're interested in the details).

One function of a well-designed harness - and this is where it gets interesting - is to mitigate or contain some model failures. Current LLMs can still hallucinate, produce unsupported results, repeat unproductive actions, or fail to follow instructions precisely. A harness can reduce the impact of these behaviors by validating its actions or final answer, limiting loops and resource use, and asking it - or a separate model - to retry or re-evaluate a result.

As a result, what you observe - whether in everyday use or in a benchmark - is the behavior of the **LLM + harness** combination, not the model alone. And that brings us back to my benchmark.

#### How Does the HTB-Challenger Harness Work?

When I started working on the {% include htb-challenger-benchmark-term.html %}, I wanted it to measure the models' behavior, not the sophistication of the harness. I therefore kept its safeguards and recovery mechanisms to a minimum:

For this reason, I kept the mechanisms in my test harness that mitigate or work around model flaws to a minimum. In practice, this is how the harness responds to such failures:

- When the model reports an incorrect result, I do not ask how confident it is or whether it can revalidate the result. I accept its result, and if it is wrong, I mark it as a false positive and the model gets 0 points.
- When the model takes many more steps or spends much more money than usual on a given test, I stop the test and the model gets 0 points.
- When the model gets stuck (and this is an area that deserves its own blog post), I try once to get it back on track. If that doesn't help, I stop the test and the model gets 0 points.

The scores therefore reflect both cybersecurity problem-solving ability and operational reliability under minimal hand-holding. Hallucinations, unsupported submissions, and repeated unproductive actions can lower a model's score despite strong cybersecurity skills.

And this is what makes this benchmark different - and why not everyone is happy with the results. But if you plan to use a model in your own harness, particularly one without sophisticated safeguards and recovery mechanisms, these results can help you understand which failures and behaviors you need to prepare for.
