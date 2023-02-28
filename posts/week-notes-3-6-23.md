---
title: week-notes-3-6-23
author: Shana
keywords: [no, nothing]
date: 2023-02-28
draft: true
---

Week notes! Week notes!

It's my birthday this week and I'm also in India for a wedding!

--- edit the below

## Projects

I've been in a personal-projects slump recently, as evidenced by my GitHub activity chart, yikes.

![A mediocre GitHub contributions graph](../images/github-dots.png)

This is mostly because of some health stuff that came up early in January and I'm still dealing with. However, I've been doing better over the last couple of weeks and I've found some energy and excitement to start playing around, particularly with ChatGPT-related things.

### This website

Read my [writeup on adding a new feature to this site](https://shana.codes/posts/chatgpt-site-improvements.html) with the "help" of ChatGPT.

### ClippyGPT

I read [this super cool article](https://supabase.com/blog/chatgpt-supabase-docs) this week about Supabase adding ChatGPT to answer questions based off their docs.

They created such a nice writeup and video of the process, I wanted to play around with a similar setup in [Sentry's docs](https://docs.sentry.io/).

I didn't get very far because our docs our on a very old version of Gatsby (2.32.13, yikes), which is not compatible with Supabase. I figured rather than trying my luck with other postgres DBs that might support both [`pgvector`](https://github.com/pgvector/pgvector) and Gatsby v2, I'd just set up a proof of concept by copying our docs markdown files into a newer project and set up Supabase with that project.

I decided to try [Markdoc](https://markdoc.dev/), since I've been wanting to play with it more since my first experiments with it at Coinbase. However, we use .mdx files, Mardoc only supports it's own flavor of markdown... whew. It quickly turned into a lot, as these things often do.

This is still a work in progress. Hopefully more updates next week!

## Writing

- [started] "What is OpenTelemetry" article with another DevRel person from GCP.
- [paused] Dreaming of finishing my Profiling 101 series (someday 💭)

## Reading

Articles I liked this week:

- [Regex crossword](https://regexcrossword.com/), not an article, but you'll like it. I've been really into crosswords lately, but I super suck at crosswords. Cultural references from the 80s just aren't my thing. This is better.

Books:

- [started] [My Grandmother's Hands](https://openlibrary.org/works/OL19718843W/My_grandmother%27s_hands?edition=ia%3Amygrandmothersha0000mena)
- [started] [By Blood](https://openlibrary.org/works/OL16239773W/By_blood?edition=ia%3Abyblood0000ullm_u3v1)
- [in-progress] [Moby Dick](https://openlibrary.org/works/OL21501229W/Moby_Dick?edition=ia%3Amobydick0000melv_c9t5)
- [in-progress], [reread] [Return of the King](https://openlibrary.org/works/OL27516W/The_Return_of_the_King?edition=ia%3Aleretourduroi0000tolk)
- [paused] [Spare](https://openlibrary.org/works/OL29240850W/Spare)
- [paused] [Unsettled Ground](https://openlibrary.org/works/OL25758323W/Unsettled_Ground)
- [finished] [Legends & Lattes](https://openlibrary.org/works/OL27591348W). Wow, this was so cute. a really cozy, easy read, which is just what I needed. ⭐️⭐️⭐️⭐️⭐️
- [finished] [Tales from the Hinterland](https://openlibrary.org/works/OL20868276W/Tales_from_the_Hinterland?edition=key%3A/books/OL38807224M). A companion book to a series I've liked recently ([The Hazel Wood](https://openlibrary.org/works/OL19730066W/The_Hazel_Wood?edition=key%3A/books/OL26943167M)). Creepy short stories, took me a while to get through. ⭐️⭐️⭐️
