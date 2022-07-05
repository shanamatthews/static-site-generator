---
title: Workout Tracker
author: Shana
keywords: [no, nothing]
date: 2022-07-05
---

I really enjoy working out, especially lifting weights and following a set program. One program I'd been trying for a while is called [Strong Curves](https://www.bretcontreras.store/products/strong-curves) (cheesy, I know... they all have crap names). The program is highly structured, with each day following the same format, alternating between different exercises that all fit into certain categories.

I'd been wanting to write my own workout tracker for a while and the format of this program lends itself well to writing a templated workout tracker.

During my experiments with creating a "Zoom bookshelf" with D3, I found that I really enjoyed writing Javascript in [Observable](https://observablehq.com/). Observable makes Javascript feel a lot more sane to my strictly-typed brain and basically creates UX for you, as long as you were okay with the default components provided.

I'm always okay with default UX if it means I don't have to write it, so I went ahead and created my own [project on Observable](https://observablehq.com/collection/@shanamatthews/strong-curves-tracker). 

Right now this project is set up to store workout data in JSON and save as a GitHub Gist on my own account. I've actually embedded a GitHub key (with only Gist permissions!!) in the project, which is a VERY BAD IDEA™️ , please don't do this at home.

It's been super convenient for my development, but it means if you want to use this project for yourself, you'll need to:

- Have a GitHub account
- Create a Gist named "A" (please don't judge the process) with 3 files in it named "A", "B", and "C" (to correspond to workout days A, B, C)
- [Create a GitHub personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with Gist write access
- Replace my Gist url (`gistUrl`) and GitHub token (`ghToken`) with your own. These variables can be found in the [Tracker Scripts notebook](https://observablehq.com/@shanamatthews/strong-curves-tracker-scripts?collection=@shanamatthews/strong-curves-tracker)

I've since ported (most) of this workout tracker to Svelte in my quest to be able to suck less at frontend development 😇 But that's a story for a different post.

Happy coding and go hit the gym!

