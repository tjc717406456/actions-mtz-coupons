## Cursor Cloud specific instructions

### Project overview

This is **actions-mtz-coupons** — a single Node.js CLI tool that auto-claims Meituan food delivery coupons. No backend server, no database, no Docker. See `README.md` for full details.

### Runtime requirements

- Node.js v20 (pinned in `.nvmrc`)
- pnpm v8.15.9 (pinned via `packageManager` in `package.json`; use `corepack enable` to activate)

### Key commands

| Task | Command |
|------|---------|
| Install deps | `pnpm install` (or `pnpm bootstrap` which also enables corepack) |
| Lint | `pnpm lint` |
| Test | `pnpm test` |
| Run locally | `pnpm start:local` (reads `.env` for config) |
| Run (CI mode) | `pnpm start` (reads env vars directly) |

### Non-obvious caveats

- **TOKEN required for most tests**: The test suites in `test/coupons.js`, `test/payload.js`, `test/template.js`, and 3 tests in `test/user.js` require a real Meituan `TOKEN` env var. Without it, they fail with `请配置 TOKEN`. The remaining tests (`test/notify.js`, `test/update.js`, `test/shadow.js`) pass without credentials.
- **No dev server**: This is a one-shot CLI script, not a long-running server. `pnpm start:local` runs the coupon-grabbing flow once and exits.
- **WASM dependency**: The project uses `@wasmer/wasi` for request signing (shadow guard). This works out of the box on Node.js 20 — no extra native dependencies needed.
- **ESM modules**: The project uses `"type": "module"` — all source files are ES modules.
