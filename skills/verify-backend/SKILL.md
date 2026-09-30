---
name: verify-backend
description: Reproduce and verify backend API, worker, data, or provider behavior with runnable checks and observable effects. Use after backend changes or when proof is requested; adapt commands to the repo and never assume a live target exists.
---

# Verify what users and operators can observe

1. Read repo `VERIFY.md` and relevant `FEATURE_MAP.md` row if they exist. Locate actual run/test commands in source, test configuration, CI, or project docs. A newly copied verification template is not evidence of the application's state. Identify whether the target is isolated unit/contract, disposable integration, dev live, or staging.
2. Check the environment before driving it: branch/HEAD, dependencies, configuration presence without exposing secrets, and ownership of any database, service, or port. For an empty repo, define a verification plan; for an existing repo, distinguish previously recorded or configured checks from checks observed during this work.
3. Run the smallest test that proves changed behavior, then broader checks only for a concrete cross-boundary risk or required gate. For an API/worker flow, observe the initiating action, returned state, and relevant side effect such as a database row, event, object, or response.
4. Use existing test clients, CLI probes, or HTTP guides before creating a new harness. For external providers, use an explicitly named target and authorized test data. Do not use reset, migration, credential creation, or deployment merely to manufacture a green signal.
5. Record exact command, environment, result, limitations, and any unrun proof level in the repo's established report location. If none exists, keep concise current proof in `VERIFY.md` when present and create a detailed report only when warranted. Use the owning component's `docs/phases/` when the new-repo starter layout applies. Keep reusable commands and the latest relevant result plus report link in `VERIFY.md` when a report exists. Update the relevant feature-map row if the route or proof path moved. Review the final diff.

A fake adapter test, disposable integration test, and live acceptance have different meanings. Keep their evidence separate.
