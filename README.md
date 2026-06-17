# Weavz Local Browser Use

[![npm version](https://img.shields.io/npm/v/%40weavz-io%2Flocal-browser-use?label=npm)](https://www.npmjs.com/package/@weavz-io/local-browser-use)
[![npm downloads](https://img.shields.io/npm/dm/%40weavz-io%2Flocal-browser-use?label=downloads)](https://www.npmjs.com/package/@weavz-io/local-browser-use)
[![GitHub release](https://img.shields.io/github/v/release/weavz/weavz-local-browser-use?label=release)](https://github.com/weavz/weavz-local-browser-use/releases)
[![Release workflow](https://github.com/weavz/weavz-local-browser-use/actions/workflows/release.yml/badge.svg?branch=main)](https://github.com/weavz/weavz-local-browser-use/actions/workflows/release.yml)
[![License](https://img.shields.io/npm/l/%40weavz-io%2Flocal-browser-use?label=license)](https://github.com/weavz/weavz-local-browser-use/blob/main/LICENSE)

Local browser companion for [Weavz](https://weavz.io) Agent Local Browser Control.

It opens a dedicated Chrome or Chromium profile on a user's machine and connects outbound to a Weavz browser session. Agents can then use the Weavz browser tools against that visible local browser while the user can complete logins, MFA, CAPTCHAs, device-trust checks, and password-manager flows on their own device.

## Usage

Start a local browser session from Weavz first. The `start_session` or `ensure_connected` action returns a `localRunnerCommand` that looks like this:

```bash
npx -y @weavz-io/local-browser-use connect \
  --url "<localRunnerUrl from start_session>" \
  --profile "<localProfileId>"
```

Run that command on the machine that should host the browser.

## Requirements

- Node.js 22.13+
- Google Chrome or Chromium installed locally
- A Weavz local browser session URL from `agent-local-browser-control`

If Chrome is not installed in a standard location, pass it explicitly:

```bash
npx -y @weavz-io/local-browser-use connect \
  --url "<localRunnerUrl from start_session>" \
  --profile "<localProfileId>" \
  --browser-executable "/path/to/chrome"
```

## Security

Treat the `localRunnerCommand` as a short-lived secret. It contains a session-scoped runner token and should only be run on the user or device that should attach the local browser.

By default, the CLI only accepts Weavz hosted local-runtime URLs and loopback development URLs. For self-hosted Weavz endpoints, pass `--allow-custom-url` only when you trust the endpoint:

```bash
npx -y @weavz-io/local-browser-use connect \
  --url "<self-hosted localRunnerUrl from start_session>" \
  --profile "<localProfileId>" \
  --allow-custom-url
```

The companion uses a dedicated profile under `~/.weavz/local-browser`; it does not attach to the user's default Chrome profile.

## Links

- [Weavz](https://weavz.io)
- [Documentation](https://weavz.io/docs/concepts/agent-browser#local-browser-control-experimental)
- [Dashboard](https://dashboard.weavz.io)
- [npm package](https://www.npmjs.com/package/@weavz-io/local-browser-use)
