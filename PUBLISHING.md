# Release promotion

This public repository never builds VCC from source.

A promotion commit updates `promotions/current.json` with the exact successful
private Windows CI run, source commit, version and channel. GitHub Actions then
downloads only that immutable candidate artifact from the private source
repository, re-verifies provenance and hashes, and creates a GitHub Release.

## One-time secret

Repository secret:

`VCC_SOURCE_ARTIFACTS_TOKEN`

Use a fine-grained credential with **read-only access to
`rkhnorkhan-bit/VPS-Control-centre`**, including **Actions: Read**. It does not
need write access to this public repository: publication uses this repository's
own short-lived `GITHUB_TOKEN`.

Never put the token in `promotions/current.json`, source code, Issues, chat or
release notes.

## Promotion policy

- `test` -> GitHub prerelease;
- `stable` -> normal/latest GitHub Release;
- existing release tags are immutable and never overwritten;
- generated binaries remain Release assets, not Git-tracked payloads.
