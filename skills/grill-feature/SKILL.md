---
name: grill-feature
description: Turn an ambiguous product or engineering idea into clear decisions and a small implementable phase. Use for vague features, architecture choices, or new projects, including work in an existing repo; skip when scope and acceptance criteria are already clear.
---

# Clarify the idea

1. Read the user's idea and relevant `AGENTS.md`, `PLAN.md`, code, tests, contracts, or product notes. In an existing repo, inspect the current behavior and any work in progress around the requested feature; do not require a full repository inventory. State the outcome you think they want. Do not ask questions already answered by these sources.
2. Ask consequential questions in small rounds. Cover users and success, boundaries, key data, failure behavior, security, deployment constraints, and observable acceptance only where each can change the next decision. Later questions should build on earlier answers.
3. Mark each point as decided, inferred, or unknown. If a choice cannot be settled by discussion, propose the smallest prototype or research check that would settle it; avoid endless hypothetical questions.
4. End when the next slice can be implemented without hidden assumptions. Summarize decisions, remaining uncertainty, and a phase-sized outcome with acceptance criteria. The user owns product scope.
5. If the repo has `PLAN.md`, update it with the agreed slice when asked to make the plan durable. For an existing repo, scope the current or remaining work without assigning phase IDs to old history. A clear request to build that slice authorizes implementation; otherwise keep the plan proposed.
6. If the repo has `FEATURE_MAP.md`, update only relevant journeys. Mark a new unbuilt journey as planned when useful; inspect existing code before recording an implemented or `in_progress` path, and do not claim verification without observed proof. Leave uninspected features unmapped.

This is an inquiry workflow inspired by Matt Pocock's `grill-me`, adapted for codebases and phase planning. Do not turn it into a fixed questionnaire.
