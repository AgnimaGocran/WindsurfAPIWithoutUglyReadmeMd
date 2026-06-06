# Audit Docs

Use this folder for dated audits that capture a point-in-time state of the
project. Do not use audit files as release notes; release-specific changes live
under `docs/releases/`.

## Current Audits

- [2026-06-07](AUDIT_2026-06-07.md): current open issue triage, priority order,
  SWE-1.6 special-agent direction, WebSearch/WebFetch direction, and native
  bridge boundary.
- [2026-06-06](AUDIT_2026-06-06.md): release metadata, dashboard pagination,
  native bridge hardening, HTTP ingress, and memory/cache observations.

## Update Rules

- Add a new dated audit when the open issue set, deployment baseline, or
  technical direction materially changes.
- Keep secrets out of audit files. Use counts, hashes, redacted IDs, and links
  to public issues instead of raw account material.
- If an audit changes the current next-step order, also update
  `docs/HANDOFF.md`.
