# homebrew-tap

Homebrew tap for [@fabiocicerchia](https://github.com/fabiocicerchia)'s tools.

```sh
brew tap fabiocicerchia/tap
brew install fabiocicerchia/tap/<tool>
```

## What is here

| Cask | What it does |
| --- | --- |
| `aws-killswitch` | Stop an AWS account spending, without losing anything |
| `chicco` | Local OpenAI- and Anthropic-compatible rotation proxy |
| `dark-canary` | Mirror traffic to a shadow deployment and diff the responses |
| `expiry-radar` | One inventory of everything that expires, ranked by blast radius |
| `llm-fit` | Which LLMs this machine can run, and how fast |
| `sci-disclose` | Software Carbon Intensity (SCI) from the command line |

Each cask ships the binary and its man page, so `man <tool>` works after
installing.

## These files are generated

Every `Casks/*.rb` here is written by [GoReleaser][gr] when the tool it belongs
to cuts a release — the source of truth is the `homebrew_casks:` block in that
tool's `.goreleaser.yaml`, not this repository. Edits made here are overwritten
by the next release.

Casks, rather than formulae, because homebrew-core requires a formula to build
from source and these are prebuilt, signed binaries.

## Not everything is here

Two tools are Linux-only by nature — `offline` and `azkaban` build on
namespaces, Landlock and seccomp — so they have no macOS cask. On Linux, every
tool is published as a `.deb`, `.rpm`, `.apk` and Arch package on its own
release page.

The Python tools are on PyPI; `pipx install <tool>` is their equivalent.

## Gatekeeper

These binaries are not notarized, so macOS quarantines them on download. Each
cask says so in its caveats, with the one-line fix. Notarization would remove
the step and needs an Apple Developer account.

[gr]: https://goreleaser.com/customization/homebrew_casks/
