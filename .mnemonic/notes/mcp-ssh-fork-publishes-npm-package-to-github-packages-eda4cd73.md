---
title: mcp-ssh fork publishes npm package to GitHub Packages
tags:
  - security
  - publishing
  - github-packages
  - mcp-ssh
lifecycle: permanent
createdAt: '2026-05-25T13:27:13.985Z'
updatedAt: '2026-05-25T13:27:13.985Z'
role: decision
alwaysLoad: false
project: github-com-boblangley-mcp-ssh
projectName: mcp-ssh
memoryVersion: 1
---
The `mcp-ssh` fork at `boblangley/mcp-ssh` intentionally publishes the npm package as `@boblangley/mcp-ssh` to GitHub Packages, not npmjs and not GHCR.

Commit `87e4bdf` changed the release workflow to use `https://npm.pkg.github.com` with `GITHUB_TOKEN`, updated package metadata and docs to the Bob Langley fork scope, restored `.mnemonic/.gitignore`, refreshed the lockfile to clear npm audit findings, and hardened SSH_ASKPASS helper creation by using a private temporary directory plus exclusive file creation.

Verification before push: `npm test` passed 99 tests, `npm audit --audit-level=high` reported zero vulnerabilities, `npm pack --dry-run` produced `@boblangley/mcp-ssh@1.3.8`, `git diff --check` passed, and workflow YAML parsed with `yq`. Local `actionlint` was unavailable.
