---
name: verify-backend
description: Reproduce and verify backend API, worker, data, or provider behavior with runnable checks and observable effects. Use after backend changes or when proof is requested; adapt commands to the repo and never assume a live target exists.
---

# Verify what users and operators can observe

1. Read `.cstack/VERIFY.md` for reusable commands and prior proof, `.cstack/PROGRESS.md` for the current spec/slice, and `.cstack/PLAN.md` for acceptance and verification intent when present. Use the relevant FEATURE_MAP row to find the product path, then follow links to existing spec/phase plans such as `PHASE-*-PLAN.md`. Otherwise use the repo's verification documents. Locate actual run/test commands in source, test configuration, CI, or project docs. A copied verification template is not evidence of application state. Identify whether the target is isolated unit/contract, disposable integration, dev live, or staging.
2. Check the environment before driving it: branch/HEAD, dependencies, configuration presence without exposing secrets, and ownership of any database, service, or port. For an empty repo, define a verification plan; for an existing repo, distinguish previously recorded or configured checks from checks observed during this work.
3. Run the smallest test that proves changed behavior, then broader checks only for a concrete cross-boundary risk or required gate. For an API/worker flow, observe the initiating action, returned state, and relevant side effect such as a database row, event, object, or response.
4. Use existing test clients, CLI probes, or HTTP guides before creating a new harness. For external providers, use an explicitly named target and authorized test data. Do not use reset, migration, credential creation, or deployment merely to manufacture a green signal.
5. Record exact command, environment, result, limitations, and any unrun proof level in the active spec/slice's existing result report (`result.md` or `PHASE-*-RESULTS.md`); preserve filenames instead of duplicating reports. When the private kit is present, keep reusable commands and the latest observed proof summary with limits and report links in `.cstack/VERIFY.md`; update `.cstack/PROGRESS.md` only when execution state, blocker, or next action changes. For a focused fix without a spec, record concise evidence in VERIFY or follow the repo's reporting convention. Slice proof does not establish acceptance of the whole spec. Update relevant product proof links in FEATURE_MAP if they moved. Review the final diff.

A fake adapter test, disposable integration test, and live acceptance have different meanings. Keep their evidence separate.
