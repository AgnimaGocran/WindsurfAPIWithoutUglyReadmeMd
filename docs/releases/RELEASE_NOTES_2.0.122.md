## v2.0.122 - LSP probe isolation and native bridge canary diagnostics

- Scheduled/dashboard probes with `allowLsStart:false` now stay truly
  resident-only: `fetchUserStatus` and canary probe steps re-check admission
  and reuse only an existing LS instead of racing into a cold `ensureLs()`.
- LS admission status now includes the resident LS `port` and `generation`, so
  probe maintenance can take the LS maintenance token and keep production
  requests mutually exclusive with probe work.
- Dashboard language-server restart now uses `stopLanguageServerAndWait()` before
  starting the default LS, avoiding old/new LS overlap during manual restarts.
- `scripts/native-bridge-smoke.mjs` now reports per-tool-call argument metadata
  and flags `<workspace>` as `redacted_workspace_path`. This makes real canary
  output distinguish protocol evidence from a client-usable local tool path.
- VPS canary notes: Bash native bridge emitted a valid `cascade_native`
  `run_command` call. Read emitted `cascade_native` `view_file` with the expected
  `read_file` allowlist and `view_file` field 10; `read_file:7801` correctly
  added subfield 15. The returned Read argument was the redacted remote workspace
  marker, so Read remains canary-only for local-tool clients.

Verification:

- `node --test test\*.test.js` passes: 1011/1011.
