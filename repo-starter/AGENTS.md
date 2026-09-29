# Project instructions

This repository starts with no product or implementation decisions. Replace the seed state as the idea becomes concrete. Project decisions here supersede global defaults from `~/.codex/AGENTS.md`.

## Session entry

1. Read the short current state in `PROGRESS.md` and the active slice in `PLAN.md`. Compare both with Git status and source before treating them as current.
2. Read only the relevant `FEATURE_MAP.md` row, feature detail, `VERIFY.md` section, or archived phase report for the task. Do not load every report at session start.
3. Use `grill-feature` for an ambiguous idea, `run-phase` for a defined implementation slice, `verify-backend` for backend proof, and `handoff-phase` after material work.

## Project decisions that override global defaults

- Product and target users: not decided yet.
- Runtime and framework: not decided yet. If this becomes a Python API and no other requirement is set, prefer Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest.
- Relational database: PostgreSQL is the global default when one is needed; a project decision here may replace it, including migrations and integration tests.
- External services, cloud, authentication, and deployment: not decided yet. Do not add them just because another project uses them.
- Directory structure and commands: use the layout below unless this project establishes a different contract; record actual run/test commands when known.

## Directory and documentation layout

- Start with `backend/`, `docker/`, and `frontend/` at the repo root; put implementation inside the relevant component. An unused directory may stay empty until that component exists.
- Keep `AGENTS.md`, `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` at the repo root for fast navigation. Do not create a root `docs/` for phase or feature history.
- Put feature detail in `backend/docs/features/` or `frontend/docs/features/`, according to the owning product surface. Put phase reports in the same component's `docs/phases/`; put enduring architecture decisions in its `docs/adr/`.
- For work spanning backend and frontend, choose one owning phase report and link to it from the other component or the root index. Docker changes belong in the report for the component they support. Avoid duplicate histories.

## Roles and lifecycle of the Markdown files

- `PLAN.md`: only the proposed or active phase/slice, its scope, decisions, and acceptance criteria. Replace the active section when moving to the next slice; preserve completed outcomes in the phase report first.
- `PROGRESS.md`: current status, blocker, next action, and a compact index with one row per parent phase linking to its report. Update rows; do not append a full event log or child-slice history here.
- `VERIFY.md`: reusable run/test commands and the latest relevant proof summary. Put exact historical commands, environment, observed result, and limitations in the owning phase report; link from the summary.
- `FEATURE_MAP.md`: this repo's user journeys, not a reusable cross-project feature list. The agent may draft it from agreed product goals and inspect code/routes/UI/tests, marking planned versus implemented versus verified. Check real behavior before claiming a journey is verified. Keep it as a short index; move lengthy drive steps and proof to `backend/docs/features/<feature>.md` or `frontend/docs/features/<feature>.md` and link the row.
- A phase report records each child ID, delivered behavior, changed code or commit, exact verification and environment, observed outcome, unresolved work, and decision links. Create or update it as child slices finish; finalize it when the parent phase closes. Keep large raw logs out of Markdown and link to CI/artifacts when available. Use an ADR for a lasting architectural choice.
- Before shortening a root file, move every unique result, decision, or limitation into its component report or ADR and leave a pointer. Code and tests remain the source of truth for actual behavior.

## Working agreement

- Define one reviewable phase/sub-phase with an observable outcome, in/out scope, and acceptance criteria. A direct request to implement a defined slice authorizes that slice; do not silently begin an unrelated next phase.
- Prefer a runnable vertical slice. Preserve unrelated edits. Use disposable or named targets for external checks. Do not claim a test or deployment passed unless it was observed.
