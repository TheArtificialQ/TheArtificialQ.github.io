---
layout: post
title:  "How not to test LLM models"
date:   2026-03-09 00:00:00 +0100
image:  /assets/images/social-preview.png
author: TheArtificialQ
hn_id:  47314569
---

In the Czech Republic, we have a whole lore built around a fictitious character called [Jára Cimrman](https://en.wikipedia.org/wiki/J%C3%A1ra_Cimrman). He was partially a genius (one of the greatest playwrights, composers, teachers, travellers, inventors, detectives, gynecologists and sportsmen, among many other things) but mostly a loser ("... while running away from one furious tribe, he missed the North Pole by just seven meters, thus almost becoming the first human to reach the North Pole.") One of his strongest skills was finding dead ends. He found many ways in which things should NOT be done and helped humanity many times by being able to authoritatively say: "This isn’t the way to do it, my friends!"

After spending several days trying to compare the performance of different LLM models, I'm sure Jára would be very proud of me.

<!--more-->

## Problem with old stuff

It started with a simple thought. For the last few weeks, I've been playing with an autonomous AI penetration testing tool called [strix](https://github.com/usestrix/strix) and I wanted to find out how its results change when I use it with different LLM models, from small (and free) ones to top-tier (and top-pricey) ones. To be able to compare the results, I decided to test it against retired Hack The Box machines.

It started well, the results made sense, I got data, I created [benchmarks]({{ '/ai-offsec-benchmarks.html' | relative_url }}).

And then I spotted Claude Sonnet 4.6 doing this:

![Claude Sonnet 4.6]({{ "/assets/images/2026-03-09-claude.png" | relative_url }})

In short, at the very start of the test, after running `nmap`, it found out that it was running against a machine it had seen during its training, and instead of finding an attack path, it simply created a plan from the attack path it had been trained on. My benchmarks could be thrown out.

## Problem with new stuff

I had half-expected this, so when this happened, I quickly decided to change my approach and run my tests against HTB machines and challenges that were published recently, after all these LLM models were released. 

I got new results, even better than the previous ones, I started preparing new benchmarks.

And then I spotted GPT 5.3 Codex doing this:

![GPT 5.3 Codex]({{ "/assets/images/2026-03-09-gpt.png" | relative_url }})

After it ran for an hour and hadn't found anything, that bastard decided to cheat on me and started searching online for writeups!

## Conclusion

The conclusion is simple - if you want to get the true performance of LLM models - one that isn't skewed by their training experience or their ability to search online for shortcuts - you need to build your own targets.

Because testing it against anything that is publicly available and has writeups online - this isn’t the way to do it, my friends!