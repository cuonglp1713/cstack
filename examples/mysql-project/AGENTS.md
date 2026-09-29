# Project instructions — MySQL example

Codex reads this file after personal `~/.codex/AGENTS.md`. The choices below replace conflicting personal defaults for this repository. Keep `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` at the repository root.

## Session entry

Read `PROGRESS.md` and current `PLAN.md`, then compare with Git and source. Read the relevant feature-map and verification sections when a task touches that behavior. Use `personal-grill-feature`, `personal-run-phase`, `personal-verify-backend`, and `personal-handoff-phase` when their descriptions apply.

## Project decisions that override personal defaults

- Runtime: Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, pytest unless the project requirements choose differently.
- Database: **MySQL 8** for this project. This replaces the personal PostgreSQL preference. Migrations, queries, local Compose services, integration tests, and deployment configuration must target MySQL.
- Do not add PostgreSQL-only SQL, extensions, drivers, or test assumptions.
- Product, external services, authentication, and deployment: decide from this project's requirements; do not inherit them from another repo.

## Working agreement

Use reviewable phase/sub-phase IDs, one active slice, observable acceptance criteria, and accurate verification evidence. A direct request to implement a defined slice authorizes that slice. Preserve unrelated changes and do not silently open another phase.
