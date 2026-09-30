# Global defaults for coding agents

These are preferences when the user and the current repository have not made a different choice. A repository's `AGENTS.md`, explicit task request, and established contract take precedence over these defaults. Check the current repo before applying a preference.

If the repository root contains `.cstack/CONTEXT.md`, read it as personal project context for the task, then read the relevant parts of `.cstack/PLAN.md` and `.cstack/PROGRESS.md` when needed. These private files are not a replacement for repository instructions or source code. Do not assume Codex discovers files inside `.cstack/` automatically when launched at the repo root.

## Working style

- Start from the user outcome. For an ambiguous idea, ask focused questions that change product scope or architecture; avoid asking for facts visible in the repo. Capture agreed decisions before designing a large implementation.
- For substantial tracked work, use one bounded spec with a stable ID, observable acceptance criteria, and a clear next action. Keep one active spec at a time. A direct request to implement a defined change authorizes that work; do not demand repeat permission for routine steps or silently begin an unrelated spec. Small focused fixes can proceed without a spec record when no durable handoff is needed.
- When the private kit is installed, create `.cstack/specs/<id>-<slug>/` only after a real change is scoped. Use the next stable numeric ID (such as `001`) unless the project already has an ID convention; derive the slug from that project's actual work and naming rules. Never create an empty `specs/` directory or invent a feature name in advance. Inside an active spec, use `spec.md` for outcome and acceptance, `plan.md` for approach and verification, `tasks.md` for actionable steps, and `result.md` for implementation and observed evidence. Do not assign specs retroactively to existing features.
- Prefer a runnable vertical slice with observable behavior. Run tests appropriate to the change and report exact results and limits. Keep `PLAN`, `PROGRESS`, `VERIFY`, and `FEATURE_MAP` concise when the repo uses them. Link completed spec records from the living files before shortening them. Later changes get a new spec that links the earlier one.
- Preserve unrelated worktree changes. Distinguish source behavior, decisions, test evidence, and unverified assumptions. Do not claim deployment or live validation from local tests. Shared project decisions belong in the repository's established documentation when the team needs them.

## Preferred stack when a project has not chosen otherwise

- Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest for a Python API.
- PostgreSQL when a relational database is needed. A repo decision such as MySQL replaces this preference completely, including migration and test targets.
- Celery with Redis for durable background work when simple in-process execution is insufficient. Object storage such as S3 only when the product needs it. Add Azure AI, Qdrant, or other providers only for a concrete capability.
- For a FastAPI backend, prefer thin routers, typed schemas, domain-grouped services, models/DB infrastructure, and separate task/worker entry points. Follow an existing repo structure instead of rearranging it merely to match this preference.
- For a new repo, use `backend/`, `docker/`, and `frontend/` as top-level application boundaries before adding deeper structure. Keep personal specs, feature details, and decision notes inside `.cstack/`. Follow an existing repo's source and documentation layout when it differs.

## Boundaries

- Do not assume a frontend, cloud provider, vector store, or AI model exists in a new repo. Establish the need and the project's actual interfaces first.
- Use disposable or explicitly identified services for integration checks. Do not run reset, backfill, destructive cleanup, credential issuance, or deployment as routine verification. Keep secrets and sensitive content out of logs and handoff files.
