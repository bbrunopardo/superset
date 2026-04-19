# Progress

Append-only log of meaningful project events. Newest entry on top. Only record verified facts.

---

## 2026-04-19 — Harness scaffolded

Adopted the agent-first project harness from `bbrunopardo/structure` at the monorepo root.

Added:
- `ARCHITECTURE.md` — codemap, boundaries, invariants.
- `PLANS.md` — execution plan rules (kept existing `plans/` + `plans/done/` convention).
- `docs/spec.md` — product scope, with two priority flows captured.
- `docs/decisions/README.md` — ADR format.
- `quality/QUALITY.md` — acceptance criteria for the two priority flows + engineering invariants.
- `state/features.json` — live feature status.
- `state/progress.md` — this file.
- `runbooks/init.md` — install/run/test/reset commands.
- `checks/README.md` — list of planned mechanical guardrails (no scripts yet).

Also added a "First reads" section to the existing `AGENTS.md` pointing to the new files. All previous `AGENTS.md` content preserved.

Two priority flows are recorded as `not-started` in `state/features.json`. Next step: open a plan in `plans/` for whichever flow is picked up first.
