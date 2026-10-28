# Personal project context

This private template starts with a new repository and no product or implementation decisions. The user's request, repository instructions such as `AGENTS.md` or `CLAUDE.md`, and established contracts take precedence over personal defaults. The installed global instructions (`~/.codex/AGENTS.md` for Codex or `~/.claude/CLAUDE.md` for Claude Code) tell the agent to read this file when present. It is not automatically loaded as an instruction file from the repository root. Both agents use the same project records here.

## Session entry

1. Read `.cstack/PROGRESS.md` for current execution state and `.cstack/PLAN.md` for intended work and approach when relevant. Compare both with Git status and source before treating them as current.
2. Follow their links to the relevant spec/phase plan, feature-map row, feature detail, or verification section. Open completed specs only when the task depends on them.
3. Use `grill-feature` for an ambiguous idea, `run-spec` for defined implementation, `verify-backend` for backend proof, and `handoff-spec` after material work.

## Project decisions that override global defaults

- Product and target users: not decided yet.
- Runtime and framework: not decided yet. If this becomes a Python API and no other requirement is set, prefer Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest.
- Relational database: PostgreSQL is the global default when one is needed; a project decision here may replace it, including migrations and integration tests.
- External services, cloud, authentication, and deployment: not decided yet. Add them only for this project's needs.
- Directory structure: use the layout below unless this project establishes a different contract; record actual run/test commands in VERIFY.md when known.

## Directory and documentation layout

- Start with `backend/`, `docker/`, and `frontend/` at the repo root; put implementation inside the relevant component. An unused directory may stay empty until that component exists.
- Keep private `CONTEXT.md`, `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` in `.cstack/`. Exclude this directory locally from Git in the target repository. Shared project documentation follows the project's own conventions.
- Create a spec only for an actual bounded change after its scope is known. Default to `.cstack/specs/<id>-<slug>/`; follow an established project location and ID scheme when present and record that choice here. Otherwise use the next numeric ID (`001`, `002`, …). Derive the slug from real work; never pre-create a placeholder spec or duplicate an existing record.
- Default file roles are `spec.md` (outcome, scope, decisions, acceptance), `plan.md` (approach, risks, verification), optional `tasks.md` (steps and state), and `result.md` (implemented behavior, code, observed evidence, limits, remaining work). Keep existing names such as `README.md`, `PHASE-*-PLAN.md`, and `PHASE-*-RESULTS.md`; a child/task table in the plan suffices without `tasks.md`. Create files only as their information becomes available.
- A spec may contain multiple phases/slices with stable IDs and their own observable acceptance. Keep one spec and one implementation slice active at a time. Link its detailed scope, plan, and results from the relevant living files below; do not add a specs-root progress README.
- Keep optional private feature detail in `.cstack/docs/features/` and lasting decision notes in `.cstack/docs/adr/`. One spec can cover a change spanning backend, frontend, and Docker; avoid duplicate histories.

## Roles and lifecycle of the living files

- `.cstack/CONTEXT.md`: stable product, stack, architecture, constraints, confirmed decisions, and documentation conventions. Keep current task status in PROGRESS.
- `.cstack/FEATURE_MAP.md`: product journeys, delivery/proof state, entry points, owning code, and related spec/proof links. Draft planned journeys from agreed goals; inspect code and behavior before claiming implemented or verified. Link longer detail in `.cstack/docs/features/`.
- `.cstack/PLAN.md`: intended outcome, scope, acceptance, approach, phase/slice dependencies, risks, and verification plan. Link detailed spec/phase plans; execution status belongs in PROGRESS.
- `.cstack/PROGRESS.md`: current spec/phase/slice, execution status, last completed work, blocker, next action, and plan/results links. Keep a short completed-spec index here, without an event log.
- `.cstack/VERIFY.md`: reusable run/test commands and latest observed proof with environment, limits, and result-report links. Keep exact historical evidence in the existing spec/phase result report.
- Link to the file responsible for each kind of information instead of duplicating execution state. Before shortening or archiving a document, preserve unique decisions, results, and limits in the spec report or ADR. After moving files, check outgoing and incoming relative links, including evidence artifacts. Completed specs are historical; later changes get a new linked spec. Code and tests remain the source of truth; team-relevant decisions belong in shared project artifacts.

## Working agreement

Define one bounded, reviewable spec with an observable outcome and acceptance criteria for substantial work. A direct request to implement a defined change authorizes it. Closing one slice does not close the whole spec; continue already authorized slices without inferring authorization for unrequested work. Small fixes can proceed without creating a spec record when no durable handoff is needed. Prefer a runnable vertical slice, preserve unrelated edits, use disposable or named external targets, and record only checks actually observed.
