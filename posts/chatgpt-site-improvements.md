---
title: chatgpt-site-improvements
author: Shana
keywords: [no, nothing]
date: 2023-02-27
draft: true
---
I've been in a personal-projects slump recently, as evidenced by my GitHub activity chart, yikes.

![](../images/github-dots.png)

This is mostly because of some health stuff that came up early in January and I'm still dealing with. However, I've been doing better over the last couple of weeks and I've found some energy and excitement to start playing around, particularly with ChatGPT-related things.

### This website

I'm really proud of myself for creating this site with my own static site generator [written with just Bash scripts](./static-site-generator-with-bash.html). I think it's sick and it aligns with my stance on not needing a framework or fancy tech to do every single thing.

However the reality is... I kinda suck at Bash scripting. I don't use Bash regularly at work, or even in personal projects, so whenever I want to go in to make tweaks to this site, I always feel super rusty and it takes ages just to remember how this very simple project works. That means that adding new "features" like the ability to have draft posts feels really tedious.

That's where ChatGPT comes in! I'd read some really promising things about folks using ChatGPT to help them with super simple scripting and I wanted to try it out with this site.

I tested out ChatGPT by feeding it my [`build` script](https://github.com/shanamatthews/static-site-generator/blob/main/build) and asking what it did. It was very accurate! Impressive!

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
>```

This was kinda right, but if "draft: true" appeared anywhere in the post, it would skip it. It's not likely that I'd write that phrase outside of the frontmatter, but I'd rather not run into that weird and confusing bug later.

With a little more prompting, ChatGPT gave me a better answer:

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
>```

Nice! That works much better. It also grabbed the post date from the frontmatter specifically, which is better than what I was doing before. Stylistically, I don't like to echo something into `sed` (not sure why...), so I updated the script to instead feed the post frontmatter to stdin for `sed` to use, but otherwise, this worked! Ship it!

After my success using ChatGPT for this, I was also inspired to have ChatGPT edit this script, as well as the [`create-post` script](https://github.com/shanamatthews/static-site-generator/blob/main/create-post) to print out error messages when something goes wrong. I'd been too lazy to do this and ChatGPT made it really easy.
