# Personal project context — MySQL example

The global `~/.codex/AGENTS.md` points Codex to this private file; Codex does not load it automatically from the repository root. These confirmed project choices replace conflicting personal defaults. Keep `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` inside `.cstack/`, with detailed personal reports in `.cstack/docs/`.

## Session entry

Read `.cstack/PROGRESS.md` and the current `.cstack/PLAN.md` when relevant, then compare with Git and source. Read the relevant feature-map and verification sections when a task touches that behavior. Use `grill-feature`, `run-phase`, `verify-backend`, and `handoff-phase` when their descriptions apply.

## Project decisions that override global defaults

- Runtime: Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, pytest unless the project requirements choose differently.
- Database: **MySQL 8** for this project. This replaces the global PostgreSQL preference. Migrations, queries, local Compose services, integration tests, and deployment configuration must target MySQL.
- Do not add PostgreSQL-only SQL, extensions, drivers, or test assumptions.
- Product, external services, authentication, and deployment: decide from this project's requirements; do not inherit them from another repo.
- Layout: `backend/`, `docker/`, and `frontend/` at the root; put personal feature details, phase reports, and decision notes under `.cstack/docs/`.

## Working agreement

Use reviewable phase/sub-phase IDs, one active slice, observable acceptance criteria, and accurate verification evidence. A direct request to implement a defined slice authorizes that slice. Preserve unrelated changes and do not silently open another phase.
