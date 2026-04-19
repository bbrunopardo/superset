# Product Spec

Source of truth for product scope. Pair with `quality/QUALITY.md` (acceptance criteria + invariants) and `state/features.json` (live status).

## Project

Superset is a code editor for AI agents. It orchestrates CLI-based coding agents (Claude Code, Codex, and others) across isolated git worktrees, with a built-in terminal, diff viewer, and editor handoff.

## Target users

Developers who run multiple coding agents in parallel and need to monitor, review, and integrate their output without context switching across terminals and editors.

## Surfaces

- **Web** (`apps/web`) — primary product UI at app.superset.sh.
- **Desktop** (`apps/desktop`) — Electron build for local worktree-based development.
- **Marketing** (`apps/marketing`) — superset.sh.
- **Admin** (`apps/admin`) — internal admin dashboard.
- **API** (`apps/api`) — backend.
- **Docs** (`apps/docs`) — public documentation.
- **Mobile** (`apps/mobile`) — Expo app.

## In scope (current focus)

The two priority flows below are the active focus. They drive the harness's quality bar and execution plans for now.

### Flow 1 — Ontology proposal lifecycle

An agent iterates on the ontology. Those iterations are bundled into a **proposal**. A reviewer opens the proposal, gets enough information from it to judge the change, and validates and accepts it. After acceptance, the changes apply to the ontology.

Open questions to resolve in a follow-up plan in `plans/`:
- Where does the proposal artifact live (DB table? file? branch?).
- What is the minimum information the proposal must surface for a reviewer (diff, justification, downstream impact, test evidence).
- Who can validate, and what does "accept" mechanically do.
- How are rejected proposals stored and revisited.

### Flow 2 — Context-graph visualization for multi-step agent runs

An agent runs through a multi-step process. Each step touches different governance rules and different parts of the context graph. The user wants to **see, visually, which parts of the context graph were involved in each step**, so it is clear what informed each decision.

Open questions to resolve in a follow-up plan in `plans/`:
- What is the canonical representation of a "context graph" in this repo (nodes, edges, governance metadata).
- What does an agent emit per step so we can map it back to the graph (event log? span? structured trace?).
- What is the visualization surface — embedded in the desktop app, web app, or a separate viewer.
- What reference material informs the design (the user mentioned having one — link from `docs/decisions/` once added).

## Out of scope (for now)

- New agent-orchestration features unrelated to the two flows above.
- New surfaces beyond the seven existing apps.
- Backwards-compatibility shims for any pre-harness conventions.

## Known gaps

- The full set of critical user journeys is much larger than the two priority flows. Additional journeys, acceptance criteria, and tests must be added to `quality/QUALITY.md` as work expands beyond the priority flows. Treat the spec as a living document.
