# homebrew-tap

Homebrew tap for [@fabiocicerchia](https://github.com/fabiocicerchia)'s tools.

```sh
brew tap fabiocicerchia/tap
brew install fabiocicerchia/tap/<tool>
```

Every tool here ships its man page, so `man <tool>` works after installing.

## Casks — the compiled tools

Prebuilt Go binaries, macOS. Each one is published by its own release, straight
from the `homebrew_casks:` block in that repository's `.goreleaser.yaml`.

| Cask | What it does |
| --- | --- |
| `aws-killswitch` | Stop an AWS account spending, without losing anything |
| `chicco` | Local OpenAI- and Anthropic-compatible rotation proxy |
| `dark-canary` | Mirror traffic to a shadow deployment and diff the responses |
| `expiry-radar` | One inventory of everything that expires, ranked by blast radius |
| `llm-fit` | Which LLMs this machine can run, and how fast |
| `sci-disclose` | Software Carbon Intensity (SCI) from the command line |

`offline` and `azkaban` are absent on purpose: both are built on namespaces,
Landlock and seccomp, so they are Linux-only and there is nothing to install on
a Mac.

## Formulae — the scripts and the Python tools

These build from a source tarball, so they work on macOS *and* Linux, and they
can depend on the tools they actually shell out to.

| Formula | What it does | Notes |
| --- | --- | --- |
| `chaosbox` | Small, time-boxed chaos experiments | Linux |
| `cluster-collect` | Gather a Kubernetes incident support bundle | needs kubectl |
| `netreport` | One-shot connectivity snapshot for incident notes | Linux |
| `init-toolkit` | `wait-for` and the HTTP/TCP health probes | |
| `portfwd` | Several kubectl port-forwards from a profile | needs kubectl |
| `security-scanner-toolbox` | `scan-image` and `verify-download` | Linux |
| `arch-map` | A living C4-style container diagram | |
| `automap` | Generate an architecture map from a source tree | |
| `backup-verify` | Prove that your backups restore | |
| `claude-keepalive` | Run claude and auto-resume after a limit reset | |
| `cron-translate` | Cron expressions in human terms | |
| `dockerfile-hardener` | Rewrite a Dockerfile to best practice | |
| `envdiff` | Diff environment variables between two environments | |
| `greenlint` | Static linter for carbon-inefficient code and CI | |
| `k8s-rightsizer-report` | Live usage into PR-ready requests and limits | needs kubectl |
| `rbac-audit` | Readable RBAC reports from a live cluster | needs kubectl |
| `sbom-diff` | Diff two SBOMs in plain language | |
| `scoville` | Rate how dangerous a shell command is | |
| `toil-audit` | Quantify the cost of babysitting CI/CD | |

A tool appears here only once a release of it carries the command and its man
page. The rest are listed in `tools.json` and join automatically.

## Everything here is generated

Do not edit `Formula/` or `Casks/` by hand — the next run overwrites it.

- **Casks** come from each tool's release, via goreleaser.
- **Formulae** come from `tools.json`, rendered by `scripts/render_formulae.py`
  and refreshed daily by `.github/workflows/update-formulae.yml`. To add a tool,
  add it to `tools.json`.

The split is not a preference: homebrew-core requires a formula to build from
source, and the Go tools ship prebuilt signed binaries, so those are casks.

## Not here

The Python tools are all on PyPI too — `pipx install <tool>` is the same thing
without Homebrew. On Linux every tool is also published as a `.deb`, `.rpm`,
`.apk` and Arch package on its own release page.

The seven tools that only ever run as a container image, the GitHub Actions and
the Terraform modules have nothing to install; GHCR, the Marketplace and the
Terraform registry are their channels.

## Gatekeeper

The cask binaries are not notarized, so macOS quarantines them on download.
Each cask says so in its caveats, with the one-line fix.
