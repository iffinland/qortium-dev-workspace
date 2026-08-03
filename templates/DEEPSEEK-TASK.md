# DeepSeek Task

Start this task in a fresh DeepSeek conversation. Assign exactly one issue.
Describe the observed symptom and expected behavior; do not instruct DeepSeek
to assume a specific root cause.

## Repository
<!-- Exact repository name and remote. -->

## Local Path
<!-- Exact absolute local path. -->

## Branch and Baseline Commit
<!-- `git status --short --branch` and `git log -1 --oneline` output. -->

## Owner Request or GitHub Issue
<!-- Exact owner request text or issue number and URL. -->

## Observed Live Symptom
<!-- Concrete owner-visible or live-runtime symptom. -->

## Expected Behavior
<!-- Exact behavior the owner should be able to validate. -->

## Primary Task Class
<!-- One from the classification list. -->

## Secondary Task Classes
<!-- Only when technically required. -->

## Project Context
<!-- Matching `projects/<project>.md` file. -->

## Required Global Guides
<!-- Only routed guides from the session-start routing table. -->

## Authoritative Home/Core Sources
<!-- Exact paths and commits for current checked-out Qortium Home and Core. -->

## Verified Starting Facts
<!-- Facts confirmed from source, not assumed. -->

## Required Production-Flow Trace
<!-- UI -> state/service -> bridge -> Core/QDN -> parser -> validation -> reducer -> render. -->

## Required Read-Only Live Investigation
<!-- Core/API, bridge response, QDN resource, transaction/name/wallet/balance evidence, as applicable. -->

## Unknowns and Owner Decisions
<!-- Explicitly record what is unknown and what requires an owner decision. -->

## Objective
<!-- One narrow issue only. -->

## Scope
<!-- Concrete deliverables. -->

## Out of Scope
<!-- Explicitly excluded work. -->

## Acceptance Criteria
<!-- Verifiable criteria, each with an evidence source. -->

## Implementation Constraints
<!-- Non-functional and process constraints. -->

## Required Validation
<!-- Include npm run verify when defined and owner embedded Qortium Home live validation. -->

## Forbidden Actions
<!-- Block commit, push, publication, release, issue closure, and live mutation unless explicitly authorized. -->

## Authorizations

| Action                  | Authorized? | Owner/Agent |
| ----------------------- | ----------- | ----------- |
| Code edits              |             |             |
| Documentation edits     |             |             |
| Tests/build commands    |             |             |
| Commit                  |             |             |
| Push                    |             |             |
| Issue mutation          |             |             |
| Release/publication/deploy |          |             |

Default all external mutations to forbidden unless explicitly authorized.

## Stop and Escalation Conditions
<!-- When to stop work and escalate to ChatGPT or Codex. -->
<!-- If owner/live validation fails once, allow one focused correction in this same session. If it still fails, escalate to Codex. -->

## Report Storage
- Project slug:
- Report type (used in filename):
- Absolute report directory: `/home/iffi/VsCodec-Projects/Qortium/docs/<project-slug>/issues/`
- Expected report filename:
- Report creation authorized: Yes

Default `Report creation authorized` to `Yes` unless the owner explicitly
requests no saved report.

See [`docs/workflows/report-storage-policy.md`](../docs/workflows/report-storage-policy.md).

## Required Final Report
<!-- Use `final-report-and-owner-handoff.md`. -->
