---
title: chatgpt-site-improvements
author: Shana
keywords: [no, nothing]
date: 2023-02-27
---

I'm really proud of myself for creating this site with my own static site generator [written with just Bash scripts](./static-site-generator-with-bash.html). I think it's sick and it aligns with my stance on not needing a framework or even a "real" programming language to do every single thing.

However the reality is... I'm not so great at Bash scripting. I don't use Bash regularly at work, or even in personal projects, so whenever I want to go in to make tweaks to this site, I always feel super rusty and it takes ages to remember how this simple project works.

I'd been wanting to add a tiny new "features" allowing me to have draft posts in the site without publishing them (aka generating an html page for them), but had been putting it off because I knew I'd have to wrap my brain around my messy Bash scripts again.

That's where ChatGPT comes in! I'd read some really promising things about folks using ChatGPT to help them with simple scripting and I figured my build script for this site was simple enough that ChatGPT might be able to help add this draft posts feature.

⚠️ Spoiler alert: It was not.

## The challenge

I first tested out ChatGPT by feeding it my [`build` script](https://github.com/shanamatthews/static-site-generator/blob/main/build) and asking what it did. It was very accurate! Impressive!

>This script is used to build a static website. Here's a step-by-step explanation of what it does:
>
>The first line (#!/usr/bin/env bash) specifies that the script should be run using the bash shell.
>
>The second line (shopt -s globstar) enables the globstar option, which allows the use of double asterisks (**) as a recursive directory wildcard.
>
>The script declares an array called unsorted_posts to hold the file names of all the Markdown files in the posts directory (excluding the index.md file) sorted by date in descending order.
>
>The for loop iterates over each file in the posts directory (excluding the index.md file), extracts the date from the front matter of each file using sed, and constructs a new file name by prefixing the date to the original file name. This new file name is then added to the unsorted_posts array.
>
>The script declares another array called sorted_posts and sets its value to the sorted version of unsorted_posts.
>
>The script declares another array called latest_posts and fills it with a list of variables to be passed to the pandoc command when building the posts/index.md page.
>
>The script extracts the latest post from sorted_posts and generates the HTML code for the latest post preview using pandoc.
>
>The script iterates over each Markdown file in the current directory and its subdirectories. For each file, it extracts the file name and directory, determines whether it is the homepage, posts page, or a regular page, and generates the corresponding HTML code using pandoc. The assets-folder variable is set to assets for pages in the current directory, and ../assets for pages in subdirectories.
>
>The generated HTML files are stored in the same directories as their corresponding Markdown files.
>
>Overall, this script generates a static website from Markdown files by converting them to HTML using pandoc and a custom HTML template. The homepage and posts page are generated separately from the other pages, and the latest post preview is included on the posts page.

Feeling confident about ChatGPT's abilities, I asked it how I could edit the script such that if a post has `draft: true` in the frontmatter, the script won't generate an html page for it.

Here was it's response:

>```bash
>#!/usr/bin/env bash
>
>shopt -s globstar
>
>declare -a unsorted_posts
>for post in $(ls -t posts/*.md); do
>  if [[ $post != "posts/index.md" ]]; then
>    # Check for 'draft: true' in front matter
>    if grep -q 'draft: true' "$post"; then
>      continue
>    fi
>
>    post_date=$(sed -n 's/^date: //p' ${post})
>    post_name=$(basename $post)
>    post_name="${post_date}_${post_name}"
>    unsorted_posts+=(${post_name})
>  fi
>done
>
>...
> <unmodified code>
>```

At first glance, this looked kinda right! I didn't like that it wasn't actually checking the frontmatter, as instructed. By using `grep` in this way, the script would skip the file if "draft: true" appeared anywhere in the post, not just in the frontmatter. It's not likely that I'd write that phrase *outside* of the frontmatter, but I'd rather not run into that weird and confusing bug later.

I was pretty optimistic at this point. I fiddled with ChatGPT a little more until I got it to output a version that checked the frontmatter specifically, and also grabbed the date from the frontmatter specifically. This was definitely an improvement!

>```bash
>#!/usr/bin/env bash
>
>shopt -s globstar
>
>declare -a unsorted_posts
>for post in $(ls -t posts/*.md); do
>  if [[ $post != "posts/index.md" ]]; then
>    # Extract the front matter and check if it contains "draft: true"
>    front_matter=$(sed -n '/^---$/,/^---$/p' "${post}")
>    if [[ ${front_matter} == *"draft: true"* ]]; then
>       continue
>    fi
>
>    # Extract the post date and name
>    post_date=$(echo "${front_matter}" | sed -n 's/^date: //p')
>    post_name=$(basename $post)
>    post_name="${post_date}_${post_name}"
>    unsorted_posts+=(${post_name})
>  fi
>done
>
>...
> <unmodified code>
>```

## The letdown

However, upon testing out the script, I realized that ChatGPT was actually pretty wrong. The first for loop in the script where ChatGPT made changes is actually only used to create an array of posts to be sorted by date, which is used to create the the latest post preview on the homepage.

ChatGPT seemed to "know" this in its description of what the script does. Remember this paragraph?

> The script iterates over each Markdown file in the current directory and its subdirectories. For each file, it extracts the file name and directory, determines whether it is the homepage, posts page, or a regular page, and generates the corresponding HTML code using pandoc. The assets-folder variable is set to assets for pages in the current directory, and ../assets for pages in subdirectories.

But when it came to editing the script, ChatGPT seemed to forget and fixate only on the first for loop. Excluding drafts from the first for loop meant that draft posts wouldn't be candidates for being the preview post on the homepage and wouldn't be added to the my list of posts on the [posts index page](https://shana.codes/posts/) (yay, good) but they were still **built into html pages and published** (boo, bad).

This mistake feels odd, because I specifically asked that we **don't generate an html file for draft posts**, but I didn't mention anything about listing draft posts on the posts index page.

As a person who writes code, I'm used to feeling like computers are [maliciously compliant](https://en.wikipedia.org/wiki/Malicious_compliance). The code I write does exactly what I wrote it to do, regardless of what I actually wanted. Here, it felt like ChatGPT understood what I *wanted*, but didn't do what I told it to do.

Ok, no more anthropomorphizing ChatGPT. It's just a [dumb LLM probabilistically spitting out words at me](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/).

I came away from this feeling disappointed and like my Bash script needed a little refactoring to be easier for future me and for LLMs to understand.

Did I do that? No 😂 However, I **did** [add the drafts post feature](https://github.com/shanamatthews/static-site-generator/commit/c7a1b9b4840b24448db21cad44a452059e09e435) by keeping the code to skip posts in the first for loop and building posts within that first for loop instead of the second.

## Small redemption

After my failure using ChatGPT for this, I still wanted to try getting ChatGPT to do something useful. I ended up having it edit my [`build` script](https://github.com/shanamatthews/static-site-generator/blob/main/build) and my [`create-post` script](https://github.com/shanamatthews/static-site-generator/blob/main/create-post) to print out error messages when something goes wrong. I'd been too lazy to do this and ChatGPT did a good job on this super simple task.
