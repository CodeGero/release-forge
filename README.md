# Release Forge — Smart Release Automation

[![Marketplace](https://img.shields.io/badge/Marketplace-release--forge-green)](https://github.com/marketplace/actions/release-forge)
[![Version](https://img.shields.io/badge/version-1.0.0-green)](https://github.com/CodeGero/release-forge/releases)

**Auto-detect version bumps from commits, generate changelogs, and create GitHub releases.** One action, zero config.

---

## Quick Start

```yaml
- uses: CodeGero/release-forge@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

## How It Works

Release Forge reads your conventional commits:

| Commit Prefix | Bump Type |
|--------------|-----------|
| `BREAKING CHANGE:`, `major:` | **Major** (1.0 → 2.0) |
| `feat:`, `feature:` | **Minor** (1.0 → 1.1) |
| `fix:`, `docs:`, `chore:` | **Patch** (1.0 → 1.0.1) |

Then automatically:
1. Calculates new version
2. Updates version file (pyproject.toml, package.json, etc.)
3. Generates CHANGELOG.md entry
4. Creates GitHub Release with release notes

## Full Workflow

```yaml
name: Release
on:
  push:
    branches: [main]
jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: CodeGero/release-forge@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          version-file: pyproject.toml
```

## Inputs

| Input | Default | What it does |
|-------|---------|-------------|
| `github-token` | *required* | For creating releases |
| `version-file` | `""` | Path to version file |
| `changelog-file` | `CHANGELOG.md` | Changelog path |
| `draft` | `false` | Create as draft |
| `prerelease` | `false` | Mark as prerelease |

## Premium

https://kryptorious.gumroad.com/l/jbvet — Conventional commit strict mode, custom templates, monorepo support.

MIT License
