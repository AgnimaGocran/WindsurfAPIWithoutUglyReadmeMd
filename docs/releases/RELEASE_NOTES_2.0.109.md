## v2.0.109 - native bridge allowlist matrix switch

This release adds a narrowly scoped reverse-engineering switch for native bridge experiments:

- Added `WINDSURFAPI_NATIVE_TOOL_BRIDGE_ALLOWLIST_NAMES`, which can override the Cascade allowlist name sent for a mapped tool, for example `Read:read_file,Grep:grep_v2,Glob:list_dir`.
- Default behavior is unchanged: `Read -> view_file`, `Bash -> run_command`, `Grep -> grep_search_v2`, and `Glob -> find`.
- The switch is intended for grey-box protocol matrix tests only. It does not enable native bridge by itself and does not change the production default, which remains off unless explicitly gated by model/route/API key/account settings.

Why this exists:

- Real smoke testing on v2.0.108 showed `Bash` can produce a provider-native tool call and finish cleanly.
- The same run showed `Read`, `Grep`, and `Glob` often return natural language instead of native tool steps under the current Cascade allowlist names.
- This switch lets operators test upstream-recognized tool names without changing caller tool schemas or falling back to prompt emulation.
