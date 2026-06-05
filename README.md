# scoop-bucket

A [Scoop](https://scoop.sh) bucket for Cameron's Windows tools. Currently ships
[`cadence-hooks`](https://github.com/cameronsjo/cadence-hooks) — the compiled
Claude Code enforcement hooks for the cadence plugin ecosystem.

## Install

```powershell
scoop bucket add cameronsjo https://github.com/cameronsjo/scoop-bucket
scoop install cameronsjo/cadence-hooks
```

Then verify:

```powershell
cadence-hooks --version
```

> **Git Bash is required for the hooks to fire.** Cadence's hooks dispatch
> through `.sh` wrappers, and Claude Code runs shell-form hook commands via Git
> Bash on Windows (it falls back to PowerShell, which can't run `.sh`, when Git
> Bash is absent). Install [Git for Windows](https://git-scm.com/download/win)
> and keep `bash` on `PATH`. The binary installs fine without it — the guards
> just won't run.

## Upgrade

```powershell
scoop update cadence-hooks
```

## Maintenance

`bucket/cadence-hooks.json` is kept current automatically by
`.github/workflows/excavator.yml`, which polls the cadence-hooks GitHub releases
every few hours and commits version + hash updates via the manifest's
`checkver`/`autoupdate` fields. No cross-repo secrets are involved — the
excavator pushes to this repo with the default `GITHUB_TOKEN`.

The manifest starts at a placeholder `0.0.0`; the first excavator run after a
Windows release (`cadence-hooks-vX.Y.Z-windows-x86_64.zip`) exists populates the
real version and hash.

## License

[BSL-1.1](LICENSE), matching cadence-hooks.
