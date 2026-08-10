---
layout: page
title: HTB-Challenger Benchmark
permalink: /htb-challenger-benchmark/
header_image: /assets/images/htb-challenger-benchmark-bg.png
header_alt: HTB-Challenger Benchmark
---

*Last updated: 2026-08-10 15:30:47 UTC*

The HTB-Challenger Benchmark measures how well large language models solve a fixed set of 16 recent Hack The Box cybersecurity challenges in a controlled environment. For more information, visit the [HTB-Challenger Benchmark Methodology page]({{ "/htb-challenger-benchmark-methodology" | relative_url }}).

This is an ongoing project, and new models are added as they are tested.

## Cost vs. Benchmark Score

Each point represents one model; models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="420" aria-label="Interactive Cost vs. Benchmark Score chart">
  <img src="{{ "/assets/images/cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score" width="800">
</object>

## Benchmark metrics

All metrics except Score are reported per challenge and calculated as medians to reduce the impact of extreme values.

Click a model name in the table to view more details about its benchmark results.

| Model | Score | Cost | Steps | Duration | Input tokens | Output tokens |
| ---  | ---: | ---: | ---: | ---: | ---: | ---: |
| <img src="{{ "/assets/images/moonshotai-icon.svg" | relative_url }}" alt="moonshotai icon" width="22" height="22"> [`moonshotai/kimi-k3`]({% post_url 2026-08-09-solving-htb-challenges-with-moonshotai-kimi-k3 %}) | 75.0% | $0.46 | 22.0 | 00:07:34 | 0.33M | 0.02M |
| <img src="{{ "/assets/images/openai-icon.svg" | relative_url }}" alt="openai icon" width="22" height="22"> [`openai/gpt-5.6-luna-pro`]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna-pro %}) | 55.0% | $0.10 | 21.5 | 00:08:55 | 1.50M | 0.07M |
| <img src="{{ "/assets/images/openai-icon.svg" | relative_url }}" alt="openai icon" width="22" height="22"> [`openai/gpt-5.6-luna`]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}) | 32.5% | $0.02 | 17.5 | 00:04:38 | 0.34M | 0.02M |

## Honorable mentions

I also attempted to run the benchmark with the following frontier models from Anthropic and OpenAI:

- **anthropic/claude-opus-4.8**
- **anthropic/claude-opus-5**
- **anthropic/claude-fable-5**
- **openai/gpt-5.6-terra**
- **openai/gpt-5.6-sol**

Unfortunately, each of these models eventually refused to continue testing, returning messages such as: “This content was flagged for possible cybersecurity risk.” As a result, these models are not included in the benchmark results.

{% include hyvortalk_comments.html %}
