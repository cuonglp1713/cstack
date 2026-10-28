# Personal project context

This private template is for a repository that already has code. Reconcile it with existing project instructions before use. The user's request, established contracts, and repository decisions take precedence over personal defaults. The installed global instructions (`~/.codex/AGENTS.md` for Codex or `~/.claude/CLAUDE.md` for Claude Code) tell the agent to read this file when present. It is not automatically loaded as an instruction file from the repository root. Both agents use the same project records here.

## Session entry

1. Read existing repo instructions, then inspect Git status, relevant source, tests, contracts, and project docs for the requested task. Read `.cstack/PROGRESS.md` for current execution state and `.cstack/PLAN.md` for intended work and approach; compare them with current code.
2. Identify the current or remaining change and its observable acceptance criteria. A defined feature or fix can proceed immediately without a full repository inventory or retrospective spec.
3. Follow PROGRESS and PLAN links to relevant spec/phase records, feature-map rows, and verification notes. Mark uninspected areas unknown.
4. Use `grill-feature` for consequential open decisions, `run-spec` for defined implementation, `verify-backend` for backend proof, and `handoff-spec` after material work.

## Existing project contract

- Record confirmed product, stack, architecture, and operational decisions here as personal context when relevant. Keep team-relevant decisions in shared project artifacts. Do not replace an existing choice with a global default.
- Follow the repository's source, test, and documentation layout. Do not create `backend/`, `frontend/`, or `docker/` merely because the new-repo template uses them.
- Keep personal kit notes inside `.cstack/`. Preserve existing repo instructions and documentation; update actual spec records in place for the requested work instead of replacing them with kit templates.
- Follow the project's existing spec location, IDs, and filenames; record that convention here and avoid parallel records. Otherwise create `.cstack/specs/<id>-<slug>/` only for a substantial change after adoption, using the next numeric ID (`001`, `002`, …) and a slug from actual work. For an in-progress feature, describe only remaining scope and known baseline. Do not reconstruct old specs or claim complete coverage.
- Default roles are `spec.md` for outcome/baseline/scope/acceptance, `plan.md` for approach and verification, optional `tasks.md` for ordered work, and `result.md` for observed implementation and proof. Existing `README.md`, `PHASE-*-PLAN.md`, `PHASE-*-RESULTS.md`, and child/task tables fulfill those roles without renaming or duplicate files. Create files only as information is known; never pre-create a placeholder specs directory.
- A spec may contain several phases/slices with stable IDs and observable acceptance; keep one spec and one implementation slice active at a time. Link its detailed scope, plan, and results from the relevant living files below; do not add a specs-root progress README or backfill old records.

## Documentation and verification

- `.cstack/CONTEXT.md` holds stable product, stack, architecture, constraints, confirmed decisions, and documentation conventions. Keep current task status in PROGRESS.
- `.cstack/FEATURE_MAP.md` is a partial map of product journeys, delivery state, entry points, owning code, and related spec/proof links. Separate delivery from verification evidence; leave uninspected areas out.
- `.cstack/PLAN.md` holds intended outcome, scope, acceptance, approach, phase/slice dependencies, risks, verification plan, and detailed plan links. Keep execution status in PROGRESS.
- `.cstack/PROGRESS.md` holds the current spec/phase/slice, execution status, last completed work, blocker, next action, and plan/results links, plus a short completed-spec index. Keep it concise; link to the file responsible for each kind of information instead of copying history.
- `.cstack/VERIFY.md` holds reusable commands and latest observed proof with environment, limits, and result-report links. Exact historical evidence belongs in the existing spec/phase report. Existing tests or CI configuration are discoverable evidence, not a claim that this agent ran them.
- Keep optional longer personal feature details in `.cstack/docs/features/` and lasting decisions in `.cstack/docs/adr/` when warranted. Preserve unique decisions, results, and limits before shortening or archiving a document; after moving it, check outgoing and incoming relative links, including evidence artifacts. Completed specs are historical; later changes get a new linked spec. Closing one slice does not close the whole spec; continue already authorized slices without inferring authorization for unrequested work. Use shared project docs for information the team needs.
- Verify changed behavior with checks appropriate to the repo. Preserve unrelated edits and use disposable or identified external targets.
