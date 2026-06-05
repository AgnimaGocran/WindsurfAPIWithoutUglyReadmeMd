## v2.0.104 - native bridge gray smoke

This release tightens the native bridge rollout path and expands the smoke
coverage for real tool-call streams.

### Native bridge gray gate

- The default native bridge tool scope is now limited to the Read / Bash /
  Grep / Glob families and their cascade aliases:
  `Read/read_file/view_file`, `Bash/shell_command/run_command`,
  `Grep/grep_search/grep_search_v2`, and `Glob/find`.
- WebSearch, WebFetch, Write, Edit, and MultiEdit remain mapped internally but
  require an explicit `WINDSURFAPI_NATIVE_TOOL_BRIDGE_TOOLS` allowlist before
  they can enter native mode.
- Existing model, provider, route, caller, API key, and account gates remain in
  place so operators can enable the bridge only for a narrow canary.

### Smoke testing

- `npm run smoke:native-bridge` now supports scenario selection with
  `NATIVE_BRIDGE_SMOKE_TOOLS=Read,Bash,Grep,Glob,mixed,all`.
- Each selected scenario runs non-stream and stream requests by default and
  fails if provider-native `<function_calls>` / `<invoke>` XML leaks to the
  client.
- The smoke still defaults to Bash only, so production canaries can start with
  a cheap single-tool probe before expanding to `all`.
