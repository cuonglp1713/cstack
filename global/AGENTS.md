# Personal defaults for my coding agents

These are preferences when the user and the current repository have not made a different choice. A repository's `AGENTS.md`, explicit task request, and established contract take precedence over these defaults. Check the current repo before applying a preference.

## Working style

- Start from the user outcome. For an ambiguous idea, ask focused questions that change product scope or architecture; avoid asking for facts visible in the repo. Capture agreed decisions before designing a large implementation.
- Split substantial work into reviewable phases and child slices with stable IDs such as `P-00.1`. Keep one active slice, explicit acceptance criteria, and a clear next action. A direct request to implement a defined slice authorizes that work; do not demand repeat permission for routine steps. Do not silently open a new, unrequested phase.
- Prefer a runnable vertical slice with observable behavior. Run tests appropriate to the change and report exact results and limits. Keep PLAN, PROGRESS, VERIFY, and FEATURE_MAP concise when the repo uses them.
- Preserve unrelated worktree changes. Distinguish source behavior, decisions, test evidence, and unverified assumptions. Do not claim deployment or live validation from local tests.

## Preferred stack when a project has not chosen otherwise

- Python 3.12+, `uv`, FastAPI, Pydantic, SQLAlchemy 2, Alembic, and pytest for a Python API.
- PostgreSQL when a relational database is needed. A repo decision such as MySQL replaces this preference completely, including migration and test targets.
- Celery with Redis for durable background work when simple in-process execution is insufficient. Object storage such as S3 only when the product needs it. Add Azure AI, Qdrant, or other providers only for a concrete capability.
- For a FastAPI backend, prefer thin routers, typed schemas, domain-grouped services, models/DB infrastructure, and separate task/worker entry points. Follow an existing repo structure instead of rearranging it merely to match this preference.

## Boundaries

- Do not assume a frontend, cloud provider, vector store, or AI model exists in a new repo. Establish the need and the project's actual interfaces first.
- Use disposable or explicitly identified services for integration checks. Do not run reset, backfill, destructive cleanup, credential issuance, or deployment as routine verification. Keep secrets and sensitive content out of logs and handoff files.
