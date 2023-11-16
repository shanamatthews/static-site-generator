---
title:  'Portfolio'
author: 'Shana'
keywords: [nothing, nothingness]
---

Regardless of job title (software engineer, developer advocate, technical writer, etc.), I've spent my career creating content and tools to help developers build things.

While I have experience [giving talks](../talks/index.html) and creating video content, my preference has always been for creating written content, especially tutorials and API/SDK documentation. Written content is more maintainable, flexible, and accessible than video content, and in my opinion, more useful.

This page gives some examples of written content that I've worked on.

## SDK and API docs

<!-- ### Sentry -->

I work at [sentry.io](https://sentry.io/welcome/) where I maintain Sentry SDK docs in collaboration with the SDK developers. I also maintain the [docs site itself](https://github.com/getsentry/sentry-docs/) (a Gatsby project hosted on Vercel), and the API docs in collaboration with  product engineers.

Sentry is open source and part of my job is to empower external contributors. This involves triaging and routing issues, and helping contributors make pull requests to our docs repo. This also involves helping Sentry employees make [internal documentation public](https://develop.sentry.dev/), so external contributors can contribute to Sentry SDKs and product code. Since our docs site is open source, you can see all my contributions to Sentry's docs via the [project's commit history](https://github.com/getsentry/sentry-docs/commits?author=shanamatthews).

- [Sentry SDK docs](https://docs.sentry.io/platforms/). Sentry provides SDKs to for more than 20 languages. Each SDK is custom, with slightly different features and API surface. This gives the best user experience, but requires more work to maintain accurate documentation.
  - I collaborate with 12 full-time SDK developers plus additional contractors to keep our SDK docs up to date. This includes ensuring docs are consistent between SDKs and adhere to our docs best practices and internal style guide.
  - I also work on bigger projects like [improving our information architecture](https://github.com/getsentry/sentry-docs/pull/8152) and coordinating across the organization to make sure [new SDKs](https://github.com/getsentry/sentry-docs/pull/6808) ship with docs included.

- [Sentry API docs](https://docs.sentry.io/api/). Sentry provides a REST API to access the Sentry platform programmatically. Our API docs are created using OpenAPI 3 and custom code to generate pages in Gatsby from the OpenAPI spec. Older endpoints require you to manually edit the OpenAPI spec, but newer endpoints use [`drf-spectacular`](https://drf-spectacular.readthedocs.io/en/latest/) to automatically create OpenAPI spec entries from the code.
  - I collaborate with product engineers ensure new endpoints are published with API docs that follow our best practices and style guide.
  - This also involves publishing documentation for Sentry engineers and external contributors on [how to publish new endpoints](https://develop.sentry.dev/api/public/). I worked closely with the lead engineer for Sentry's APIs to rewrite our internal docs on creating new APIs and make the [new docs set public](https://develop.sentry.dev/api/).
  - Here are some specific endpoints I helped document:
    - [Create a Metric Alert Rule for an Organization](https://docs.sentry.io/api/alerts/create-a-metric-alert-rule-for-an-organization/). Sentry's Metric Alert Rules are complex. While creating docs for this endpoint I collaborated with the technical writer who owns the product docs for [Metric Alert Rules](https://docs.sentry.io/product/alerts/alert-types/#metric-alerts) to revamp those docs and cross link between them to ensure all necessary information was available from both pages.
    - [Create an Issue Alert Rule for a Project](https://docs.sentry.io/api/alerts/create-an-issue-alert-rule-for-a-project/). This endpoint also required extensive documentation, including JSON snippets to better explain how to provide the correct data formats as params.

### Coinbase

- [JSON-RPC API docs for Coinbase Chainnode](https://playground.open-rpc.org/?schemaUrl=https://node-openrpc.s3.us-west-2.amazonaws.com/node-openrpc.json&uiSchema[appBar][ui:examplesDropdown]=false&uiSchema[appBar][ui:input]=false&uiSchema[appBar][ui:title]=Node%20JSON-RPC%20API). I authored API docs for an alpha version of [Coinbase Chainnode](https://github.com/coinbase/chainnode) for 10 large Coinbase customers. These docs use [OpenRPC](https://open-rpc.org/), a specification and set of tools to document JSON-RPC APIs, based on OpenAPI. OpenRPC tooling is less mature than OpenAPI and there's no tool to generate OpenRPC specs from code. This meant I had to create the (2460 line) [OpenRPC spec](https://github.com/shanamatthews/node-openrpc/blob/main/node-openrpc.json) by hand, including example requests and results, and reusable OpenRPC objects for all object types (see "`components`"). Authoring these docs required very close collaboration with the engineers building the beta APIs, including participating in API design reviews and reading the Golang codebase. I left Coinbase before this project's beta release, and it appears the product's final scope is significantly smaller than was planned.

## Tutorials

<!-- ### Sentry -->

- [Frontend Error Monitoring Tutorial](https://docs.sentry.io/product/sentry-basics/integrate-frontend/). I rewrote this tutorial to bring it up to date and demonstrate Sentry best practices, as well as follow docs best practices and style guide. I also created a new [React sample app](https://github.com/getsentry/frontend-tutorial) for this tutorial that uses Webpack without `create-react-app` to more accurately represent user experience.

- [Create a Sentry Authentication Token](https://docs.sentry.io/api/guides/create-auth-token/) and [Create and List Teams with the Sentry API](https://docs.sentry.io/api/guides/teams-tutorial/). Authored these two new beginner-friendly tutorials to help users authenticate and get started with Sentry's APIs. The prerequisites for authenticating with Sentry's APIs is nonstandard and I created these tutorials to mitigate user confusion as engineering work happened to make authentication easier.

### Coinbase

- [Coinbase Wallet Integration Tutorials](https://docs.cloud.coinbase.com/wallet-sdk/docs/wagmi). I authored the Wagmi, Web3-Onboard, Web3-React, and Web3Modal integration tutorials for Coinbase Wallet, based on React sample apps an engineer on the Wallet SDK team created in CodeSandbox.

<!--
### Microsoft

## Other docs-related projects

### Algolia -->
