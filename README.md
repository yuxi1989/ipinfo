# ipcn

A tiny CLI to query IP/domain geolocation and ASN details.

## Usage

```bash
./ipcn 8.8.8.8
./ipcn example.com
./ipcn --all-ips example.com
./ipcn --ipv6 --json example.com
./ipcn -f targets.txt
```

## Options

- `-v, --version`: show version
- `-h, --help`: show help
- `--json`: output JSON array
- `-f, --file <path>`: read query targets from file
- `--all-ips`: for domain, query all resolved A/AAAA records
- `--ipv4`: resolve/query IPv4 only
- `--ipv6`: resolve/query IPv6 only

## Requirements

- curl
- jq
- whois
- dig

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

## API Disclaimer

- `ipcn` relies on third-party network services (currently `ip-api.com` and Team Cymru whois).
- Query results, availability, latency, and accuracy depend on those services and your network.
- Third-party services may apply rate limits, blocks, or policy changes at any time.
- Do not send sensitive data unless you accept the external service's terms and privacy practices.
