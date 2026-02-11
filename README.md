# ipcn

A tiny CLI to query IP/domain geolocation and ASN details.

## Usage

```bash
./ipcn 8.8.8.8
./ipcn example.com
```

## Requirements

- curl
- jq

## Release

```bash
git tag v0.2.0
git push --tags
```

## Homebrew sync

This repo can auto-sync the formula in `yuxi1989/homebrew-ipcn` when a tag is pushed.

Required GitHub repository secret in this repo:

- `HOMEBREW_TAP_GITHUB_TOKEN` (recommended) or `TOKEN`: token with push access to `yuxi1989/homebrew-ipcn`

Optional GitHub repository variable in this repo:

- `HOMEBREW_TAP_REPO`: defaults to `yuxi1989/homebrew-ipcn`

Workflow file:

- `.github/workflows/sync-homebrew.yml`

Release guard:

- Tag sync fails if `ipcn` has no changes compared with the previous `v*` tag.
