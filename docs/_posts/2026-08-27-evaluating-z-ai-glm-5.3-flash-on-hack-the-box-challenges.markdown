---
layout: post
title:  "Evaluating GLM 5.3 Flash on Hack The Box Challenges"
date:   2026-08-28 07:57:22 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

I had already evaluated **GLM 5.3 Flash** when Z.ai previewed it anonymously as the mysterious [Ox Alpha]({% post_url 2026-08-21-evaluating-stealth-ox-alpha-on-hack-the-box-challenges %}) on OpenRouter, and its performance was fantastic. The one thing I couldn't measure was cost-effectiveness because the preview was free. Now that Z.ai has [revealed Ox Alpha as GLM 5.3 Flash](https://z.ai/blog/glm-5.3-flash) and published its pricing, I could return to it and measure the final missing piece.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

My new test closely reproduced the earlier **Ox Alpha** result: 81.4% in the anonymous preview run and 81.0% after release. It means, that **GLM 5.3 Flash** has the second-highest score after [GPT-5.6 Sol]({% post_url 2026-08-13-solving-htb-challenges-with-openai-gpt-5.6-sol %}) (87.2%). Both models correctly solved the same 15 out of 16 challenges. Flash's lower score came from requiring more model steps on the solved challenges: its median was 24.5, compared with Sol's 8.5.

Anyway, despite needing more steps and tokens, **GLM 5.3 Flash's** median cost per challenge was about one-twentieth of **GPT-5.6 Sol's** ($0.0140 vs. $0.2898). In this benchmark, that meant the same number of correct solves at a fraction of the measured cost. Flash was even cheaper than [GPT-5.6 Luna]({% post_url 2026-08-09-solving-htb-challenges-with-openai-gpt-5.6-luna %}), whose median cost was $0.0181. As a side note, Flash was under a temporary 50% launch discount at the time of my test, so this should not be read as the permanent list-price ratio. But even at 100% of its price, it would still be very competitive.


At the moment, **GLM 5.3 Flash** has replaced **GPT-5.6 Luna** as my go-to model, not just for cybersecurity work. It was less step-efficient than Sol, but no other included model in this benchmark achieved both a higher score and a lower median cost.

## GLM 5.3 Flash is not a smaller GLM 5.3

One final note on this model's name. **GLM 5.3 Flash** may sound like a smaller version of [GLM 5.3]({% post_url 2026-08-19-evaluating-z-ai-glm-5.3-on-hack-the-box-challenges %}), but the two models have different origins. According to its [official model card](https://huggingface.co/zai-org/GLM-5.3-Flash), Flash is a 320B-total, 18B-active model trained from a new 30T-token multimodal base, with a new architecture combining sparse and linear attention. By contrast, [Z.ai says GLM 5.3](https://z.ai/blog/glm-5.3) reuses the GLM 5.2 base and derives all its improvements from additional post-training. The published [GLM 5.2 artifact](https://huggingface.co/zai-org/GLM-5.2) - the base reused by GLM 5.3 - is listed at 753B parameters. They are therefore separate branches of the GLM family, not full-size and compressed versions of the same model.

I tested **GLM 5.3** just a few days earlier, and it performed much worse in this benchmark: it scored 47.2% and solved 10 challenges, compared with Flash's 81.0% and 15 solves. Its measured median cost was also $0.4915, compared with Flash's $0.0140, so I'm not sure why Z.ai decided to use its brand for the new model. **GLM 5.4 Flash** would have made much more sense to me.


---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/z-ai-glm-5.3-flash-20260826-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/z-ai-glm-5.3-flash-20260826-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/z-ai-glm-5.3-flash-20260826-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 15
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr>:** 1
- **Benchmark score:** 81.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 24.5 | 507 |
| Model cost | $0.01 | $0.39 |
| Duration | 00:10:52 | 04:50:09 |
| Number of input tokens | 0.45M | 12.73M |
| Number of output tokens | 0.02M | 0.50M |
| Number of `read_file` tool calls | 1.0 | 29 |
| Number of `write_file` tool calls | 2.5 | 80 |
| Number of `execute_command` tool calls | 22.0 | 481 |
| Number of `web_search` tool calls | 0.0 | 1 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 3 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended because the model appeared to be caught in a never-ending loop.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 1 |
| Benchmark score | 94.1% | 93.2% | 89.8% | 64.9% |
| **Median per challenge** | | | | |
| Model steps | 17.5 | 24 | 30 | 25 |
| Model cost | $0.01 | $0.01 | $0.03 | $0.03 |
| Duration | 00:06:07 | 00:10:52 | 00:18:19 | 00:25:38 |
| Number of input tokens | 0.32M | 0.21M | 0.86M | 0.68M |
| Number of output tokens | 0.01M | 0.01M | 0.04M | 0.03M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 1.0 | 2.0 |
| Number of `write_file` tool calls | 1.0 | 3.0 | 3.0 | 2.5 |
| Number of `execute_command` tool calls | 19.5 | 20.0 | 29.5 | 27.0 |
| Number of `web_search` tool calls | 0.0 | 0.0 | 0.0 | 0.0 |
