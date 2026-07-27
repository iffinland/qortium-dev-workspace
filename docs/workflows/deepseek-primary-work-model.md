# DeepSeek Primary Work Model — Pilot

**Pilot period:** 2026-07-27 through 2026-08-10

## Purpose

Evaluate DeepSeek as the default cost-efficient local implementation agent for
routine Qortium development. ChatGPT remains the cross-project architect, task
planner, GitHub-backed reviewer, and quality gate. Codex becomes an escalation
and independent-review resource for high-risk, failed, or unusually complex
work.

## Roles

### ChatGPT

- cross-project architecture;
- task scoping;
- GitHub-backed source review;
- DeepSeek task creation;
- result and diff review;
- escalation decision;
- pilot evaluation.

### DeepSeek

- default daily local investigator and implementer;
- documentation, testing, builds, diff review, and handoff;
- one narrow task at a time;
- no external mutation without authorization.

### Codex

- high-risk architecture/data-integrity work;
- independent final audit;
- difficult multi-file or repo-wide refactor;
- repeated DeepSeek failure;
- unresolved runtime or platform-contract problem;
- release-critical verification.

## Risk levels

### LEVEL 1 — DeepSeek implementation

Routine bugfixes, documentation, test additions, dependency updates, and
localized code changes with no architecture or data-integrity impact.

Examples:

- fix a null check in a UI component;
- add a unit test for an existing pure function;
- update a dependency and verify the build;
- correct a documentation error;
- add a console log for runtime diagnostics.

### LEVEL 2 — DeepSeek implementation plus mandatory ChatGPT review

Implementation that touches cross-project concerns, modifies shared
interfaces, or requires QDN/Home verification.

Examples:

- add a new bridge action after verifying the Home contract;
- modify a publication payload field after confirming the QDN schema;
- refactor a shared module used by multiple projects;
- implement a new feature that reads but does not mutate identity state.

### LEVEL 3 — Codex implementation or Codex independent audit

High-risk architecture changes, data-integrity boundaries, critical
authentication or authorization logic, release-blocking fixes, and repeated
DeepSeek failures.

Examples:

- change wallet/name binding logic;
- modify moderation trust or migration authority;
- implement deterministic reduction for conflict resolution;
- refactor identity or authentication across the platform;
- audit a release candidate before publication.

## Pilot measurements

- first-attempt completion;
- number of correction rounds;
- scope violations;
- unsupported platform assumptions;
- test/build success;
- runtime/live-validation quality;
- reverted work;
- Codex escalations;
- task duration;
- DeepSeek credit cost;
- Codex credit or weekly-limit usage;
- owner time spent correcting or explaining.

Measure usable, verified development output rather than raw code volume.

## Pilot decision outcomes

At the end of the pilot, choose one:

- `CONTINUE` — DeepSeek remains the default local implementation agent.
- `CONTINUE WITH STRONGER CONTROLS` — Keep the model but add constraints.
- `RESTRICT DEEPSEEK TASK CLASSES` — Limit to specific task classes only.
- `RETURN SELECTED WORK TO CODEX` — Move specific work back to Codex.
- `STOP THE MODEL` — Discontinue DeepSeek as a local implementation agent.

## Workflow summary

```
ChatGPT scopes and reviews
→ DeepSeek investigates and implements locally
→ owner/runtime validation
→ GitHub
→ Codex escalation when required
```
