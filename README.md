<!-- revenuedot:readme:start -->
<p align="center"><a href="https://revenuedot.app"><picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/revenuedot/revenuedot/main/brand/kit/wordmark/revenuedot-lockup-white.svg">
  <img alt="RevenueDot" src="https://raw.githubusercontent.com/revenuedot/revenuedot/main/brand/kit/wordmark/revenuedot-lockup-black.svg" height="40">
</picture></a></p>

# RevenueDot Web SDK

This is RevenueDot's MIT fork of RevenueCat's `@revenuecat/purchases-js`: the same classes and method names, pointed at a RevenueDot server ([RevenueDot Cloud](https://app.revenuedot.app/signup) at `https://api.revenuedot.app`, or one you host) with RevenueDot's response-signing key built in, and kept in sync with upstream.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE) [![npm](https://img.shields.io/npm/v/@revenuedot/purchases-js?label=npm)](https://www.npmjs.com/package/@revenuedot/purchases-js) [![Upstream](https://img.shields.io/badge/upstream-RevenueCat%2Fpurchases--js_1.67.0-lightgrey)](https://github.com/RevenueCat/purchases-js)

## Install

```sh
npm install @revenuedot/purchases-js
```
Or keep every import as it is with an npm alias in `package.json`:
```json
"@revenuecat/purchases-js": "npm:@revenuedot/purchases-js@1.67.0"
```

## Configure

```ts
import { Purchases } from "@revenuedot/purchases-js";

const purchases = Purchases.configure({
  apiKey: "test_...",      // the web app's public key from the RevenueDot dashboard
  appUserId: "user_123",
  // Self-hosted server only: RevenueDot Cloud (https://api.revenuedot.app) is the default. No trailing slash.
  httpConfig: { proxyURL: "https://revenuedot.example.com" },
});
```

The fork already trusts RevenueDot's signing key, so no signature or verification setting is needed. Analytics events follow `proxyURL` too, so `collectAnalyticsEvents` can stay on, and the checkout reads "Secure checkout by RevenueDot". Full guide: https://revenuedot.app/docs/sdks/web.

## What RevenueDot adds

- **Self-host for free, or use RevenueDot Cloud** free up to $10,000 a month of tracked revenue ([pricing](https://revenuedot.app/pricing)).
- **The same REST API and webhook payloads** as RevenueCat, so your backend and integrations keep working ([API reference](https://revenuedot.app/docs/api)).
- **Entitlements shared with your iOS and Android apps,** Test Store purchases in the browser, and real payments through RevenueDot's hosted Stripe checkout ([web billing guide](https://revenuedot.app/docs/guides/web-billing)).
- **A one-line migration:** point the stock SDK at RevenueDot with `httpConfig.proxyURL`, or install this fork and drop the line ([migration guide](https://revenuedot.app/docs/migrate)).

## Use with your coding agent

Coding agents can read this repository's docs and code on demand, so they use the right package and imports:

- **Context7:** https://context7.com/revenuedot/purchases-js
- **DeepWiki:** https://deepwiki.com/revenuedot/purchases-js
- **GitMCP:** https://gitmcp.io/revenuedot/purchases-js

## Links

- **Docs for this SDK:** https://revenuedot.app/docs/sdks/web
- **Example app:** https://github.com/revenuedot/examples/tree/main/web/purchases-js-vite
- **Releases and changelog:** https://github.com/revenuedot/purchases-js/releases (tags `<upstream version>-revenuedot`; upstream's changes are in `CHANGELOG.md`)
- **RevenueDot server and dashboard:** https://github.com/revenuedot/revenuedot
- **Fork pipeline (what we change and how upstream is merged):** https://github.com/revenuedot/revenuedot/tree/main/scripts/forks

RevenueDot is not affiliated with RevenueCat, Inc. RevenueCat's copyright notice stays in `LICENSE`; RevenueDot's changes are MIT too.

---

## Upstream README (RevenueCat's, unchanged)
<!-- revenuedot:readme:end -->

<h3 align="center">😻 In-App Subscriptions Made Easy 😻</h3>
<h4 align="center">🕸️ For the web 🕸️</h4>

RevenueCat is a powerful, reliable, and free to use in-app purchase server with cross-platform support.
This repository includes all you need to manage your subscriptions on your website or web app using RevenueCat.

Sign up to [get started for free](https://app.revenuecat.com/signup).

# Prerequisites

Login @ [app.revenuecat.com](https://app.revenuecat.com)

- Connect your Stripe account if you haven't already (More payment gateways are coming soon)
- Create a Project (if you haven't already)
- Add a new Web Billing app
- Get the sandbox API key or production API key (depending on the environment)
- Create some products for the Web Billing App
- Create an offering and add packages with Web Billing products
- Create the entitlements you need in your app and link them to the Web Billing products

# Installation

- Add the library to your project's dependencies
  - npm
    ```
    npm install --save @revenuecat/purchases-js
    ```
  - yarn
    ```
    yarn add --save @revenuecat/purchases-js
    ```

# Usage

See the [RevenueCat docs](https://www.revenuecat.com/docs/web/web-billing) and the [SDK Reference](https://revenuecat.github.io/purchases-js-docs).

# Development

## Install the library in a local project

- Clone the repository
- Install dependencies
- Build the library

```bash
pnpm install
pnpm run build:dev
```

For automatic rebuilds of the web entry point during development, run:

```bash
pnpm run build:dev-watch
```

`build:dev-watch` is web-only. It preserves the Vega artifacts produced by
`build:dev`, but does not rebuild them; rerun `pnpm run build:dev` after
changing code used by the Vega entry point.

To avoid publishing the package you can use pnpm's link feature:

1. In the purchases-js directory, register the package:

```bash
pnpm link
```

2. In your testing project, link to the registered package:

```bash
pnpm link "@revenuecat/purchases-js"
```

> **Note:** Any changes you make to the library will be automatically reflected in your testing project after running `pnpm run build:dev` or `pnpm run build`.

### Using a local `@revenuecat/purchases-ui-js`

When you need to iterate on both `purchases-js` and `purchases-ui-js` together, you can point this repo at a sibling checkout using a `pnpm-workspace.yaml` override (instead of manually editing `package.json`).

1. Place the two repos side by side, for example:

```
Developer/
  purchases-js/
  purchases-ui-js/
```

2. In `purchases-js`, create or edit `pnpm-workspace.yaml` and add:

```yaml
overrides:
  "@revenuecat/purchases-ui-js": "link:../purchases-ui-js"
```

Use the **scoped** package name (`@revenuecat/purchases-ui-js`). A key like `purchases-ui-js` will not apply the override.

3. Reinstall dependencies from the `purchases-js` root:

```bash
pnpm install
```

4. Verify the override resolved:

```bash
pnpm why @revenuecat/purchases-ui-js
```

You should see `link:../purchases-ui-js`.

5. Build the UI package when you change it (from `purchases-ui-js`), then rebuild or run dev builds in `purchases-js` as needed.

#### Reverting

Remove the override from `pnpm-workspace.yaml` and run `pnpm install` again to return to the published `@revenuecat/purchases-ui-js` version.

## Running Storybook

```bash
pnpm run storybook
```

### Environment Setup for Purchase Stories

> **Note:** This setup is only required if you need to test Storybook stories involving the `payment-entry` page.

To run these specific stories, you'll need to set up some environment variables. There are two options:

### Option 1: Internal Teams

Internal team members can find the required environment variables in 1Password.

### Option 2: Setup Manually

1. Create a test account in Stripe
2. Create a `.env.development.local` file and set the following variables:

```bash
VITE_STORYBOOK_PUBLISHABLE_API_KEY="pk_test_1234567890"
VITE_STORYBOOK_ACCOUNT_ID="acct_1234567890"
```

## Running tests

```bash
pnpm run test
```

## Running linters

```bash
pnpm run test:typecheck
pnpm run svelte-check
pnpm run prettier
pnpm run lint
```

## Running E2E tests

Please check the Demo app readme [here](./examples/webbilling-demo/README.md#e2e-tests)

## Update API specs

```bash
pnpm run extract-api
```

This will update the files in `api-report` and `vega/api-report` with the latest public API for both packages.
If it has uncommitted changes, CI tests will fail. Run this command and commit the changes if
they are expected.

# Publishing a new version

New versions are automated weekly, but you can also trigger a new release through CircleCI or locally
following these steps:

- Run `bundle exec fastlane bump` and follow the instructions
- A PR should be created with the changes and a hold job in CircleCI.
- Approve the hold job once tests pass. This will create a tag and continue the release in CircleCI
- Merge the PR once it's been released
