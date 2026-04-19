# Checks

Mechanical guardrails that enforce the invariants in `ARCHITECTURE.md` and `quality/QUALITY.md`.

This directory currently scaffolds the **intent**. Scripts will be added incrementally; nothing here runs yet.

## Planned guardrails

Tracked here so the goal of mechanical enforcement is documented even before code lands.

### Architecture boundaries
- **No app-to-app imports.** `apps/*` may not import from another `apps/*`.
- **Packages must not depend on apps.** `packages/*` may not import from `apps/*`.
- **`packages/ui` is presentation-only.** No imports from `packages/db`, `packages/auth`, `packages/trpc`, or any app.
- **`packages/db` schema isolation.** Consumers go through Drizzle; nothing imports from `packages/db/drizzle/` (the generated artifacts).

### Project structure
- **Co-location compliance.** New components follow `Component/Component.tsx` + `index.ts`; tests sit next to source. Exception: shadcn primitives in `src/components/ui/` and `src/components/ai-elements/` (kebab-case single files, intentional).
- **No `*_PLAN.md` at app roots or inside `src/`.** Plans live in `plans/` or `apps/<app>/plans/`.
- **No `middleware.ts` in Next.js 16 apps.** Use `proxy.ts`.

### Drizzle hygiene
- **`packages/db/drizzle/` is read-only to humans and agents.** Any diff in this directory must come from `bunx drizzle-kit generate`.

### MCP / agent config consistency
- **Single MCP source of truth.** `.mcp.json` is canonical. `.cursor/mcp.json` must be a symlink. `.codex/config.toml` and `opencode.json` must list the same MCP set.
- **Single command source of truth.** Slash commands live in `.agents/commands/`. `.claude/commands` and `.cursor/commands` must be symlinks.

### Runbook smoke
- **Init runbook is executable.** A check should `bun install`, `bun run typecheck`, and `bun run lint` from a clean clone and fail loudly if any step regresses.

## Adding a check

When adding a script here:

1. Make it idempotent and runnable locally and in CI.
2. Have it exit non-zero on failure with a single-line, human-readable explanation.
3. Wire it into `package.json` scripts so `bun run check:<name>` works.
4. Document what invariant it enforces, in this file, with a link to the source rule.
