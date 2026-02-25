# ipcn

A tiny CLI to query IP/domain geolocation and ASN details.

一个轻量的命令行工具，用于查询 IP/域名的地理位置、运营商和 ASN/BGP 信息。

Related project: [homebrew-ipcn](https://github.com/yuxi1989/homebrew-ipcn)

## Usage

```bash
./ipcn 8.8.8.8
./ipcn example.com
./ipcn --all-ips example.com
./ipcn --ipv6 --json example.com
./ipcn --lang en --fields ip,country,asn 8.8.8.8
./ipcn --timeout 6 --retries 2 example.com
./ipcn -f targets.txt
```

## Options

- `-v, --version`: show version
- `-h, --help`: show help
- `--lang <zh|en>`: output language (default: auto-detect from system locale)
- `--timeout <sec>`: request timeout seconds (default `10`)
- `--retries <n>`: retry count for API requests (default `1`)
- `--fields <list>`: comma-separated output fields, e.g. `ip,country,asn`
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
git tag v0.2.5
git push --tags
```

## Signing Policy

- All commits in this repository must be GPG-signed.
- All release tags in this repository must be GPG-signed.
- Local recommended git settings:
  - `git config commit.gpgsign true`
  - `git config tag.gpgsign true`
  - `git config user.signingkey D2223998BC2A8C28`

Version note:

- `ipcn -v` will read the latest git tag only when running inside the `yuxi1989/ipcn` git repository.
- For Homebrew installs, `ipcn -v` reports the Cellar package version.
- You can override it by setting `IPCN_VERSION`, e.g. `IPCN_VERSION=v0.2.5 ipcn -v`.

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
- `ip-api.com` free JSON endpoint is rate-limited (documented as 45 requests/minute per source IP); heavy overuse can trigger temporary blocks.
- Team Cymru whois does not publish a fixed numeric limit, but abusive/high-volume usage may be null-routed or blocked.
- Do not send sensitive data unless you accept the external service's terms and privacy practices.
