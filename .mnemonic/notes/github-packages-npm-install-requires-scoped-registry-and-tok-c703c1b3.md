---
title: GitHub Packages npm install requires scoped registry and token npmrc
tags:
  - github-packages
  - npm
  - mcp-ssh
  - gotcha
lifecycle: permanent
createdAt: '2026-05-25T13:49:07.693Z'
updatedAt: '2026-05-25T13:49:07.693Z'
role: context
alwaysLoad: false
project: github-com-boblangley-mcp-ssh
projectName: mcp-ssh
memoryVersion: 1
---
Installing or running `@boblangley/mcp-ssh` from GitHub Packages requires npm registry configuration. Plain `npx @boblangley/mcp-ssh` defaults to `registry.npmjs.org` and fails with E404 because the package is published to GitHub Packages.

Working local npm config shape:

```text
@boblangley:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${NODE_AUTH_TOKEN}
```

The auth-token line must contain `${NODE_AUTH_TOKEN}` without a leading backslash. If it is written as `\${NODE_AUTH_TOKEN}`, npm sends the literal placeholder and GitHub Packages returns E401. After fixing `~/.npmrc`, `npm view @boblangley/mcp-ssh version` returned `1.3.8`, and `npx --yes --registry=https://npm.pkg.github.com @boblangley/mcp-ssh --silent` started cleanly.
