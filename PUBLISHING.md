# Publishing Instructions

This document contains instructions for publishing the @boblangley/mcp-ssh package to GitHub Packages' npm registry.

## Prerequisites

1. The package name must stay scoped to the repository owner: `@boblangley/mcp-ssh`
2. The package repository metadata must point at `https://github.com/boblangley/mcp-ssh`
3. The GitHub Actions workflow needs `packages: write` permission and uses `GITHUB_TOKEN`

## Publishing Process

### Automated Publishing (Recommended)

The package is automatically published when you create a GitHub release:

1. Commit all changes
2. Create a new release on GitHub
3. The GitHub Action will automatically publish to GitHub Packages

### Manual Publishing

```bash
# 1. Make sure you're on the main branch and everything is committed
git checkout main
git pull origin main

# 2. Bump the version (patch, minor, or major)
npm version patch  # or minor/major

# 3. Publish to GitHub Packages
npm publish --registry=https://npm.pkg.github.com

# 4. Push the version commit and tag
git push origin main --tags
```

### Testing Before Publishing

```bash
# Test the package locally
npm pack
npm install -g ./boblangley-mcp-ssh-1.0.0.tgz

# Test the binary
mcp-ssh --help

# Clean up
npm uninstall -g @boblangley/mcp-ssh
rm *.tgz
```

## First-Time Setup

If this is the first time publishing this package:

```bash
# Login to GitHub Packages with a classic PAT
npm login --scope=@boblangley --auth-type=legacy --registry=https://npm.pkg.github.com

# Verify package metadata points at the fork
npm pkg get name repository.url publishConfig.registry

# Publish the package
npm publish --registry=https://npm.pkg.github.com
```

## Package Configuration

The package is configured with:
- Scoped name: `@boblangley/mcp-ssh`
- Registry: `https://npm.pkg.github.com`
- Binary: `mcp-ssh` command
- Entry point: `server.mjs`
