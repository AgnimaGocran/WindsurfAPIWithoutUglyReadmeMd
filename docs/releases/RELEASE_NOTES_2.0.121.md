## v2.0.121 - LSP admission hardening and native tool_choice guard

This release closes issues found during the engineering audit before expanding
the native bridge matrix.

- LSP start/restart admission is stricter. Default LS starts now share the same
  capacity guard as proxy LS starts, while first-process bootstrap still has a
  narrow memory-guard exception so low-memory installs can boot.
- LS restart paths keep a `_stopping` reservation and wait briefly for the old
  process to exit before spawning the replacement, reducing transient RSS and
  port overlap during dashboard binary updates or restarts.
- Maintenance/probe use is now exclusive: production RPCs refuse registered LS
  instances under maintenance, idle eviction/sweep skip maintenance entries,
  and resident-only probe re-checks admission inside the probe body before any
  `ensureLs()` call.
- Native bridge routing now respects OpenAI `tool_choice` before partitioning:
  `tool_choice:"none"` disables native tools, and forced function choices narrow
  the native allowlist and emitted tool-call filter to that function.

Validation:

- `node --check src/langserver.js src/auth.js src/client.js src/handlers/chat.js`
- `node --test test/*.test.js` passes locally (`1010/1010`).
