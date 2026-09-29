# Project instructions

This repository starts with no product or implementation decisions. Replace the initial state in PLAN/PROGRESS as the idea becomes concrete. Project decisions written here supersede personal defaults from `~/.codex/AGENTS.md`.

## Session entry

1. Read `PROGRESS.md` and the active section of `PLAN.md`. Check `git status`, recent commits, and source before treating a document as current.
2. Read the relevant `FEATURE_MAP.md` row and `VERIFY.md` only when the task touches that behavior. An empty feature map means no user flow has been established yet.
3. For a vague idea, use `grill-feature`; for a defined implementation slice, use `run-phase`; for backend proof, use `verify-backend`; after material work, use `handoff-phase`.

## Project decisions that override personal defaults

- Product and target users: not decided yet.
- Runtime and framework: not decided yet. If this becomes a Python API and no other requirement is set, prefer Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy, Alembic, and pytest.
- Relational database: PostgreSQL is the personal default when one is needed; a project decision here may replace it, including migrations and integration tests.
- External services, cloud, authentication, and deployment: not decided yet. Do not add them just because another project uses them.
- Directory structure and commands: establish from the first runnable slice, then record them here.

## Working agreement

- Define one reviewable phase/sub-phase with an observable outcome, in/out scope, and acceptance criteria. A direct request to implement a defined slice authorizes that slice; do not silently begin an unrelated next phase.
- Prefer a runnable vertical slice. Keep behavior and evidence separate: `PLAN.md` is intent, `PROGRESS.md` is state, `VERIFY.md` is proof, and `FEATURE_MAP.md` is navigation.
- Preserve unrelated edits. Use disposable or named targets for external checks. Do not claim a test or deployment passed unless it was observed.
