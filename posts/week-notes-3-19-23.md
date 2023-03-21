---
title: week-notes-3-19-23
author: Shana
keywords: [no, nothing]
date: 2023-03-19
draft: true
---

I'm back from India! The trip went surprisingly well health-wise. I did take 7 (yes, SEVEN) different medications for my allergies/MCAS, but I didn't have any major issues and didn't get sick, so overall, huge win.

## Work updates

## Projects



### This website

Read my [writeup on adding a new feature to this site](https://shana.codes/posts/chatgpt-site-improvements.html) with the "help" of ChatGPT.

### ClippyGPT

I read [this super cool article](https://supabase.com/blog/chatgpt-supabase-docs) this week about Supabase adding ChatGPT to answer questions based off their docs.

They created such a nice writeup and video of the process, I wanted to play around with a similar setup in [Sentry's docs](https://docs.sentry.io/).

I didn't get very far because our docs our on a very old version of Gatsby (2.32.13, yikes), which is not compatible with Supabase. I figured rather than trying my luck with other postgres DBs that might support both [`pgvector`](https://github.com/pgvector/pgvector) and Gatsby v2, I'd just set up a proof of concept by copying our docs markdown files into a newer project and set up Supabase with that project.

I decided to try [Markdoc](https://markdoc.dev/), since I've been wanting to play with it more since my first experiments with it at Coinbase. However, we use .mdx files, Mardoc only supports it's own flavor of markdown... whew. It quickly turned into a lot, as these things often do.

This is still a work in progress. Hopefully more updates next week!

## Writing

- [in-progress] "What is OpenTelemetry" article with another DevRel person from GCP.
- [paused] Dreaming of finishing my Profiling 101 series (someday 💭)

## Reading

### Articles I liked this week

- [Automatic Machine Knitting of 3D Meshes](https://textiles-lab.github.io/publications/2018-autoknit/). Highly relevant to my interests. Is there code I can run? I haven't dug in enough to find it yet.

### Books

- [in-progress] [Never Bet Against Occam](https://openlibrary.org/works/OL20811242W/Never_Bet_Against_Occam). Reading this to learn more about mastocytosis :/
- [in-progress] [My Grandmother's Hands](https://openlibrary.org/works/OL19718843W/My_grandmother%27s_hands?edition=ia%3Amygrandmothersha0000mena)
- [paused] [Moby Dick](https://openlibrary.org/works/OL21501229W/Moby_Dick?edition=ia%3Amobydick0000melv_c9t5). Reading as [Whale Weekly](https://whaleweekly.substack.com/about) Sad to pause it, but I'm way behind on my Substacks.
- [paused] [Spare](https://openlibrary.org/works/OL29240850W/Spare)
- [paused] [Unsettled Ground](https://openlibrary.org/works/OL25758323W/Unsettled_Ground)
- [finished] [Modern Technical Writing](https://openlibrary.org/works/OL27309148W/Modern_Technical_Writing). Very short and practical. An easy read to start to feel prepared for a role on a docs team. ⭐️⭐️⭐️⭐️⭐️

