---
layout: post
title:  "Solving Hack The Box Challenges with Grok 4.5"
date:   2026-08-12 15:11:26 +0000
image:  /assets/images/htb-challenger-benchmark-logo-social.png
author: TheArtificialQ
hn_id:  
---

When I tested an older version of Grok [this spring]({% post_url 2026-04-14-agentic-ai-pentesting-with-strix-results-from-18-llm-models %}), my only comment was blunt: "grok-4.20 was useless." So when **Grok 4.5** was released a month ago and started receiving very positive reviews, I was quite surprised.

Now I've finally had a chance to test it against HTB challenges, and the team behind it deserves an apology. I'm not sure what the folks at xAI did, but the performance increase over the older version is jaw-dropping.

<!--more-->

---

> ![HTB-Challenger Benchmark]({{ "/assets/images/htb-challenger-benchmark-logo-full.png" | relative_url }}){: width="300px" }
>
> This blog post is part of a series of tests for the HTB-Challenger Benchmark.
> See the [benchmark results page]({{ "/htb-challenger-benchmark" | relative_url }}) for all results and the [benchmark methodology]({{ "/htb-challenger-benchmark-methodology" | relative_url }}) to learn how the benchmark is calculated.

---

During my testing, I watched this model crack one HTB challenge after another in a steady, confident way, and the final boss fight against the last challenge was exhilarating, even though it was ultimately unsuccessful. In the end, with a 90% score, it's the undisputed new king of my leaderboard - not only because of its results, but also because of its speed (it had the fewest steps per challenge of all the models I've tested so far) and cost. Look at the **Cost vs. Benchmark Score** graph on the [HTB-Challenger Benchmark]({{ "/htb-challenger-benchmark" | relative_url }}) page to see what I mean.

So let's forget that useless old version. For me, **Grok 4.5** is currently the best model I've tested on offensive-security challenges.

---

![HTB-Challenger Benchmark LLM model card]({{ "/assets/images/x-ai-grok-4.5-20260708-model-card.svg" | relative_url }})

## Overall benchmark results

- **Number of challenges:** 16
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 15
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 90.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 13.5 | 431 |
| Model cost | $0.25 | $12.83 |
| Duration | 00:05:48 | 03:10:27 |
| Number of input tokens | 0.28M | 19.04M |
| Number of output tokens | 0.01M | 0.45M |
| Number of `read_file` tool calls | 0.0 | 16 |
| Number of `write_file` tool calls | 0.0 | 6 |
| Number of `execute_command` tool calls | 13.5 | 407 |
| Number of `web_search` tool calls | 0.0 | 11 |

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
| Model steps | 9.5 | 60 |
| Model cost | $0.09 | $0.83 |
| Duration | 00:01:34 | 00:11:32 |
| Number of input tokens | 0.08M | 1.30M |
| Number of output tokens | 0.00M | 0.03M |
| Number of `read_file` tool calls | 0.5 | 6 |
| Number of `write_file` tool calls | 0.0 | 1 |
| Number of `execute_command` tool calls | 7.5 | 53 |
| Number of `web_search` tool calls | 0.0 | 2 |

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
| Model steps | 13 | 48 |
| Model cost | $0.17 | $0.63 |
| Duration | 00:04:28 | 00:16:56 |
| Number of input tokens | 0.21M | 0.70M |
| Number of output tokens | 0.01M | 0.03M |
| Number of `read_file` tool calls | 1.0 | 6 |
| Number of `write_file` tool calls | 0.0 | 1 |
| Number of `execute_command` tool calls | 11.0 | 45 |
| Number of `web_search` tool calls | 1.5 | 7 |

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
| Model steps | 16 | 104 |
| Model cost | $0.34 | $3.29 |
| Duration | 00:06:41 | 00:35:59 |
| Number of input tokens | 0.43M | 4.89M |
| Number of output tokens | 0.01M | 0.09M |
| Number of `read_file` tool calls | 0.0 | 1 |
| Number of `write_file` tool calls | 0.0 | 1 |
| Number of `execute_command` tool calls | 14.5 | 99 |
| Number of `web_search` tool calls | 0.0 | 0 |

### Hard challenges

- **Number of challenges:** 4
- **<abbr title="Runs where the submitted flag matched the expected flag.">Number of solved challenges</abbr>:** 3
- **<abbr title="Runs where the submitted flag did not match the expected flag.">Number of false positives</abbr>:** 0
- **<abbr title="Runs in which the model decided not to continue and gave up.">Runs where the model gave up</abbr>:** 0
- **<abbr title="Runs that ended after reaching the maximum number of steps or the maximum total cost.">Runs that reached the step or cost limit</abbr>:** 1
- **<abbr title="Runs that ended after the model response exceeded the maximal length twice in a row.">Runs where the model got stuck</abbr>:** 0
- **Benchmark score:** 75.0%

| Metric | Per challenge (median) | Total |
| --- | ---: | ---: |
| Model steps | 49 | 219 |
| Model cost | $1.54 | $8.08 |
| Duration | 00:24:02 | 02:05:59 |
| Number of input tokens | 2.69M | 12.14M |
| Number of output tokens | 0.04M | 0.30M |
| Number of `read_file` tool calls | 0.0 | 3 |
| Number of `write_file` tool calls | 0.5 | 3 |
| Number of `execute_command` tool calls | 47.5 | 210 |
| Number of `web_search` tool calls | 0.5 | 2 |
