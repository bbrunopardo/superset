# Init Runbook

How to install, run, test, and reset the project. An agent should never need to guess.

## Prerequisites

- Bun (no npm/yarn/pnpm). Version pinned in `.bun-version`.
- Node toolchain consistent with `package.json` engine hints.
- A populated `.env` (start from `.env.example`).

## Install

```bash
bun install
```

## Run

```bash
bun dev          # all dev servers (Turborepo)
```

Run a single app via Turborepo filters, e.g. `turbo dev --filter=web`.

## Test

```bash
bun test         # full test suite
```

## Code quality

```bash
bun run lint           # check (no changes)
bun run lint:fix       # fix auto-fixable issues
bun run format         # format only
bun run format:check   # CI-style check
bun run typecheck      # type check all packages
```

Biome runs at the root, not per-package. Use `bun run lint:fix` as the one-shot fixer.

## Build

```bash
bun build        # build all packages
```

## Reset

```bash
bun run clean              # clean root node_modules
bun run clean:workspaces   # clean all workspace node_modules
```

After a reset, re-run `bun install`.

## Database (read this before touching data)

- Schema lives in `packages/db/src/schema/`.
- **Never touch the production database unless explicitly asked, and confirm first.**
- For migrations: spin up a new Neon branch, point the root `.env` at it, then change the schema and run `bunx drizzle-kit generate --name="<snake_case_name>"`.
- Never hand-edit `packages/db/drizzle/` files (they are auto-generated).

## Validating a priority flow

Until each priority flow has a dedicated runbook entry, capture validation steps inline in the active plan under `plans/`. Once a flow is shippable, lift the steps into a new `runbooks/<flow>.md` file.
