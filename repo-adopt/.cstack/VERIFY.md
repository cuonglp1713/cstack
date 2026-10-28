# Verification guide

No check has been recorded in this template. This says nothing about existing tests, CI results, or deployed behavior. Discover actual commands and safe targets before running them.

## Reusable commands

- Build/start: not documented here yet.
- Focused test: not documented here yet.
- Full test/quality gate: not documented here yet.
- External acceptance: not documented here yet; use a named target and safe test data.

## Latest relevant proof

- **Spec or focused task:** none recorded here yet.
- **Environment and command:** not recorded here yet.
- **Observed result and side effect:** not recorded here yet.
- **Limitations:** not assessed here yet.
- **Detailed evidence:** link the existing result report for the active spec/slice when one exists.

For each new change, run the smallest check that demonstrates changed behavior and relevant side effects. Distinguish inspected pre-existing evidence from checks run during this work. Record exact commands, environments, failures, and skipped checks in the existing result report (`result.md` or `PHASE-*-RESULTS.md`) and link it from the specs-root README, or report concisely here for a focused fix. Slice proof does not establish acceptance of the whole spec. Never infer a pass from a test file or CI workflow.
