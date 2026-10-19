# Naiwa Post Office — Signed Update Distribution

**Public distribution only. Application source code and account data are private and are not hosted here.**

This repository will host cryptographically signed **V6.2 closed-Beta** app updates for macOS Apple Silicon and Windows x64. It is not the application backend.

## Current status

**Not live. No downloadable app update or `beta/latest.json` has been published.** Please do not link or advertise an update until both signed platform artifacts, their signatures, and an end-to-end installation test are verified.

## Future file layout

```text
beta/
  latest.json          # Add ONLY when a verified two-platform update is ready
```

Installer/updater assets will be attached to version-tagged public GitHub Releases (e.g. `v0.6.2-beta.3`). The `latest.json` will point to those immutable, signed release assets; it must never point to a draft release, a private repository, or an arbitrary URL.

## Release safety checklist

1. Generate and back up the **Tauri updater private key** on a trusted developer machine. Never upload the private key, its password, cloud credentials, or user data to this repository.
2. Embed the corresponding **public key** in the new signed Beta bootstrap installers. This is separate from Windows Authenticode and macOS Developer ID/notarization.
3. Build Windows x64 and macOS ARM64 updater bundles using the same app version; collect the genuine `.sig` files and verify signing against the embedded public key.
4. Upload fully tested updater assets to one public version-tagged release. Validate their download URLs and hashes.
5. **Publish `beta/latest.json` last**, and only after the owner approves the rollout. The manifest version must be newer than the bootstrap version, with both `windows-x86_64` and `darwin-aarch64` entries.
6. Test updater install, interrupted downloads, rejected invalid signatures, retained local credentials and rollback plan on disposable test accounts. Monitor launch health before expanding the Beta audience.

## Platform layout

| Platform key | Signed Tauri v2 updater asset | Traditional installer |
| --- | --- | --- |
| `windows-x86_64` | Signed NSIS installer `.exe` plus `.exe.sig` | NSIS `.exe` |
| `darwin-aarch64` | Signed macOS `.app.tar.gz` plus `.sig` | `.dmg` |

The release's manifest is a public **signed artifact index**. The signature is the contents of the generated `.sig` file, not the path to it.

## Separation of concerns

- This public repository hosts only public release binaries, signatures, release notes and manifests.
- App development and private Beta test infrastructure are managed separately.
- **No GitHub Actions deployment or auto-publish is configured here.** No automatic release is started by ordinary commits.

Developer-side setup and security gates are documented in the private source repository's V6.2 finalization Draft PR. Updating this README does **not** activate the updater.
