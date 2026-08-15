---
layout: page
title: HTB-Challenger Benchmark
permalink: /htb-challenger-benchmark/
header_image: /assets/images/htb-challenger-benchmark-bg.png
header_alt: HTB-Challenger Benchmark
---

*Last updated: 2026-08-15 07:20:25 UTC*

The HTB-Challenger Benchmark measures how well large language models solve a fixed set of 16 recent Hack The Box cybersecurity challenges in a controlled environment. For more information, visit the [HTB-Challenger Benchmark Methodology page]({{ "/htb-challenger-benchmark-methodology" | relative_url }}).

This is an ongoing project, and new models are added as they are tested.

## Cost vs. Benchmark Score

Each point represents one model; models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart">
  <img src="{{ "/assets/images/cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score" width="800" height="550">
</object>

## Benchmark metrics

All metrics except Score are reported per challenge and calculated as medians to reduce the impact of extreme values.

Click a model name in the table to view more details about its benchmark results.

| Model | Score | Cost | Steps | Duration | Tokens |
| ---  | ---: | ---: | ---: | ---: | ---: |
| <img src="{{ "/assets/images/x-ai-icon.svg" | relative_url }}" alt="x-ai icon" width="22" height="22"> [`Grok 4.6`]({% post_url 2026-08-12-solving-htb-challenges-with-x-ai-grok-4.6 %}) | 76.1% | $0.23 | 14.0 | 00:03:38 | 0.24M |
| <img src="{{ "/assets/images/moonshotai-icon.svg" | relative_url }}" alt="moonshotai icon" width="22" height="22"> [`Kimi K3`]({% post_url 2026-08-09-solving-htb-challenges-with-moonshotai-kimi-k3 %}) | 70.7% | $0.46 | 22.0 | 00:07:34 | 0.35M |
| <img src="{{ "/assets/images/qwen-icon.svg" | relative_url }}" alt="qwen icon" width="22" height="22"> [`Qwen3.8 Max`]({% post_url 2026-08-11-solving-htb-challenges-with-qwen-qwen3.8-max %}) | 54.8% | $2.00 | 29.0 | 00:15:32 | 0.96M |
| <img src="{{ "/assets/images/openai-icon.svg" | relative_url }}" alt="openai icon" width="22" height="22"> [`GPT-5.6 Luna Pro`]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}) | 51.3% | $0.10 | 21.5 | 00:08:55 | 1.57M |
| <img src="{{ "/assets/images/deepseek-icon.svg" | relative_url }}" alt="deepseek icon" width="22" height="22"> [`DeepSeek V4 Pro`]({% post_url 2026-08-12-solving-htb-challenges-with-deepseek-deepseek-v4-pro %}) | 36.2% | $0.35 | 62.5 | 00:06:19 | 1.94M |
| <img src="{{ "/assets/images/openai-icon.svg" | relative_url }}" alt="openai icon" width="22" height="22"> [`GPT-5.6 Luna`]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}) | 31.6% | $0.02 | 17.5 | 00:04:38 | 0.36M |
| <img src="{{ "/assets/images/deepseek-icon.svg" | relative_url }}" alt="deepseek icon" width="22" height="22"> [`DeepSeek V4 Flash 0731`]({% post_url 2026-08-11-solving-htb-challenges-with-deepseek-deepseek-v4-flash-0731 %}) | 8.2% | $0.00 | 14.5 | 00:02:29 | 0.10M |

## Honorable mentions

I also attempted to run the benchmark with the following frontier models from Anthropic and Google:

- **Claude Opus 4.8**
- **Claude Opus 5**
- **Claude Fable 5**
- **Gemini 3.7 Flash**

Unfortunately, each of these models eventually refused to continue testing, returning messages such as: “This content was flagged for possible cybersecurity risk.” As a result, these models are not included in the benchmark results.

{% include hyvortalk_comments.html %}
