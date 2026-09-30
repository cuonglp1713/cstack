# Personal project context

This private template starts with a new repository and no product or implementation decisions. The user's request, repository `AGENTS.md`, and established contracts take precedence over personal defaults. The global `~/.codex/AGENTS.md` points the agent here; Codex does not load this file automatically from the repository root.

## Session entry

1. Read the short current state in `.cstack/PROGRESS.md` and `.cstack/PLAN.md` when relevant. Compare both with Git status and source before treating them as current.
2. Read only the active spec and the relevant `.cstack/FEATURE_MAP.md` row, feature detail, or `.cstack/VERIFY.md` section. Open completed specs only when the task depends on them.
3. Use `grill-feature` for an ambiguous idea, `run-spec` for defined implementation, `verify-backend` for backend proof, and `handoff-spec` after material work.

## Project decisions that override global defaults

- Product and target users: not decided yet.
- Runtime and framework: not decided yet. If this becomes a Python API and no other requirement is set, prefer Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest.
- Relational database: PostgreSQL is the global default when one is needed; a project decision here may replace it, including migrations and integration tests.
- External services, cloud, authentication, and deployment: not decided yet. Add them only for this project's needs.
- Directory structure and commands: use the layout below unless this project establishes a different contract; record actual run/test commands when known.

## Directory and documentation layout

- Start with `backend/`, `docker/`, and `frontend/` at the repo root; put implementation inside the relevant component. An unused directory may stay empty until that component exists.
- Keep private `CONTEXT.md`, `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` in `.cstack/`. Exclude this directory locally from Git in the target repository. Shared project documentation follows the project's own conventions.
- Create `.cstack/specs/<id>-<slug>/` only for an actual bounded change after its scope is known. Use the next numeric ID (`001`, `002`, …), or follow an established project ID scheme. Choose the slug from that project's real task or feature name and naming convention; never pre-create a placeholder spec.
- Each spec folder contains `spec.md` (outcome, scope, decisions, acceptance), `plan.md` (implementation approach, risks, verification plan), `tasks.md` (ordered steps and state), and `result.md` (implemented behavior, changed code, observed evidence, limits, remaining work). Create these files as their information becomes available; do not fill them with invented content. Use local task IDs such as `T01` in `tasks.md` when tracking steps helps.
- Keep optional private feature detail in `.cstack/docs/features/` and lasting decision notes in `.cstack/docs/adr/`. One spec can cover a change spanning backend, frontend, and Docker; avoid duplicate histories.

## Roles and lifecycle of the living files

- `.cstack/PLAN.md`: the current proposed or active change, its next action, and a link to the active spec. The per-spec `plan.md` holds the detailed approach.
- `.cstack/PROGRESS.md`: current status, blocker, next action, and a short index linking completed specs. It is not an event log.
- `.cstack/VERIFY.md`: reusable run/test commands and latest relevant proof summary. The spec's `result.md` stores exact historical command, environment, observed result, and limitation.
- `.cstack/FEATURE_MAP.md`: this repo's user journeys and their observed delivery/proof state. Draft planned journeys from agreed goals; inspect code and behavior before claiming implemented or verified. Keep it a short index and link longer detail in `.cstack/docs/features/`.
- Before shortening a living file, move unique decisions, results, and limitations into the spec record or ADR and leave a pointer. Completed specs are historical records. A later change gets a new spec linked to the earlier one. Code and tests remain the source of truth for actual behavior; team-relevant decisions belong in shared project artifacts.

## Working agreement

Define one bounded, reviewable spec with an observable outcome and acceptance criteria for substantial work. A direct request to implement a defined change authorizes it; do not silently begin unrelated work. Small fixes can proceed without creating a spec record when no durable handoff is needed. Prefer a runnable vertical slice, preserve unrelated edits, use disposable or named external targets, and record only checks actually observed.
