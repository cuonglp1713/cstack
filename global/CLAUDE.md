# Global defaults for Claude Code

These are preferences when the user and the current repository have not made a different choice. Repository instructions such as `CLAUDE.md` or an existing `AGENTS.md`, the explicit task request, and established contracts take precedence over these defaults. Check the current repo before applying a preference.

If the repository root contains `.cstack/CONTEXT.md`, read it as personal project context for the task, then read the relevant parts of `.cstack/PLAN.md` and `.cstack/PROGRESS.md` when needed. These private files are not a replacement for repository instructions or source code. This file is installed at `~/.claude/CLAUDE.md`; do not assume Claude Code automatically loads `.cstack/CONTEXT.md` as an instruction file when launched at the repo root.

For tracked spec work, use the short `README.md` at the chosen specs root (`.cstack/specs/README.md` by default, or the project's existing `specs/README.md`) to locate the current work. Follow its links rather than reading every historical report.

## Working style

- Start from the user outcome. For an ambiguous idea, ask focused questions that change product scope or architecture; avoid asking for facts visible in the repo. Capture agreed decisions before designing a large implementation.
- For substantial tracked work, use one bounded spec with a stable ID, observable acceptance criteria, and a clear next action. A spec may contain multiple phases/slices; keep one active spec and one implementation slice at a time, with stable slice IDs and observable acceptance. A direct request to implement a defined change authorizes that work; do not demand repeat permission for routine steps or silently begin an unrelated spec or an unrequested slice. Small focused fixes can proceed without a spec record when no durable handoff is needed.
- Create a spec record only after a real change is scoped. Follow the project's existing location and naming convention; otherwise use `.cstack/specs/<id>-<slug>/` for private kit records. Use the next stable numeric ID (such as `001`) unless the project already has an ID convention; derive the slug from its actual work. Default roles are `spec.md` for outcome and acceptance, `plan.md` for approach and verification, optional `tasks.md` for steps, and `result.md` for observed implementation and proof. Existing `README.md`, `PHASE-*-PLAN.md`, `PHASE-*-RESULTS.md`, and child/task tables can fulfill those roles. Preserve them instead of renaming files or creating duplicate records. Never pre-create an empty specs directory or assign specs retroactively to existing features.
- Create or update the short specs-root `README.md` when actual tracked work begins. Keep current work, status, active or waiting slice, next action, and links to the relevant plan/results there; do not invent results or reconstruct all old specs. Keep detailed design and evidence in the linked records, and use pointers from other living documents to avoid duplicate histories.
- Prefer a runnable vertical slice with observable behavior. Run tests appropriate to the change and report exact results and limits. Keep `PLAN`, `PROGRESS`, `VERIFY`, and `FEATURE_MAP` concise when the repo uses them. Preserve unique decisions, results, and limits before shortening or archiving documents; after moving files, verify outgoing and incoming relative links, including evidence artifacts. Completed specs are historical; later changes get a new linked spec. Closing a slice does not close the whole spec. Continue already authorized slices; do not infer authorization for unrequested work from a completed slice.
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
