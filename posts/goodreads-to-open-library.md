---
title: Switching from Goodreads to Open Library
author: Shana
keywords: [no, nothing]
date: 2021-08-18
---

Sometime during the last year (what even is pandemic time) I was exploring D3.js for kicks. One of the projects I created was a "virtual bookshelf" that would pull the books I was currently reading or just finished from the Goodreads API and display them. My hope was to create something pretty (judge for yourself 🥲) that I could download regularly and use as a Zoom background.

The project was a lot of fun ([check out the code](https://observablehq.com/@shanamatthews/spine-generator-v2) if you're curious) and was going pretty well. D3 was a lot of fun for someone who knew absolutely nothing about SVG and Canvas and not a ton about HTML and Javascript. 

<iframe width="100%" height="496" frameborder="0"
  src="https://observablehq.com/embed/@shanamatthews/spine-generator-v2?cells=books%2Cviewof+NUMBOOKS%2Cviewof+FONT"></iframe>

###### I might have missed the mark on "pretty".

However, after taking a break from the project for a few weeks when life got busy, I came back to a totally broken project. Maybe not that surprising, it wasn't exactly robust code... But once I dug in, I realized that my calls to the Goodreads API weren't working anymore. My API key had expired during my time away from the project... weird. I'm not sure how quickly API keys normally expire, but no big deal, I'll just grab a new one! 

No dice. Goodreads had decided to stop issuing new developer keys (and shut off any that hadn't been active in a few weeks) without any warning. I already wasn't a huge fan of Goodreads, since they're owned by Amazon, but this was the last straw for me. I was done with Goodreads. Next step - find a new place to log my book reading habit, preferably with functional APIs where I could grab that data.

My search for the perfect book catalogue with APIs didn't get me very far. There aren't very many sites that let you log your books and TBR (to be read, for you non-book nerds) list and retrieve them via an API. [LibraryThing](https://www.librarything.com/) seemed like a good option, but their APIs weren't going to do quite what I wanted. At this point, they've disabled [their APIs](https://www.librarything.com/services/rest/documentation/1.1/) as well (what is going on in the book API world??!?).

I ultimately landed on [Open Library](https://openlibrary.org/) as my book log provider of choice. While Open Library's API doesn't currently allow you to retrieve books that you've logged, Open Library is open source! And not only is it "open source" but it actually has a great community of contributors and helpful, friendly staff. In my first couple days of exploring I was already able to PR a small feature request to the project ☺️

I was able to import all my Goodreads data into Open Library and I'm hopeful that me or another contributor can eventually add the functionality I need to their APIs so that my book backgrounds project can live on!

#### Update!!

Open Library totally *does* support doing what I want with [their REST API](https://openlibrary.org/developers/api). It's not explicitly documented, but you can easily grab your reading lists as json, e.g. <https://openlibrary.org/people/stinkerelly/books/currently-reading>.

More coming soon as I rework my "spine generator" (AGAIN) using the Open Library REST API 🥳
