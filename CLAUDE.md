# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

The project guide is AGENTS.md (architecture, house rules, full test and build
commands). It is imported here so there is one copy to keep current:

@AGENTS.md

## Additions for working in this tree

### Running one test

```sh
node tests/test-markdown-render.mjs          # one frontend suite (plain Node, no install)
python3 tests/test-engine-args.py            # one launcher/installer suite
bash ./stage-web.sh && go test ./internal/supervisor/...          # one Go package
bash ./stage-web.sh && go test ./internal/server -run TestName    # one Go test
```

- `tests/README.md` explains what each non-obvious suite pins and why; read the
  entry for a suite before changing what it guards.
- `tests/test-stop-script.py` skips half its checks without PowerShell 7
  (`pwsh`, or `GOBBONET_TEST_PWSH`), and says so.
- Without `stage-web.sh`, the embed is empty and the server falls back to
  serving the repo root from disk (`internal/server/webroot.go`). Builds still
  work, but tests that depend on embedded assets need staging first.

### Version bumps

`VERSION` is the release number most things read. Two places hold it as a
literal and must be changed by hand; tests fail if they drift:

- `GOBBONET_UI_VERSION` in `js/01-config.js` (`tests/test-version-stamp.mjs`)
- `APPVER`, `OutFile` and `VIProductVersion` in `installer-win/gobbonet.nsi`
  (`tests/test-version-strings.py`)

### Keeping AGENTS.md true

AGENTS.md says the code wins when the two disagree, and that the doc must be
fixed in the same change. If a change moves a file, function, route or setting
it names, update AGENTS.md too. `make-zip.sh` ships it inside the ZIP.
