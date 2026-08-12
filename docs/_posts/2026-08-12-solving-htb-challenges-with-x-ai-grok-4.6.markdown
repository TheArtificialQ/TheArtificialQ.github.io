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
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

During my testing, I watched this model crack one HTB challenge after another in a steady, confident way, and the final boss fight against the last two challenges was exhilarating, even though it was ultimately unsuccessful. In the end, with a 80% score, it's the undisputed new king of my leaderboard - not only because of its results, but also because of its speed (it had the fewest steps per challenge of all the models I've tested so far) and cost. Look at the **Cost vs. Benchmark Score** graph on the [HTB-Challenger Benchmark]({{ "/htb-challenger-benchmark" | relative_url }}) page to see what I mean.

So let's forget that useless old version. For me, **Grok 4.6** is currently the best model I've tested on offensive-security challenges.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/x-ai-grok-4.6-20260810-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 14
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 80.0%

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

### Very Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 11.5 | 50 |
| Model cost | $0.10 | $0.96 |
| Duration | 00:01:26 | 00:09:26 |
| Number of input tokens | 0.10M | 1.05M |
| Number of output tokens | 0.00M | 0.03M |
| Number of `read_file` tool calls | 0.5 | 8 |
| Number of `write_file` tool calls | 0.0 | 1 |
| Number of `execute_command` tool calls | 9.0 | 42 |
| Number of `web_search` tool calls | 0.5 | 4 |

### Easy challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 11.5 | 43 |
| Model cost | $0.14 | $0.58 |
| Duration | 00:03:00 | 00:12:29 |
| Number of input tokens | 0.12M | 0.51M |
| Number of output tokens | 0.01M | 0.03M |
| Number of `read_file` tool calls | 1.0 | 4 |
| Number of `write_file` tool calls | 2.0 | 8 |
| Number of `execute_command` tool calls | 8.0 | 30 |
| Number of `web_search` tool calls | 0.5 | 3 |

### Medium challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 4
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 0
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 100.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 19 | 106 |
| Model cost | $0.58 | $3.98 |
| Duration | 00:09:39 | 00:45:15 |
| Number of input tokens | 0.61M | 4.50M |
| Number of output tokens | 0.02M | 0.11M |
| Number of `read_file` tool calls | 0.0 | 4 |
| Number of `write_file` tool calls | 0.5 | 6 |
| Number of `execute_command` tool calls | 16.5 | 102 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Hard challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 2
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 2
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 50.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 63.5 | 253 |
| Model cost | $2.89 | $11.79 |
| Duration | 00:24:56 | 01:38:25 |
| Number of input tokens | 3.50M | 14.23M |
| Number of output tokens | 0.08M | 0.31M |
| Number of `read_file` tool calls | 4.5 | 25 |
| Number of `write_file` tool calls | 1.0 | 20 |
| Number of `execute_command` tool calls | 55.0 | 229 |
| Number of `web_search` tool calls | 1.0 | 8 |
