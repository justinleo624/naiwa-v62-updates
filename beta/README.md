# V6.2 Beta update channel — publication lock

This directory is intentionally missing `latest.json`.

**DO NOT add `latest.json` until:**
- Owner has approved rollout after the final combined Windows/Mac QA.
- Both macOS ARM64 and Windows x64 signed updater artifacts, signature text and immutable public release URLs have been checked.
- A previous signed bootstrap build has been manually installed on a disposable test device, and the higher-version update has been tested end-to-end.
- The current independent Beta backend is backed up and its recovery plan has been verified.

Release files must never contain a Tauri signing private key, password, server AccessKey, user token, phone number or database.

A missing `latest.json` is **intentional** until the first signed update is approved. A README here does not activate any automatic update.
