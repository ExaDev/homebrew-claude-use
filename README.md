# homebrew-claude-use

Homebrew tap for [`claude-use`](https://github.com/ExaDev/claude-use), a profile manager and launcher for Claude Code.

## Install

```bash
brew install ExaDev/claude-use/claude-use
```

or, tapped separately first:

```bash
brew tap ExaDev/claude-use
brew install claude-use
```

Both install the same two commands, `claude` and `claude-use`, that the project's own `curl | sh` installer, `npm install -g claude-use`, and its Scoop bucket (Windows) all provide — see [the main repo's Install section](https://github.com/ExaDev/claude-use#install) for the full comparison across all four distribution channels.

## What this is

`Formula/claude-use.rb` fetches the precompiled, self-contained Node SEA binary from the matching [claude-use GitHub Release](https://github.com/ExaDev/claude-use/releases) for the running platform, rather than building from source — the whole point of the SEA binary is that installing it needs no Node.js toolchain, and building from source here would defeat that. macOS arm64 and both Linux architectures are Node core's own verified single-executable-application targets; the macOS x64 asset is published best-effort by the same release and is not a supported target upstream, but the formula still installs it on Intel Macs since it is the best available option there.

## Keeping the formula in sync with releases

The formula's `version` and every platform's `sha256` are regenerated from scratch and pushed here automatically by the `update-tap` job in `claude-use`'s own `release.yml`, immediately after each GitHub Release is published — never by hand. That job authenticates by checking this repository out directly with an SSH deploy key (`actions/checkout`'s `ssh-key` input), stored as the `HOMEBREW_TAP_DEPLOY_KEY` secret in the `ExaDev/claude-use` repository — the default `GITHUB_TOKEN` a workflow gets is scoped to the repo it runs in, so it cannot push here on its own. The corresponding public key is added to this repository's own Deploy keys (Settings → Deploy keys) with write access. Until both halves of that key pair exist, the `sha256` values above stay at their placeholder zeros and `brew install` will fail its checksum check, rather than silently installing something unverified.
