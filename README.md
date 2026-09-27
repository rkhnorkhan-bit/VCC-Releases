# VPS Control Center — Releases

Public **binary-only** distribution feed for VPS Control Center (VCC).

This repository intentionally does **not** contain the private application source
or builder. Development, tests and release construction happen in the private
canonical source repository. Only reviewed release assets are published here.

## Channels

- **Stable** — normal GitHub Releases.
- **Test / prerelease** — GitHub Releases marked as prerelease.

VCC clients read this repository through the GitHub Releases API. They do not
need access to the private source repository and do not contain a developer
GitHub token.

## Release assets

A VCC application release can contain:

- `VCC-Update-<version>-win-x64.zip` — installed-runtime update package;
- `vcc-release.json` — update metadata (version, channel, architecture,
  package SHA-256/size and source commit);
- a bootstrap/installer asset when needed;
- public release notes.

Future module releases may use separately signed `.vccmodule` packages.

## Safety

Before applying an update, VCC creates and verifies a local FULL backup of the
current runtime and VCC-managed state. SQLite is backed up through the SQLite
backup API. Windows Credential Manager secrets are not exported. UpdateHost
verifies the backup again, applies an exact runtime replacement, waits for the
new VCC readiness marker and restores runtime + managed state on failure.

Release SHA-256 protects integrity but is not a publisher signature. Stable
public distribution will add the approved publisher-signing/provenance layer.

## Source

Source code is private. This repository is not a source mirror and should never
receive source archives, private diagnostics, credentials, keys or CI secrets.
