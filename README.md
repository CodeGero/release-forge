# Release Forge — Smart Release Automation

Auto-detect version bump type from commits, generate changelog, and create GitHub releases — all in one action.

## Quick Start

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
```

## How It Works

Release Forge reads your commit messages and auto-detects the bump type:

| Commit prefix | Bump |
|--------------|------|
| `BREAKING CHANGE:`, `major:` | **Major** (1.0.0 → 2.0.0) |
| `feat:`, `feature:`, `minor:` | **Minor** (1.0.0 → 1.1.0) |
| `fix:`, `docs:`, `chore:`, `patch:` | **Patch** (1.0.0 → 1.0.1) |

Then it:
1. Calculates the new version
2. Updates your version file
3. Generates/updates CHANGELOG.md
4. Creates a GitHub Release with auto-generated notes

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `github-token` | *required* | GitHub token |
| `version-file` | `""` | Path to version file |
| `changelog-file` | `CHANGELOG.md` | Changelog path |
| `draft` | `false` | Create as draft |
| `prerelease` | `false` | Mark as prerelease |

## Premium Upgrade

Get advanced features at https://kryptorious.gumroad.com/l/jbvet:
- Conventional commit strict mode
- Custom changelog templates
- Slack/Discord release notifications
- Multi-package monorepo support
- Release analytics dashboard

## License

MIT
