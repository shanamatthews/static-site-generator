# Static site generator + blog

This is a super simple static site generator written with `pandoc` and a few lines of bash script.

The [`build`](https://github.com/shanamatthews/static-site-generator/blob/main/build) script generates the site using `pandoc`. This script must be run after any changes & before pushing to GitHub.

Posts with `draft: true` in the frontmatter will be ignored by the build script.

Idea inspired by [rwxrob](https://github.com/rwxrob/).

### how to run locally

You can preview this locally with my [`preview`](https://github.com/shanamatthews/dotfiles/blob/main/scripts/preview) script.

### Hosting

This is hosted using [Azure Static Webapps](https://learn.microsoft.com/azure/static-web-apps/getting-started?tabs=vanilla-javascript) because it's free 🎉 and uses the associated GitHub plugin for CI/CD.

Currently hosted at [shana.codes](https://shana.codes/).
