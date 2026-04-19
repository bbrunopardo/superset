# Architecture

Bird's-eye view of the Superset monorepo. Pair with `AGENTS.md` (operational rules) and `docs/spec.md` (product scope).

## Codemap

- `apps/web` — main web app (app.superset.sh).
- `apps/marketing` — marketing site (superset.sh).
- `apps/admin` — admin dashboard.
- `apps/api` — backend API.
- `apps/desktop` — Electron desktop app.
- `apps/docs` — documentation site.
- `apps/mobile` — Expo React Native app.
- `packages/ui` — shared shadcn/ui + Tailwind v4 components.
- `packages/db` — Drizzle ORM + Neon Postgres schema.
- `packages/auth` — auth.
- `packages/trpc` — shared tRPC definitions.
- `packages/shared` — cross-app utilities.
- `packages/mcp`, `packages/desktop-mcp` — MCP servers.
- `packages/local-db` — local SQLite.
- `packages/durable-session` — durable session management.
- `packages/email` — email templates and sending.
- `packages/scripts` — CLI tooling.
- `tooling/typescript` — shared tsconfigs.

Build system: Turborepo. Package manager: Bun.

## Boundaries

- Apps may depend on packages. Packages must not depend on apps.
- `packages/ui` is presentation-only — no DB, no auth, no app-specific logic.
- `packages/db` owns the schema. Other packages and apps consume it via Drizzle, never by reaching into `packages/db/drizzle/` artifacts.
- `packages/trpc` is the shared API contract. Apps consume it; it does not import from any app.
- Shared MCP definitions live in `.mcp.json`. Per-tool configs (`.cursor/mcp.json`, `.codex/config.toml`, `opencode.json`) mirror the same set.
- Slash command source of truth is `.agents/commands/`. `.claude/commands` and `.cursor/commands` are symlinks.

## Invariants

- Inputs from the network or filesystem are parsed at the boundary and never trusted as raw JSON.
- Type safety: avoid `any` unless necessary; treat `any` as a smell that needs justification.
- Next.js 16: request interception lives in `proxy.ts`. Never create `middleware.ts`.
- Drizzle migrations are auto-generated. Never hand-edit `packages/db/drizzle/` (`.sql`, `meta/_journal.json`, snapshots).
- Project structure follows the co-location rules in `AGENTS.md` (`Component/Component.tsx` + `index.ts`; co-locate tests, hooks, utils by usage scope).
- shadcn primitives in `src/components/ui/` and `src/components/ai-elements/` use kebab-case single files — this is intentional and required by the shadcn CLI.
- Implementation plans live in `plans/` (cross-cutting) or `apps/<app>/plans/` (app-scoped). Shipped plans move to `plans/done/`.
- Architecture/reference docs live in `<app>/docs/` (app-scoped) or `docs/` (cross-cutting). Never `*_PLAN.md` at an app root or inside `src/`.
