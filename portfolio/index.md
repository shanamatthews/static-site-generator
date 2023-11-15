---
title:  'Portfolio'
author: 'Shana'
keywords: [nothing, nothingness]
---

Regardless of job title (software engineer, developer advocate, technical writer, etc.), I've spent my entire career creating content and tools to help developers make things.

While I have experience [giving talks](../talks/index.html) and creating video content, my preference has always been for creating written content, especially tutorials and API/SDK documentation. Written content is more maintainable, flexible, and accessible than video, and frankly, more useful, in my opinion.

This page gives some examples of written content that I've worked on.

## API and SDK docs

<!-- ### Sentry -->

I currently work at [sentry.io](https://sentry.io/welcome/) where I maintain Sentry SDK docs in collaboration with the SDK developers. I also maintain the [docs site itself](https://github.com/getsentry/sentry-docs/) (a Gatsby project hosted on Vercel), and the API docs in collaboration with  product engineers.

Sentry is open source and part of my role also includes empowering external contributors, both by working with them on docs contributions, and by helping Sentry employees make [internal documentation public](https://develop.sentry.dev/) so external contributors can contribute to Sentry SDKs and product code. Additionally, since our docs site is open source, you can see all my contributions to Sentry's docs via the [project's commit history](https://github.com/getsentry/sentry-docs/commits?author=shanamatthews).

- [Sentry SDK docs](https://docs.sentry.io/platforms/). Sentry provides SDKs to add to your project to collect error and performance data for more than 20 languages. Each SDK is custom written to work best with its language and each SDK has slightly different features and API surface. This gives the best user experience, but requires more work to maintain accurate documentation. I collaborate with 12 full-time SDK developers plus additional contractors to keep our SDK docs up to date. I help make sure docs are consistent between SDKs and adhere to our docs best practices and internal style guide. I also collaborate on bigger projects like [improving our information architecture](https://github.com/getsentry/sentry-docs/pull/8152) and coordinating across the organization to ensure [new SDKs](https://github.com/getsentry/sentry-docs/pull/6808) ship with docs included.

- [Sentry API docs](https://docs.sentry.io/api/). Sentry provides a REST API to access the Sentry platform programmatically. Our API docs are created using OpenAPI 3 and custom code to generate pages in Gatsby from the OpenAPI spec. Older endpoints require you to manually edit the OpenAPI spec, but newer endpoints use [`drf-spectacular`](https://drf-spectacular.readthedocs.io/en/latest/) to automatically create OpenAPI spec entries from the code. I collaborate with product engineers working to publish new endpoints to ensure they also publish API docs that follow our best practices and style guide. This involved authoring documentation for Sentry engineers about [how to publish new endpoints](https://develop.sentry.dev/api/public/). Since Sentry is fully open-source, Sentry encourages employees to make internal docs public whenever possible. I also worked closely with the lead engineer for Sentry's APIs to rewrite our internal docs on creating creating new APIs and make the [new docs public](https://develop.sentry.dev/api/). This enables external contributors to help author APIs.

<!-- ### Coinbase -->

## Tutorials

<!-- ### Sentry -->

- [Frontend Error Monitoring Tutorial](https://docs.sentry.io/product/sentry-basics/integrate-frontend/). I created a new [React sample app](https://github.com/getsentry/frontend-tutorial) for this tutorial, that uses Webpack without `create-react-app` to more accurately represent user experience. I also rewrote the tutorial content to demonstrate Sentry best practices and highlight new features, as well as follow docs best practices and style guide.

- [Create a Sentry Authentication Token](https://docs.sentry.io/api/guides/create-auth-token/) and [Create and List Teams with the Sentry API](https://docs.sentry.io/api/guides/teams-tutorial/). Authored two new beginner-friendly tutorials to help users authenticate and get started with Sentry's APIs. The prerequisites for authenticating with Sentry's APIs is nonstandard and I created these tutorials to mitigate user confusion as engineering work happened to make authentication easier.
<!--
### Coinbase

### Microsoft

## Other docs-related projects

### Algolia -->
