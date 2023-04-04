---
title: week-notes-4-3-23
author: Shana
keywords: [no, nothing]
date: 2023-04-03
draft: false
---

## Producing

### Work

Today was my first day as a "Documentation Engineer" at Sentry! I'm currently working on wrapping my head around our very old Gatsby docs site that we host on Vercel and familiarizing myself with the (long) list of complaints about it.

My very first project on the team was to implement a PR template for the repo with "pre-merge checklist" to try to convince employees to get a review from our technical writers before merging their docs PRs. The team is hesitant to gate PRs on our review more formally, but I think we're going to need to. ~60% of employees are just deleting the checklist when they create the PR :/

### Life

I perform with the [Seattle Labor Chorus](https://seattlelaborchorus.org/) and we had our annual concert this weekend on April 1st! It was a blast, and I got to sing a duet with a fellow chorus member, performing Joe Jencks' [Rise As One](https://www.youtube.com/watch?v=A69eP-kiARk&ab_channel=JoeJencks-Topic). YouTube link to some shortly (if I remember).

### Experiments

#### This website

My posts folder is getting really messy, so I was trying to edit the bash script so it could accept nested post folders. I spent longer than 30 min on it without success, which I think means its time to move on to rewriting this thing in a more sane language, like Go... I also recently noticed that [Brandur's blog](https://brandur.org/) is created with [his own SSG written in Go](https://github.com/brandur/sorg)... More to come soon?

## Consuming

### Nature

I live about 5 minutes away from a local park with a pond which I rarely go to, which is such a waste. There are a lot of things I don't love about my house, but one of them was how much it feels like it's in nature, despite being very much in town.

Inspired by the Huberman Lab podcast, I've been trying to take short morning walks to that pond and just sit and absorb morning sunlight for a while. It turns out, I love it! Who would have guessed. Here is a suspiciously friendly duck that was probably looking for some food:

![A very friendly duck](../images/pond.jpg)

### Articles I liked this week

- [The influence of language-generative AI tools on tech comm](https://idratherbewriting.com/trends/trends-to-follow-or-forget-language-generative-ai.html). This one made me think. There have been so many terrible ChatGPT takes recently and I've been feeling sick of reading about it, but this one was short and reasonable. I'm extremely interested in what we'll be able to do with automatically generating documentation directly from source code. Or even using AI to generate OpenAPI specs from source. Basically how to build a pipeline from code -> docs using AI tools.
- [GPT-4 and professional benchmarks](https://aisnakeoil.substack.com/p/gpt-4-and-professional-benchmarks). This was an "AI pessimist" take. Here's a very very (very) INTERESTING quote:

    > To benchmark GPT-4’s coding ability, OpenAI evaluated it on problems from Codeforces, a website that hosts coding competitions. Surprisingly, Horace He pointed out that GPT-4 solved 10/10 pre-2021 problems and 0/10 recent problems in the easy category. The training data cutoff for GPT-4 is September 2021. This strongly suggests that the model is able to memorize solutions from its training set — or at least partly memorize them, enough that it can fill in what it can’t recall.
    >
    > As further evidence for this hypothesis, we tested it on Codeforces problems from different times in 2021. We found that it could regularly solve problems in the easy category before September 5, but none of the problems after September 12.
    >
    > In fact, we can definitively show that it has memorized problems in its training set: when prompted with the title of a Codeforces problem, GPT-4 includes a link to the exact contest where the problem appears (and the round number is almost correct: it is off by one). Note that GPT-4 cannot access the Internet, so memorization is the only explanation.

### Books

Wow, not a lot of progress on the books front. Life has been happening!

- [in-progress] [Never Bet Against Occam](https://openlibrary.org/works/OL20811242W/Never_Bet_Against_Occam). Reading this to learn more about mastocytosis :(
- [in-progress] [My Grandmother's Hands](https://openlibrary.org/works/OL19718843W/My_grandmother%27s_hands?edition=ia%3Amygrandmothersha0000mena)
- [paused] [Spare](https://openlibrary.org/works/OL29240850W/Spare)
- [paused] [Unsettled Ground](https://openlibrary.org/works/OL25758323W/Unsettled_Ground)
