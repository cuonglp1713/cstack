---
name: grill-feature
description: Turn an ambiguous product or engineering idea into clear decisions and a bounded implementable spec. Use for vague features, architecture choices, or new projects; skip when scope and acceptance criteria are already clear.
---

# Clarify the idea

1. Read the user's idea, repository instructions, relevant `.cstack/CONTEXT.md` and `.cstack/PLAN.md` when present, code, tests, contracts, or product notes. If the private kit is absent, use the repo's own planning documents. In an existing repo, inspect current behavior and work in progress around the requested change; do not require a full repository inventory. State the outcome you think they want. Do not ask questions already answered by these sources.
2. Ask consequential questions in small rounds. Cover users and success, boundaries, key data, failure behavior, security, deployment constraints, and observable acceptance only where each can change the next decision. Later questions should build on earlier answers.
3. Mark each point as decided, inferred, or unknown. If a choice cannot be settled by discussion, propose the smallest prototype or research check that would settle it; avoid endless hypothetical questions.
4. End when one bounded change can be implemented without hidden assumptions. Summarize decisions, remaining uncertainty, and acceptance criteria. The user owns product scope.
5. When asked to make the plan durable and the private kit is present, create an actual `.cstack/specs/<id>-<slug>/` for the agreed change, following `.cstack/CONTEXT.md`. Derive the slug from the project's own task or feature name; do not create `specs/` before work is defined. Write `spec.md` with the outcome, boundaries, decisions, and observable acceptance; write `plan.md` and `tasks.md` once approach and steps are known. Point `.cstack/PLAN.md` and `.cstack/PROGRESS.md` at this spec. In an existing repo, document current or remaining work without backfilling old features. If the kit is absent, follow the repo's planning convention.
6. If `.cstack/FEATURE_MAP.md` exists, update only relevant journeys. Mark a new unbuilt journey as planned when useful; inspect existing code before recording an implemented or in-progress path, and do not claim verification without observed proof. Leave uninspected features unmapped.

This is an inquiry workflow inspired by Matt Pocock's `grill-me`, adapted for codebases and spec planning. Do not turn it into a fixed questionnaire.
