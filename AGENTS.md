# AGENTS.md

## Cursor Cloud specific instructions

### Project overview

This is a Node.js CLI tool (Meituan food delivery coupon auto-claimer) that runs as a GitHub Actions cron job or locally. No external services, databases, or Docker required — it's a pure HTTP client.

### Prerequisites

- Node.js v20 (see `.nvmrc`); use `nvm use 20` when the environment has nvm
- pnpm v8.15.9 via corepack: `corepack enable && corepack pnpm i` (aliased as `pnpm bootstrap`)

### Key commands

See `package.json` scripts. Summary:

| Task | Command |
|---|---|
| Install deps | `pnpm bootstrap` |
| Lint | `pnpm lint` |
| Test | `pnpm test` |
| Run (CI) | `pnpm start` (reads `TOKEN` from env) |
| Run (local) | `pnpm start:local` (reads `.env` via dotenv) |

### Testing caveats

- Most tests in `test/coupons.js`, `test/payload.js`, `test/template.js`, and 3 tests in `test/user.js` require a real Meituan `TOKEN` env var. Without it they throw "请配置 TOKEN" and fail. This is expected.
- Tests that do not need a token (`test/notify.js`, `test/update.js`, `test/shadow.js`, plus token-parsing tests in `test/user.js`) pass without any configuration.

### Running the app

The app needs `TOKEN` as env var. For local development, create a `.env` file with `TOKEN=<your_meituan_token>` and run `pnpm start:local`. See `docs/本地运行.md` for details.
