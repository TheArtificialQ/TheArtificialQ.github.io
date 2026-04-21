---
layout: post
title:  "Kimi K2.6 with Strix: a quick test"
date:   2026-04-21 09:00:00 +0100
image:  /assets/images/2026-04-21-ModelScoreRanges-kimi-k26.png
author: TheArtificialQ
hn_id:  47847091
---

The [Kimi K2.6](https://www.kimi.com/blog/kimi-k2-6) was released just yesterday, and looking at the benchmarks quoted in the release blog post, one could easily get the impression that it is the best model ever released. So I decided to do a quick test.

<!--more-->

For this quick check, I used the same Strix lab, three-run setup, and CVSS-based scoring as in my [Agentic AI pentesting with Strix: results from 18 LLM models]({% post_url 2026-04-14-agentic-ai-pentesting-with-strix-results-from-18-llm-models %}) post from last week. I ran the model through [OpenRouter](https://openrouter.ai/moonshotai/kimi-k2.6).

The first chart shows the score range across the three runs. The second compares performance with average cost per run.

![Model Score Ranges]({{ "/assets/images/2026-04-21-ModelScoreRanges-kimi-k26.png" | relative_url }})

![Model Performance]({{ "/assets/images/2026-04-21-ModelPerformance-kimi-k26.png" | relative_url }})

In short, K2.6 performed better than K2.5 in this setup. That is impressive because K2.5 was already one of the strongest lower-cost models in my previous testing. The trade-off is price: on OpenRouter, the average cost per run was almost three times higher than for K2.5.
