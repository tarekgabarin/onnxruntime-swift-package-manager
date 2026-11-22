# onnxruntime-swift-package-manager (mirror)

A byte-exact mirror of Microsoft's removed `microsoft/onnxruntime-swift-package-manager`
at tag 1.24.2 (`b7fb7f7`), with the binary targets re-hosted on this repo. Used by the
BenkyoReader iOS app's SPM dependency.

## Why this exists

On 2026-11-17, Microsoft pulled `microsoft/onnxruntime` (and its
`onnxruntime-swift-package-manager` repo) off GitHub — reportedly over a software
supply-chain attack. The Swift package's binary targets were never in the repo: they
download from `download.onnxruntime.ai`, which died with the org. So **no fork of the
repo can build by itself** — every fork's `Package.swift` points at the same dead
domain.

This repo is the self-hosted copy:

- `main` and tag `1.24.2` point at the re-hosting commit: upstream's 1.24.2 content
  with the two `binaryTarget` URLs in `Package.swift` rewritten to the
  [`binaries-1.24.2` release](../../releases/tag/binaries-1.24.2) here (new SHA256
  checksums recorded; the zips were re-made from SPM's own resolved artifacts).
- Everything else — the Swift bindings, the layout — is upstream 1.24.2 unchanged.

## The rules

- **Dependents must not repoint at `microsoft/onnxruntime*`** — not even when
  upstream returns. A repo returning after a supply-chain incident needs a reviewed
  phase, not a URL edit.
- **Updating:** push the new upstream tag here, re-host its binaries in a new release
  on this repo, and point `Package.swift` at it with the new checksums.
