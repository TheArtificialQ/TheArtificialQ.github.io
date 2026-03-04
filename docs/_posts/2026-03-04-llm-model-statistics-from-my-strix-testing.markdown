---
layout: post
title:  "LLM model statistics from my Strix testing"
date:   2026-03-04 00:00:00 +0100
author: TheArtificialQ
hn_id:  
---

In my [previous post]({% post_url 2026-03-01-strix-first-impressions %}) I summarized a few impressions from my **[strix](https://github.com/usestrix/strix)** testing (TL;DR I was impressed).

Since then, I have collected some hard data and summarized it on [this page]({{ '/ai-offsec-benchmarks/' | relative_url }}). I still haven't run enough tests to be able to objectively compare different models, but I believe that page is not a bad starting point when selecting an LLM model for your own testing.

Beyond the numbers, here are some short personal observations for each model.

<!--more-->

### gpt-5.3-codex

It was a clear winner of my testing. It not only had good results, but it was also quick and relatively cheap.

I noticed just one thing which worried me a bit - when using **strix** with this model, it was creating a lot of subagents. For example when it found a web site with a login form, it spawned 3-4 different subagents running at the same time, one looking for XSS, another for SQLi, another brute forcing the login form, etc. This works great, until it doesn't. These subagents can easily step on each other's toes and their results could be influenced by the activities of those other subagents. On top of that it can flood the target website with a lot of requests, causing some rate limiting mechanisms to kick in and block these requests. I must say that it went through those Hack The Box machines which I tested smoothly, but I saw glimpses of these issues when using **strix + gpt-5.3-codex** in other use cases.

This can probably be mitigated by setting the [`--scan-mode`](https://docs.strix.ai/usage/cli#param-scan-mode-m) parameter to `standard` or even `quick`, but it could have other side effects. Maybe the best solution would be to send some additional instructions using the [`--instruction-file`](https://docs.strix.ai/usage/cli#param-instruction-file) parameter, something like "You may create at most 2 subagents total, and never have more than 1 running at once." I haven't tested it yet, because, honestly, I got this idea while writing this post, but I'll very likely use these instructions during my future testing :-).

### gemini-3.1-pro-preview

It had slightly worse results than **gpt-5.3-codex**, it typically ran twice as long and cost twice as much, but still - it was arguably the most intelligent and entertaining model which I tested. It gives you much more insight into its thinking process and I always enjoyed sitting back in my chair and watching it work. Contrary to **gpt-5.3-codex**, it doesn't create subagents (I really don't remember any subagent created by this model) so it works in one uninterrupted flow which you can easily follow.

The only (cosmetic) issue is its overuse of the word "Wait". For example "Wait, I can try tyler's credentials here. Wait, I already tested them and it didn't work. Wait, but I can..." At first it was annoying, but then it became part of its charm to me :-)

### glm-5 and kimi-k2.5

I had no experience with these models before and they were a really nice surprise. Their results were not bad, especially with **kimi-k2.5**, which is quite cheap. If you are looking for open source alternatives to those big commercial AI models that can be hosted locally, these models are definitely worth testing.

### deepseek-v3.2

This was the biggest disappointment of my testing. Despite its famous name, this model failed on all fronts. Bad results combined with the highest average price per test and the longest time needed for test completion were enough for me to exclude this model from any further testing.

### gpt-5-mini and gpt-5-nano

My [page with test results]({{ '/ai-offsec-benchmarks/' | relative_url }}) contains just one test for **gpt-5-mini**, but I used it multiple times, together with **gpt-5-nano**. Unfortunately I didn't collect statistics for all those tests, but they were very consistent - low price per test, but virtually no successful findings.

### Honorable mention: stepfun/step-3.5-flash:free

Unfortunately, this is another model where I didn't properly collect all statistics, so it's missing in my results, but this model had better results than **gpt-5-mini** and **gpt-5-nano** and it has one indisputable quality - you can use it for free when you create an account on [OpenRouter.ai](https://openrouter.ai). It's ideal when you are setting up your test environment to verify that everything works as expected before you switch to some paid model.

## Conclusion

I'm sure there are many other interesting models, but there is only so much time and money I can spend on this testing. I tried to conduct my tests on models from different categories (from state-of-the-art to open source, low-end and free models) to get a sense of the differences between them and I'm quite happy with what I found.

I would like to continue my testing when time permits so hopefully I'll have more data in the next few weeks.