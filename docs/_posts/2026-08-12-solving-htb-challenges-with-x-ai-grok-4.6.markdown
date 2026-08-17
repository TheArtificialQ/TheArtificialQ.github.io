---
layout: post
title:  "Solving Hack The Box Challenges with Grok 4.6"
date:   2026-08-12 20:05:34 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

When I tested an older version of Grok [this spring]({% post_url 2026-04-14-agentic-ai-pentesting-with-strix-results-from-18-llm-models %}), my only comment was blunt: "grok-4.20 was useless." So when Grok 4.5 was released a month ago and started receiving very positive reviews, I was quite surprised.

Today, Grok 4.6 was released and I've finally had a chance to test it against HTB challenges, and the team behind it deserves an apology. I'm not sure what the folks at xAI did, but the performance increase over the older version is jaw-dropping.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the {% include htb-challenger-benchmark-term.html %}.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

During my testing, I watched this model crack one HTB challenge after another in a steady, confident way, and the final boss fight against the last two challenges was exhilarating, even though it was ultimately unsuccessful. In the end, with a 76.1% score, it's the undisputed new king of my leaderboard - not only because of its results, but also because of its speed (it had the fewest steps per challenge of all the models I've tested so far) and cost. Look at the **Cost vs. Benchmark Score** graph on the {% include htb-challenger-benchmark-term.html %} page to see what I mean.

So let's forget that useless old version. For me, **Grok 4.6** is currently the best model I've tested on offensive-security challenges.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/x-ai-grok-4.6-20260810-model-card.svg" | relative_url }})

## Cost vs. Benchmark Score

The highlighted point is this model. Models closer to the upper-left achieve a higher benchmark score at a lower median cost per challenge.

<object data="{{ "/assets/images/x-ai-grok-4.6-20260810-cost-vs-benchmark-score.svg" | relative_url }}" type="image/svg+xml" width="800" height="550" aria-label="Interactive Cost vs. Benchmark Score chart with this model highlighted">
  <img src="{{ "/assets/images/x-ai-grok-4.6-20260810-cost-vs-benchmark-score.svg" | relative_url }}" alt="Cost vs. Benchmark Score with this model highlighted" width="800" height="550">
</object>

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 14
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 76.1%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 14 | 452 |
| Model cost | $0.23 | $17.31 |
| Duration | 00:03:38 | 02:45:35 |
| Number of input tokens | 0.23M | 20.29M |
| Number of output tokens | 0.01M | 0.47M |
| Number of `read_file` tool calls | 1.0 | 41 |
| Number of `write_file` tool calls | 0.0 | 35 |
| Number of `execute_command` tool calls | 10.0 | 403 |
| Number of `web_search` tool calls | 0.0 | 15 |

## Results by challenge difficulty

All resource-usage metrics are medians per challenge.

| Metric | Very Easy | Easy | Medium | Hard |
| --- | ---: | ---: | ---: | ---: |
| **Results** | | | | |
| Number of challenges | 4 | 4 | 4 | 4 |
| <abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr> | 4 | 4 | 4 | 2 |
| <abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr> | 0 | 0 | 0 | 0 |
| <abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr> | 0 | 0 | 0 | 2 |
| <abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr> | 0 | 0 | 0 | 0 |
| Benchmark score | 97.5% | 98.4% | 93.6% | 46.6% |
| **Median per challenge** | | | | |
| Model steps | 11.5 | 11.5 | 19 | 63.5 |
| Model cost | $0.10 | $0.14 | $0.58 | $2.89 |
| Duration | 00:01:26 | 00:03:00 | 00:09:39 | 00:24:56 |
| Number of input tokens | 0.10M | 0.12M | 0.61M | 3.50M |
| Number of output tokens | 0.00M | 0.01M | 0.02M | 0.08M |
| Number of `read_file` tool calls | 0.5 | 1.0 | 0.0 | 4.5 |
| Number of `write_file` tool calls | 0.0 | 2.0 | 0.5 | 1.0 |
| Number of `execute_command` tool calls | 9.0 | 8.0 | 16.5 | 55.0 |
| Number of `web_search` tool calls | 0.5 | 0.5 | 0.0 | 1.0 |
