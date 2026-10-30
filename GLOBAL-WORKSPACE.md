# GobboNet Global workspace 🧜‍♀️

An optional Linux/container workspace around upstream GobboNet: **Tailscale,
Obsidian, Rootshell and TUIOS**. Keep the original local-first experience intact.
This fork is independent; additions are not upstream endorsements.

## Baseline reviewed

2026-10-30: fork HEAD and freshly fetched upstream main both equal
`02f6291f47fc76c84c050912fa9407987f32104b` (v1.7.8), the same source pin used by
our working prototype. There are no newer main commits to integrate at this checkpoint.

Upstream already supplies Linux .deb/.rpm/AppImage/ZIP entry points, the browser
wizard, external-backend configuration, a supervisor, shared chat state and tests.
Reuse these instead of duplicating model management or patching generated assets.

## Integration boundaries

| Addition | Role | First step |
| --- | --- | --- |
| Tailscale | Explicit private host/tablet access | Audit and adapt existing bridge; retain upstream access restrictions |
| Obsidian | Shared setup notes and continuity | Guided Sync workflow, marked mockups and official docs; preserve existing vault |
| Rootshell | iPad terminal client | Document SSH/TUIOS connection; no client credentials in the container |
| TUIOS | Reconnectable console and agent/model panes | Port isolated container startup and saved-layout handling |

**gobo-workspace** names the next revision with persistent volumes and Obsidian Sync.
Cloud discovery/pricing/provisioning is later, explicit and budget-controlled—not a default
network behavior, cloud dependency or automatic update check.

## Small, reviewable changes

1. Bring container/uv scaffolding and focused adapters into this fork on separate commits.
   Keep the Go module path and upstream launcher behavior; do not import an entire second
   README, changelog, package cache or `.git` history over upstream.
2. Check every network destination/dependency against CONTRIBUTING.md. Remote/cloud
   integrations stay opt-in. Never auto-install Sync, alter host auth or rent resources.
3. Audit reverse-proxy trust before reusing the prototype bridge: upstream's config editor
   intentionally rejects remote browsers and forwarding headers. Rewriting Host/Origin to
   loopback must not make a remote visitor appear local. Preserve that boundary with tests.
4. Add setup/persistence/reconnect tests and run upstream's relevant suites. Keep the two
   wizard copies synchronized if either changes. Generated embedded assets are never edited.
5. Prove fresh-machine startup and recreation before moving the existing user's runtime.
6. Prepare focused upstream proposals only after human validation. Outreach is deferred;
   no issue, PR or message has been sent to the upstream authors.

## Existing source and running state

The consolidated prototype lives at `/home/johnycsh/dex/globo-gobbo-net`, checkpoint
`1913da8`. Its scripts, Dev Container and curated screenshots are the source material,
not yet imported here. The live app still uses `/workspace/repos/workspace-lab`.
Original repos, models, chats, credentials and services remain untouched.

## See also

- [Linux start](LINUX-START-HERE.md) — Original first-party setup experience.
- [Contributing](CONTRIBUTING.md) — Privacy and contribution requirements.
- [Agent guide](AGENTS.md) — Source layout and testing contracts.
- [Linux installer](installer-linux/README.md) — Launcher and wizard implementation notes.
