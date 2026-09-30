# Personal project context

This private template is for a repository that already has code. Reconcile it with existing project instructions before use. The user's request, established contracts, and repository decisions take precedence over personal defaults. The global `~/.codex/AGENTS.md` points the agent here; Codex does not load this file automatically from the repository root.

## Session entry

1. Read existing repo instructions, then inspect Git status, relevant source, tests, contracts, and project docs for the requested task. Treat `.cstack/PLAN.md` and `.cstack/PROGRESS.md` as navigation aids; compare them with current code.
2. Identify the current or remaining change and its observable acceptance criteria. A defined feature or fix can proceed immediately without a full repository inventory or retrospective spec.
3. Read only the relevant feature-map row, verification notes, and past spec records when they exist. Mark uninspected areas unknown.
4. Use `grill-feature` for consequential open decisions, `run-spec` for defined implementation, `verify-backend` for backend proof, and `handoff-spec` after material work.

## Existing project contract

- Record confirmed product, stack, architecture, and operational decisions here as personal context when relevant. Keep team-relevant decisions in shared project artifacts. Do not replace an existing choice with a global default.
- Follow the repository's source, test, and documentation layout. Do not create `backend/`, `frontend/`, or `docker/` merely because the new-repo template uses them.
- Keep personal kit notes inside `.cstack/`. Leave root `AGENTS.md`, plans, verification guides, and other team documents intact; consult them as project evidence.
- Create `.cstack/specs/<id>-<slug>/` only for a substantial change being worked on after adoption. Use the next numeric ID (`001`, `002`, …) unless the project has an established ID scheme; derive the slug from its actual task and naming rules. For an already in-progress feature, describe only the remaining scope and known baseline. Do not reconstruct old specs or claim complete feature coverage.
- Inside that folder, use `spec.md` for outcome/current baseline/scope/acceptance, `plan.md` for implementation and verification approach, `tasks.md` for ordered work (local IDs such as `T01` when useful), and `result.md` for observed implementation and proof. Create files as the information is known; never pre-create a placeholder `specs/` directory.

## Documentation and verification

- `.cstack/PLAN.md` points to the current spec or focused task and its next action. Per-spec `plan.md` holds the details. `.cstack/PROGRESS.md` records current state and links completed specs; neither is a history of all prior development.
- `.cstack/VERIFY.md` holds reusable commands and recent observed proof; exact historical evidence for tracked work belongs in `result.md`. Existing tests or CI configuration are discoverable evidence, not a claim that this agent ran them.
- `.cstack/FEATURE_MAP.md` is a partial index of user journeys discovered while working. Record delivery state separately from verification evidence; leave uninspected areas out of the map.
- Keep optional longer personal feature details in `.cstack/docs/features/` and lasting decisions in `.cstack/docs/adr/` when warranted. Preserve unique evidence before shortening an index. Completed specs are historical; later changes get a new linked spec. Use shared project docs for information the team needs.
- Verify changed behavior with checks appropriate to the repo. Preserve unrelated edits and use disposable or identified external targets.
