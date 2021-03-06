# Microsoft Authentication Library for JavaScript (MSAL.js) 2.0 for Browser-Based Single-Page Applications
[![npm version](https://img.shields.io/npm/v/@azure/msal-browser.svg?style=flat)](https://www.npmjs.com/package/@azure/msal-browser/)[![npm version](https://img.shields.io/npm/dm/@azure/msal-browser.svg)](https://nodei.co/npm/@azure/msal-browser/)[![Coverage Status](https://coveralls.io/repos/github/AzureAD/microsoft-authentication-library-for-js/badge.svg?branch=dev)](https://coveralls.io/github/AzureAD/microsoft-authentication-library-for-js?branch=dev)

| <a href="https://docs.microsoft.com/azure/active-directory/develop/guidedsetups/active-directory-javascriptspa" target="_blank">Getting Started</a> | <a href="https://aka.ms/aaddevv2" target="_blank">AAD Docs</a> | <a href="https://azuread.github.io/microsoft-authentication-library-for-js/ref/msal-core/" target="_blank">Library Reference</a> |
| --- | --- | --- |

1. [About](#about)
2. [FAQ](./FAQ.md)
3. [Releases](#releases)
4. [Prerequisites](#prerequisites)
5. [Installation](#installation)
6. [Usage](#usage)
    - [Migrating from Previous MSAL Versions](#migrating-from-previous-msal-versions)
    - [MSAL Basics](#msal-basics)
    - [Advanced Topics](#advanced-topics)
7. [Samples](#samples)
8. [Build and Test](#build-and-test)
8. [Authorization Code vs Implicit](#oauth-2.0-and-the-implicit-flow-vs-authorization-code-flow-with-pkce)
9. [Security Reporting](#security-reporting)
10. [License](#license)
11. [Code of Conduct](#we-value-and-adhere-to-the-microsoft-open-source-code-of-conduct)

## About

The MSAL library for JavaScript enables client-side JavaScript applications to authenticate users using [Azure AD](https://docs.microsoft.com/azure/active-directory/develop/v2-overview) work and school accounts (AAD), Microsoft personal accounts (MSA) and social identity providers like Facebook, Google, LinkedIn, Microsoft accounts, etc. through [Azure AD B2C](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview#identity-providers) service. It also enables your app to get tokens to access [Microsoft Cloud](https://www.microsoft.com/enterprise) services such as [Microsoft Graph](https://graph.microsoft.io).

The `msal-browser` package described by the code in this folder uses the [`msal-common` package](../msal-common/) as a dependency to enable authentication in Javascript Single-Page Applications without backend servers. This version of the library uses the OAuth 2.0 Authorization Code Flow with PKCE. To read more about this protocol, as well as the differences between implicit flow and authorization code flow, see the section [below](#oauth-2.0-and-the-implicit-flow-vs-authorization-code-flow-with-pkce). If you are looking for the version of the library that uses the implicit flow, please see the [`msal-core` library](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-core).

This is an improvement upon the current `msal-core` library which will utilize the authorization code flow in the browser. Most features available in the old library will be available in this one, but there are nuances to the authentication flow in both. The `msal-browser` package does NOT support the implicit flow.

**IMPORTANT:** Please be aware that this is not a production ready library. You are required to use a browser that disables CORS checks. The server will be making changes that will allow CORS requests and remove the requirement for client secret for applications which are registered using a `SPA` type redirect.

## FAQ

See [here](./FAQ.md).

## Releases

*Expect us to detail our major and minor releases moving forward, while leaving out our patch releases.  Patch release notes can be found in our change log.*

Date | Release | Announcement | Main features
------| ------- | ---------| ---------
January 17, 2020 | msal-browser v2.0.0-alpha | No release notes yet | Alpha version of the `msal-browser` package with authorization code flow for SPAs working in dev; relies on msal-common v1.0.0-alpha

## Prerequisites

- `msal-browser` is meant to be used in [Single-Page Application scenarios](https://docs.microsoft.com/azure/active-directory/develop/scenario-spa-overview).

- Before using `msal-browser` you will need to [register an application in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app) to get a valid `clientId` for configuration, and to register the routes that your app will accept redirect traffic on.

- You will also need a CORS-disabled browser until the AAD service has rolled out changes to introduce CORS requests on the `/token` endpoint. This is not a recommended production setting, but for the purposes of this alpha you should follow these instructions:
    - We recommend using Chrome for this. 
        - For Windows machines, you can do the following:
            1. Right click on your desktop -> New -> Shortcut
            2. Paste the following: 
            ```javascript
            "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --disable-web-security --disable-gpu --user-data-dir=~/chromeTemp
            ```
            3. Click next and create a name for the shortcut (i.e. Chrome-no-cors)
        - For other machines, you can follow the steps [here](https://alfilatov.com/posts/run-chrome-without-cors/) to figure out how to run Chrome withput CORS enabled for your OS.

## Installation
### Via NPM:
```javascript
npm install @azure/msal-browser
```
### Via CDN:

## Usage

### Migrating from Previous MSAL Versions

If you have MSAL v1.x currently running in your application, you can follow the instructions [here](./docs/v1migration.md) to migrate your application to using the `msal-browser` package.

### MSAL Basics

1. [Initialization](./docs/initialization.md)
2. [Logging in a User](./docs/loginuser.md)
3. [Acquiring and Using an Access Token](./docs/acquiretoken.md)
4. [Managing Token Lifetimes](./docs/renewtoken.md)
5. [Logging Out a User](./docs/logout.md)

### Advanced Topics

- [Configuration Options](./docs/configuration.md)
- [Request and Response Details](./docs/requestresponseobject.md)
- [Cache Storage](./docs/caching.md)
- [Logging](./docs/logging.md)

## Samples

The [`samples`](../samples) folder contains samples applications for our libraries. Here is a complete list of samples for the MSAL.js 2.x library:

| Sample | Description |
| ------ | ----------- |
| [Vanilla JS Sample](../../samples/VanillaJSTestApp2.0) | A vanilla Javascript sample showing basic usage of the MSAL 2.0 library (`msal-browser` package) with the Microsoft Graph API. |

Instructions to run the samples can be found in the respective READMEs.

## Build and Test

### Build Library
```javascript
// Change to the msal-browser package directory
cd lib/msal-browser/
// Ensure you are using the local build of msal-common
npm link @azure/msal-common
// To run build only for browser package
npm run build
// To run build for common and browser package
npm run build:all
```

### Running Tests
`msal-browser` uses [mocha](https://mochajs.org/) and [chai](https://www.chaijs.com/) to run unit tests, as well as Istanbul's [nyc](https://github.com/istanbuljs/nyc) tool for code coverage.

```javascript
// To run tests
npm test
// To run tests with code coverage
npm run test:coverage:only
```

## OAuth 2.0 and the Implicit Flow vs Authorization Code Flow with PKCE
MSAL.js 1.x implemented the [Implicit Grant Flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-implicit-grant-flow), as defined by the OAuth 2.0 protocol and [OpenID](https://docs.microsoft.com/azure/active-directory/develop/v2-protocols-oidc).

Our goal is that the library abstracts enough of the protocol away so that you can get plug and play authentication, but it is important to know and understand the implicit flow from a security perspective. The MSAL 1.x client for single-page applications runs in the context of a web browser which cannot manage client secrets securely. It uses the implicit flow, which optimized for single page apps and has one less hop between client and server so tokens are returned directly to the browser. These aspects make it naturally less secure. These security concerns are mitigated per standard practices such as- use of short lived tokens (and so no refresh tokens are returned), the library requiring a registered redirect URI for the app, library matching the request and response with a unique nonce and state parameter. You can read more about the [disadvantages of the implicit flow here](https://tools.ietf.org/html/draft-ietf-oauth-browser-based-apps-04#section-9.8.6).

The MSAL library will now support the Authorization Code Flow with PKCE for Browser-Based Applications without a backend web server. 
We plan to continue support for the implicit flow in the `msal-core` library.

You can learn further details about `msal-browser` functionality documented in our [docs folder](./docs) and find complete [code samples](#samples).

## Security Reporting

If you find a security issue with our libraries or services please report it to [secure@microsoft.com](mailto:secure@microsoft.com) with as much detail as possible. Your submission may be eligible for a bounty through the [Microsoft Bounty](http://aka.ms/bugbounty) program. Please do not post security issues to GitHub Issues or any other public site. We will contact you shortly upon receiving the information. We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.

## License

Copyright (c) Microsoft Corporation.  All rights reserved. Licensed under the MIT License (the "License");

## We Value and Adhere to the Microsoft Open Source Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
