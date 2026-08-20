# Final Report and Owner Handoff

## Purpose

Standardize truthful task status, evidence, limitations, owner actions, and
issue closure readiness.

## Use when

Use before the final response for every substantial implementation, audit,
runtime, live-validation, maintenance, or release task.

## Do not use when

Do not inflate a small answer with irrelevant sections. Do not report
`COMPLETE` when mandatory evidence or owner validation is outstanding.

## Prerequisites

- Final diff and working-tree review.
- Validation outputs.
- Acceptance-criterion review.
- Known live/owner validation state.

## Required inputs

- Baseline commit and initial status.
- Exact files changed.
- Root cause or architecture decision.
- Tests/measurements and environments.
- Security, compatibility, migration, and runtime impact.
- Commit/push/release/publication state.

## Status vocabulary

Project/phase progress follows the canonical standard statuses (`NOT STARTED`,
`IMPLEMENTED`, `LOCAL/AUTOMATED VERIFIED`, `READY FOR OWNER VALIDATION`,
`COMPLETE`). This section defines the final handoff status.

Use exactly one:

- `COMPLETE`
- `COMPLETE WITH DOCUMENTED ADVISORIES`
- `IMPLEMENTED — OWNER LIVE VALIDATION REQUIRED`
- `PARTIALLY COMPLETE`
- `NOT COMPLETE`
- `OWNER DECISION REQUIRED`
- `ENVIRONMENT BLOCKER`
- `PLATFORM DEPLOYMENT REQUIRED`

`COMPLETE` means all mandatory implementation and validation requirements are
satisfied. Advisories are non-blocking. Mandatory live verification always uses
the owner-live-validation status until confirmed. The last three states are
terminal non-completion states, not synonyms for `NOT COMPLETE`.

Do not mark a task `COMPLETE` merely because tests passed, code exists, or a
platform patch exists locally but has not been deployed where runtime proof
requires it. When a task spans multiple components, report each component
separately, for example:

```text
app implementation = ready
platform patch = locally verified
runtime = deployment required
```

## Workflow

1. Re-read the owner request and issue acceptance criteria.
2. Inspect actual implementation, not planned behavior.
3. Run required validation and final Git checks.
4. Separate direct evidence, inference, unavailable evidence, and advisory.
5. Choose status from the vocabulary.
6. State whether the issue can close and why.
7. Save the substantial report to the canonical workspace report location.
8. Give the owner only a concise chat summary, exact remaining actions, and the
   absolute path of the saved report.

## Report fields

For substantial work include, where applicable:

1. final status;
2. exact scope completed;
3. files changed;
4. baseline;
5. root cause or architectural decision;
6. implementation;
7. tests;
8. measurements;
9. security/data-integrity impact;
10. runtime impact;
11. compatibility/migration impact;
12. limitations;
13. automated validation;
14. live validation performed;
15. owner validation still required;
16. unrelated findings;
17. commit/push/tag/release/publication status;
18. issue closure readiness.

Documentation migrations SHOULD also report original inventory, added/rewritten/
merged/removed/archived files, stale-reference search, and link validation.

## Mandatory rules

- MUST NOT hide failed or unavailable validation.
- MUST identify the environment for runtime measurements.
- MUST NOT claim embedded or live behavior from local preview/Core API alone.
- MUST distinguish pre-existing owner files from task changes.
- MUST NOT imply GitHub/QDN actions occurred when they did not.
- Substantial reports MUST be written to the canonical report location defined
  by [`docs/workflows/report-storage-policy.md`](../docs/workflows/report-storage-policy.md).
- Agents MUST NOT use the chat response as the sole storage location for a
  substantial report.
- Agents MUST NOT print the full saved report into chat unless the owner
  explicitly asks to see the full report there.
- The normal chat handoff MUST stay concise and contain only the final status,
  key findings or completed work, validation summary, unresolved blockers or
  owner actions, and the exact absolute path of the saved report.
- Every final report MUST include:

  ```
  Report saved:
  <absolute path>
  ```

  If no report file was created:

  ```
  Report saved:
  Not created — <reason>
  ```

  MUST NOT claim that a report was saved unless the file exists.
  Follow [`docs/workflows/report-storage-policy.md`](../docs/workflows/report-storage-policy.md).

## Validation

Cross-check the report against `git status`, diff, test outputs, issue state,
and live-validation evidence. Ensure all linked local files exist.

## Completion criteria

- Status matches the strongest completed evidence.
- Files, validations, limitations, and owner actions are exact.
- Issue closure recommendation follows its completion requirement.
- A substantial report exists in the canonical workspace report location.
- The chat handoff is concise and points to the saved report instead of
  duplicating it.

## Related files

- [`00-SESSION-START.md`](00-SESSION-START.md)
- [`live-qdn-validation.md`](live-qdn-validation.md)
- [`git-generated-files-and-hygiene.md`](git-generated-files-and-hygiene.md)
- [`../docs/workflows/report-storage-policy.md`](../docs/workflows/report-storage-policy.md)
