# Execution Plans

Use an execution plan for complex features, large refactors, migrations, or any task expected to span multiple sessions or agents.

## Where plans live

- Cross-cutting plans: `plans/`
- App-scoped plans: `apps/<app>/plans/`
- Shipped plans: move to `plans/done/` (or `apps/<app>/plans/done/`)

Never drop `*_PLAN.md` at an app root or inside `src/`.

## What every plan must contain

- **Purpose** — the problem and the desired outcome.
- **Progress** — what is done, what is next, what is blocked.
- **Discoveries** — facts learned during execution that change the plan.
- **Decision log** — choices made, why, and what was rejected.
- **Concrete steps** — sequenced, verifiable steps an agent can pick up cold.
- **Validation** — how to prove each step worked (tests, browser flow, screenshot, log line, fixture).
- **Recovery notes** — what to do if a step fails partway, or if state diverges.

## Conventions

- Filename: `YYYYMMDD-HHMM-short-slug.md` for new plans, or `short-slug.md` if the date is already obvious from context.
- Keep the plan self-contained. An agent should be able to resume from the file alone, without chat history.
- Update the plan in place as work progresses. Do not let the plan drift from reality.
- When shipping, append a final "outcome" entry, then move the file to `plans/done/`.
