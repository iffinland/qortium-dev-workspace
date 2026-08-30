# Qortium Development Workflow v2

## Purpose

Define the canonical operating contract for AI-assisted Qortium development.
This document controls task shape, evidence, execution, validation, challenge,
completion, and synchronization. Domain guides define how the contract applies
to architecture, QDN, Home, runtime, release, and maintenance work.

## Use when

Use for every substantial Qortium task after entering through
[`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md) and
classifying the request.

## Core contract

### 1. Compact prompt, referenced context

A task prompt supplies the task-specific delta, not a copy of the governance
repository. It SHOULD contain only:

- one objective and observable exit criterion;
- exact repository and matching project context;
- concrete scope and non-goals;
- task-specific invariants or unusual constraints;
- required evidence and owner-visible acceptance condition;
- explicit authority for commit, push, release, publication, deployment, live
  writes, issue mutation, or destructive action.

The prompt references shared standards, routed guides, and project context.
Agents MUST read those sources rather than expecting generic rules to be
repeated in every prompt.

### 2. One objective at a time

One task/controller has one primary outcome and one exit criterion. Routine
implementation SHOULD normally map to one issue.

Multiple findings MAY share one controller only when they are tightly related,
share the same architecture or domain context, require the same acceptance
evidence, and must be regression-tested together. Unrelated architecture,
runtime, visual, dependency, release, or cleanup outcomes remain separate
tasks. This rule prevents both unbounded “fix everything” prompts and wasteful
micro-prompting.

### 3. Evidence before implementation

Use this sequence:

```text
owner outcome or observed symptom
-> repository and working-tree baseline
-> current authoritative source and project context
-> real production-flow trace
-> first confirmed mismatch or approved design boundary
-> smallest coherent change
-> required validation layers
-> adversarial self-audit
-> remediation of confirmed in-scope BLOCKER/HIGH findings
-> truthful handoff
```

Do not code from a presumed root cause when source or runtime evidence can
distinguish competing explanations. Later stages that were not reached remain
`NOT VERIFIED`.

### 4. Evidence-based disagreement

Agents MUST NOT agree by default. When a requested method conflicts with
current source, measured runtime evidence, approved architecture, safety, data
integrity, or a materially better technical path, the agent MUST:

1. state the relevant verified evidence;
2. explain the consequence of the requested method;
3. recommend the better bounded alternative;
4. identify any genuine owner decision still required.

Disagreement does not authorize scope expansion, destructive action, or
external mutation. The owner retains product and authorization decisions.

### 5. Validation layers are not interchangeable

Plan and report each applicable layer separately:

1. static and automated checks;
2. local runtime or browser interaction;
3. read-only Core/API and live QDN evidence;
4. embedded Qortium Home behavior;
5. deployed live QDN behavior;
6. adversarial agent review;
7. owner product/runtime acceptance.

Typecheck, lint, unit tests, mocked or synthetic integration tests, project
verification, build, local preview, artifact creation, and agent self-report do
not prove embedded Home or deployed QDN compatibility.

### 6. Live and SSH evidence is mandatory when applicable

When acceptance depends on QDN state, metadata, identity, discovery,
persistence, overwrite semantics, publication metadata, transactions,
references, names, wallets, balances, or Core behavior, the agent MUST use the
available read-only Qortium endpoint and SSH tunnel when they are available or
expected to be available.

The endpoint is environment-specific. Current Core source defines mainnet and
testnet/preview defaults separately, and Home/runtime configuration can select
or override the endpoint. Agents MUST determine the intended environment,
inspect current source/configuration, verify actual reachability, and record the
endpoint used. Port `12391` belongs to Qortal in current dual-runtime Home
configuration and MUST NOT be assumed to be a Qortium endpoint.

Use embedded Home when bridge injection, selected account, approval, routing,
display settings, or owner-visible embedded behavior is material. Use the exact
deployed QDN resource when deployment behavior is claimed.

If required live evidence is unavailable, report the missing level and select
the truthful non-completion status. Do not silently downgrade to mocks or source
inspection.

Read-only investigation does not authorize publication, signing, moderation,
transactions, deployment, or other live writes. Those require exact owner
authorization.

### 7. Local canonical authority and GitHub mirror

The current local `qortium-dev-workspace` working tree is the active governance
editing authority. GitHub is the approved durable mirror and collaboration
history. Uncommitted local content MUST be identified as pending review rather
than represented as an already published standard.

Before synchronization:

1. inspect branch, commit, remote relationship, and complete working tree;
2. preserve pre-existing owner changes;
3. validate links, routed references, terminology, and the complete diff;
4. obtain explicit owner authority for commit and push;
5. commit only the approved coherent change;
6. push and verify that the remote commit matches the approved local version.

Agents MUST NOT replace a newer local authority version with an older remote
copy merely to make Git clean.

## Task workflow

### Start

1. Establish exact repository, branch, HEAD, remote, and dirty state.
2. Classify the task.
3. Read the matching project context and routed guides.
4. Identify authoritative Home/Core sources and required validation levels.
5. State objective, exit criterion, scope, non-goals, risks, and permissions.

### Investigate or design

1. Reproduce the observed outcome when applicable.
2. Trace the actual production path.
3. Compare application expectation, bridge response, Core response, QDN state,
   and UI state as required.
4. Separate verified fact, inference, unknown, and owner decision.
5. Challenge unsupported premises and propose the best bounded solution.

### Implement

1. Make the smallest coherent in-scope change.
2. Preserve owner changes and working behavior.
3. Do not silently begin another objective.
4. Keep application and platform changes separate unless the task explicitly
   authorizes both.

### Validate

1. Run project-defined focused and complete checks.
2. Use required real runtime/SSH/Home/QDN evidence.
3. Re-read the exit criterion.
4. Perform an adversarial self-audit.
5. Fix confirmed in-scope BLOCKER/HIGH findings and repeat validation.
6. Review the complete diff and final working tree.

### Handoff

Report:

- exact status and satisfied exit criterion;
- baseline and files changed;
- evidence by validation layer;
- unavailable or failed validation;
- live environment and endpoint actually used;
- owner actions still required;
- commit/push/release/publication/deployment state;
- exact saved report path.

## Stop conditions

Stop with a truthful terminal state when:

- a material product or architecture choice requires the owner;
- required platform behavior cannot be verified and no safe equivalent exists;
- owner changes overlap the intended edit and cannot be preserved safely;
- required live/runtime evidence is unavailable;
- the correct solution needs authority beyond the task;
- continuing would exceed the one-objective scope.

Routine source inspection, safe read-only live checks, defined tests, and
in-scope fixes are not blockers when they are available and authorized.

## Compact controller shape

Use [`../../templates/TASK-CONTROLLER.md`](../../templates/TASK-CONTROLLER.md).
The controller states the delta; this workflow, the session router, domain
guides, project context, and role overlay supply reusable rules.

## Completion criteria

- One objective and exit criterion were explicit.
- Current authority sources and working tree were inspected.
- Unsupported premises were challenged with evidence.
- Required validation layers were completed or truthfully reported missing.
- Mocks/builds were not presented as live proof.
- Applicable read-only live/SSH evidence was used.
- No unrelated objective or unauthorized external mutation occurred.
- Local/remote governance state was reported accurately.

## Related files

- [`../../AGENTS.md`](../../AGENTS.md)
- [`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md)
- [`../../agents/live-qdn-validation.md`](../../agents/live-qdn-validation.md)
- [`../architecture/qortium-dapp-development-standard.md`](../architecture/qortium-dapp-development-standard.md)
- [`../governance/source-of-truth-and-lifecycle.md`](../governance/source-of-truth-and-lifecycle.md)
- [`report-storage-policy.md`](report-storage-policy.md)
