# Personal project context — MySQL example

The global `~/.codex/AGENTS.md` points Codex to this private file; Codex does not load it automatically from the repository root. These confirmed project choices replace conflicting personal defaults. Keep `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md` inside `.cstack/`. Create a spec record there only when a real change is scoped.

## Session entry

Read `.cstack/PROGRESS.md` and the current `.cstack/PLAN.md` when relevant, then compare with Git and source. Once specs exist, use their root README to locate current work, status, active or waiting slice, next action, and plan/results. Follow existing filenames and child/task tables instead of creating duplicate records. Read relevant feature-map and verification sections. Use `grill-feature`, `run-spec`, `verify-backend`, and `handoff-spec` when their descriptions apply.

## Project decisions that override global defaults

- Runtime: Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, pytest unless the project requirements choose differently.
- Database: **MySQL 8** for this project. This replaces the global PostgreSQL preference. Migrations, queries, local Compose services, integration tests, and deployment configuration must target MySQL.
- Do not add PostgreSQL-only SQL, extensions, drivers, or test assumptions.
- Product, external services, authentication, and deployment: decide from this project's requirements; do not inherit them from another repo.
- Layout: `backend/`, `docker/`, and `frontend/` at the root. Put private spec records in `.cstack/specs/<id>-<project-slug>/` only for defined work, feature details in `.cstack/docs/features/`, and decision notes in `.cstack/docs/adr/`.

## Working agreement

Use one active bounded spec for substantial tracked work, with observable acceptance criteria and accurate verification evidence. A spec can contain multiple phases/slices, with one implementation slice active at a time. A direct request to implement a defined change authorizes it. Completing a slice does not close the whole spec; continue already authorized slices without inferring authorization for unrequested work. Preserve unique information before archiving documents, and check incoming and outgoing relative links after moving files. Preserve unrelated changes.
