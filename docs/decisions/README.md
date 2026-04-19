# Decisions

Architecture and product decisions live here as ADRs (architecture decision records).

## When to add one

- A choice changes how the system is built or how teams work.
- A choice locks out other plausible options and a future reader will ask "why this?".
- A constraint comes from outside the repo (legal, compliance, vendor, deadline) and shapes implementation.

## Format

One file per decision: `NNNN-short-slug.md`. Numbers are zero-padded and monotonically increasing.

Each ADR contains:

- **Status** — proposed | accepted | superseded by NNNN | deprecated.
- **Context** — what forced the decision.
- **Decision** — what was chosen, in plain language.
- **Consequences** — what becomes easier and what becomes harder.
- **Alternatives** — what was rejected and why.
