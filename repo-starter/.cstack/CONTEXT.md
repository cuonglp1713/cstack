# Personal project context

This is a private seed for a new repository with no product or implementation decisions yet. Replace the seed state as the idea becomes concrete. The user's request, repository `AGENTS.md`, and established contracts take precedence over personal defaults. The global `~/.codex/AGENTS.md` points the agent to this file; Codex does not load it automatically from the repository root.

## Session entry

1. Read the short current state in `.cstack/PROGRESS.md` and the active slice in `.cstack/PLAN.md` when the task needs them. Compare both with Git status and source before treating them as current.
2. Read only the relevant `.cstack/FEATURE_MAP.md` row, feature detail, `.cstack/VERIFY.md` section, or archived phase report for the task. Do not load every report at session start.
3. Use `grill-feature` for an ambiguous idea, `run-phase` for a defined implementation slice, `verify-backend` for backend proof, and `handoff-phase` after material work.

## Project decisions that override global defaults

- Product and target users: not decided yet.
- Runtime and framework: not decided yet. If this becomes a Python API and no other requirement is set, prefer Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest.
- Relational database: PostgreSQL is the global default when one is needed; a project decision here may replace it, including migrations and integration tests.
- External services, cloud, authentication, and deployment: not decided yet. Do not add them just because another project uses them.
- Directory structure and commands: use the layout below unless this project establishes a different contract; record actual run/test commands when known.

## Directory and documentation layout

- Start with `backend/`, `docker/`, and `frontend/` at the repo root; put implementation inside the relevant component. An unused directory may stay empty until that component exists.
- Keep personal `CONTEXT.md`, `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` in `.cstack/`. The target repository should exclude this directory locally from Git; shared project documentation follows the project's own conventions.
- Put private feature detail in `.cstack/docs/features/`, phase reports in `.cstack/docs/phases/`, and enduring personal decision notes in `.cstack/docs/adr/`.
- For work spanning backend and frontend, use one phase report and link to it from the living indexes. Docker changes belong in the same report when relevant. Avoid duplicate histories.

## Roles and lifecycle of the Markdown files

- `.cstack/PLAN.md`: only the proposed or active phase/slice, its scope, decisions, and acceptance criteria. Replace the active section when moving to the next slice; preserve completed outcomes in the phase report first.
- `.cstack/PROGRESS.md`: current status, blocker, next action, and a compact index with one row per parent phase linking to its report. Update rows; do not append a full event log or child-slice history here.
- `.cstack/VERIFY.md`: reusable run/test commands and the latest relevant proof summary. Put exact historical commands, environment, observed result, and limitations in the phase report; link from the summary.
- `.cstack/FEATURE_MAP.md`: this repo's user journeys, not a reusable cross-project feature list. The agent may draft it from agreed product goals and inspect code/routes/UI/tests, marking planned versus implemented versus verified. Check real behavior before claiming a journey is verified. Keep it as a short index; move lengthy drive steps and proof to `.cstack/docs/features/<feature>.md` and link the row.
- A phase report records each child ID, delivered behavior, changed code or commit, exact verification and environment, observed outcome, unresolved work, and decision links. Create or update it as child slices finish; finalize it when the parent phase closes. Keep large raw logs out of Markdown and link to CI/artifacts when available. Use an ADR for a lasting architectural choice.
- Before shortening a living file, move every unique result, decision, or limitation into its report or ADR and leave a pointer. Code and tests remain the source of truth for actual behavior. Record team-relevant decisions in shared project artifacts when required.

## Working agreement

- Define one reviewable phase/sub-phase with an observable outcome, in/out scope, and acceptance criteria. A direct request to implement a defined slice authorizes that slice; do not silently begin an unrelated next phase.
- Prefer a runnable vertical slice. Preserve unrelated edits. Use disposable or named targets for external checks. Do not claim a test or deployment passed unless it was observed.
