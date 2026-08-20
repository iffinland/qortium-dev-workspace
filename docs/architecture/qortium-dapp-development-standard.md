# Qortium dApp Development Standard

## Purpose

This standard defines the reusable development workflow for Qortium dApps. It
captures validated cross-project lessons from Architecture V2 work without
binding future projects to Discussion Boards-specific entities, identifiers, or
implementation details.

## Scope

Use this standard for new Qortium applications, existing dApp audits,
issue-driven refactors, bridge/QDN work, live validation, publication, release,
and agent handoffs.

Project-specific decisions belong in `projects/<project>.md` or the
application repository. This document contains only reusable Qortium rules.

This document is the canonical cross-project standard. Task guides and role
overlays apply it to narrower workflows; if a concise summary conflicts with
this standard, this standard takes precedence.

## 1. Live Qortium Home Validation Is the Final Truth

Passing local and automated checks is necessary but not sufficient. TypeScript,
lint, unit tests, mocked integration tests, `npm run verify`, production build,
and an agent self-report do not prove that a Qortium dApp works in production.

Evidence is produced in three non-interchangeable layers: automated integrity,
adversarial agent audit, and owner product/runtime validation. A green automated
suite does not satisfy the audit or owner-validation layers.

For owner-visible Qortium behavior, use this validation chain:

```text
observed live symptom
-> trace real production flow
-> read-only live-node investigation
-> identify first confirmed broken step
-> minimal fix
-> npm run verify
-> clean deterministic build
-> exact artifact publication
-> embedded Qortium Home live-test
```

An issue that requires embedded or live behavior remains validation-pending
until the project owner confirms the live result against the intended artifact.

## 2. Investigate Live Nodes Read-Only Whenever Practical

When a problem concerns QDN resources, resource discovery, bridge responses,
Core transactions, transaction references, names, wallets, balances, authority,
persistence, publication metadata, or live reload behavior, use the available
SSH tunnel and live Qortium Core API whenever practical.

Compare all relevant layers:

```text
application expectation
bridge response
Core API response
live QDN resource
UI state
```

Do not guess that a problem is only in the UI when read-only live evidence can
be collected. Investigation stays read-only unless the owner explicitly
authorizes publication, signing, moderation, transactions, or any other live
mutation.

## 3. Trace the First Confirmed Failure Gate

Bugfixes and audits must follow the production path:

```text
UI
-> component/hook/state
-> service/domain wrapper
-> Qortium Home bridge
-> Core/QDN
-> response parser
-> validation
-> reducer/state
-> render
```

Stop at the first confirmed broken step. Later stages that were never reached
must remain `NOT VERIFIED`, not blamed by inference.

Do not begin from a guessed root cause. Fix the first confirmed mismatch rather
than patching a downstream symptom.

## 4. One Issue Per Fresh Implementation Conversation

Routine implementation work uses:

```text
fresh conversation
-> one issue only
-> concrete observed live symptom
-> expected behavior
-> production-flow trace
-> read-only live-node investigation
-> evidence-based root cause
-> minimal fix
-> npm run verify
-> concise report
-> owner live validation
```

Prompts must describe the observed symptom and expected behavior without
over-directing the presumed root cause.

The implementation agent must not commit, push, publish, release, close issues,
perform live mutations, or modify unrelated work unless explicitly instructed.

If the first implementation fails live validation:

1. give the exact live failure back to the same issue-focused session;
2. allow one focused correction;
3. if it still fails, use an independent audit/rescue agent.

## 5. Verify Bridge Response Shapes Per Command

Do not assume every Qortium Home bridge action returns the same response shape.

A confirmed production shape for some `FETCH_NODE_API` calls is:

```typescript
{
  body,
  data,
  ok,
  status,
  ...
}
```

For those calls, the Core response may be in `response.data`. Other commands,
including some QDN resource and name lookups, may already return unwrapped
payloads.

Production parsers must be small, reusable, command-specific, and tested using
real confirmed response shapes. Tests must exercise the production parser, not
duplicate parsing logic.

Failures must not silently become valid domain values:

```text
lookup failure -> zero balance
authority failure -> unknown owner
incomplete discovery -> valid empty state
transaction lookup failure -> accepted operation
```

Likewise, incomplete discovery and complete rejection are different states.
Preserve `incomplete`, `unavailable`, `rejected`, and valid-empty outcomes
separately so partial evidence cannot become either authority or a false
complete result.

## 6. New Applications Must Be Architecture V2-Native

Do not start from a V1 write model and later add V2 shadow entities,
compatibility publications, or parallel authority systems.

Before implementing a feature, define:

```text
canonical entity
authority source
immutable proof
operation lineage
derived indexes
discovery path
state/reducer path
publication flow
reload behavior
live-test scenario
```

Indexes and caches are derived hints, not canonical authority. Embedded fields
such as author name, user ID, publisher name, or wallet address are claims until
validated through required immutable evidence and name-wallet evidence.

Legacy compatibility must not weaken Architecture V2 authority. If safe legacy
editing or migration is impossible, keep legacy data read-only and explain why.

## 7. Cache Policy Must Preserve Authority

Every cache must define:

- cache key;
- success TTL;
- failure TTL;
- invalidation;
- force-refresh behavior;
- whether failed or null results are cached;
- whether stale success can be used during incomplete discovery.

A forced high-level refresh must also bypass stale dependent caches where
authority, discovery, identity, balance, or transaction evidence depends on
them.

Transient null results must not poison authority resolution long after the
bridge, node, or QDN resource recovers.

## 8. Coordinated Multi-Resource Publication Is Not Atomic

At Qortium Home commit `a41e5f9678d7f20d7fb77a223c45fddc0096632e`,
the exact bridge action is `PUBLISH_MULTIPLE_QDN_RESOURCES`. Its request has a
non-empty `resources` array. Each entry supplies `service`, `name`, optional
`identifier`, `title`, `description`, `category`, `tags`/`tag1` through
`tag5`, and `fee`, plus either inline `data64`/`base64` or a `sourceToken`.

Home presents one approval request for the resource count, then processes each
entry sequentially as its own QDN transaction. The response is:

```typescript
{
  accepted: true,
  action: 'PUBLISH_MULTIPLE_QDN_RESOURCES',
  published: Array<{ result, resource, transactionSignature }>,
  failures: Array<{ error, resource }>
}
```

This is coordinated application/UI-level approval with explicit partial-success
semantics. It is not one transaction, rollback is not shown, and it must not be
described as transaction-level or application-level atomicity. Source does not
establish a separate "chunks window" beyond the single approval request.

## 9. Publication and Release Require Exact Provenance

Publication, release, and deployment are independent external mutations and
require explicit owner authorization.

Authorization is layered. Task/model authorization permits source and
documentation edits. Execution-harness permission controls shell, network, and
filesystem access. Destructive/release authorization covers commit, push, tag,
release, QDN publish, deploy, transaction/payment, issue mutation, and other
external writes. Full-access execution permission does not imply
destructive/release authorization.

For every artifact or QDN deployment, record:

- source repository and commit;
- clean install/build commands;
- verify/build results;
- artifact path and checksum when applicable;
- service/name/identifier;
- publication or release action performed;
- embedded Home and owner live-validation status.

A deterministic artifact does not prove deployed behavior. A deployed resource
does not prove stable release readiness until the required embedded/live checks
pass.

## 10. Reporting and Closure

Issue-scoped reports use
`/home/iffi/VsCodec-Projects/Qortium/docs/<project-slug>/issues/`.

Treat implementation reports as engineering handoff artifacts, not verbose
diaries. A useful report records scope and baseline, architecture/contracts,
files changed, validation, adversarial findings and fixes, live evidence,
unresolved decisions or blockers, exact owner smoke, and final status. It does
not narrate every command.

Reports must distinguish:

- verified fact;
- inference;
- unknown;
- owner decision;
- automated validation;
- Core/API evidence;
- embedded Home evidence;
- live QDN evidence;
- owner validation still required.

Do not close or recommend closing an issue that requires owner live validation
until that validation is confirmed.

## 11. Qortium Platform Integration Is Reference-First

Platform-level integration MUST NOT be designed from memory when current
working Qortium implementations already exist.

Before implementing or materially changing any of the following, search the
current checked-out Qortium repositories and working Qortium dApps for proven
reference implementations:

- Qortium Home/QDN bridge bootstrap and request transport;
- bridge tokens, injected globals, request/response envelopes, and errors;
- selected account/authentication and account-change handling;
- registered-name and publisher identity resolution;
- owner/admin authorization and owner-only navigation;
- embedded routing, `_qdnBase`, basename, and dynamic QDN render paths;
- QDN publication, source-token/file-path flows, discovery, fetching, status,
  metadata, URLs, and deletion, plus platform-specific file/source handling;
- Home settings, display settings, share/navigation, clipboard, and other
  platform capabilities.

The required sequence is:

```text
platform requirement or live symptom
-> search current Qortium Home/Core and working dApps
-> identify one or more proven reference implementations
-> document the exact runtime contract
-> compare the target app against the reference as a subsystem
-> reuse or adapt the proven pattern
-> implement the complete integration change
-> run focused automated checks
-> run one end-to-end runtime smoke test
```

Do NOT default to:

```text
invent wrapper
-> observe one symptom
-> patch one field
-> retest
-> discover next missing field
-> repeat
```

For bridge/auth/routing/QDN infrastructure, agents SHOULD inspect the complete
integration boundary together rather than debugging isolated lines unless a
working-reference comparison proves the rest of the subsystem already matches.

Classify every proposed integration solution as:

- **Direct reuse** — copy the proven Qortium mechanism with only project-specific
  adaptation;
- **Adaptation** — preserve the verified Qortium contract behind the app's own
  abstraction layer;
- **Project-specific implementation** — allowed only when no current Qortium
  reference covers the requirement, with the reason documented.

A working reference MUST be preferred over speculative diagnostics or custom
platform plumbing. Temporary diagnostics are appropriate only after the
reference comparison has been performed and a runtime uncertainty genuinely
remains.

Reference-first does not mean blindly copying obsolete code. The reference must
be current, Qortium-native, and checked against the present Home/Core behavior.
When multiple working implementations differ, determine which one matches the
current runtime and application context before adapting it.

Reports for platform-integration work MUST identify the repositories/files used
as references and distinguish verified reuse from newly designed behavior.

## 12. Autonomous Phase Execution Loop

For substantial implementation phases, prefer one autonomous phase controller
over repeated human-mediated micro-prompts when the agent has sufficient local
context, repository access, tests, reference sources, and runtime evidence.

The objective is not speed. The objective is to take a phase from its current
state to the strongest validation state the available environment can prove,
while minimizing unnecessary owner intervention.

A phase controller SHOULD execute this loop autonomously:

```text
read authoritative phase spec and current worktree
-> inspect current Qortium references
-> implement the phase or next coherent correction
-> run automated validation
-> switch to an adversarial reviewer role
-> audit the implementation against the phase exit criteria
-> classify findings by severity
-> fix all in-scope blocker/high findings
-> run complete validation again
-> investigate live Core/QDN evidence when relevant
-> perform available runtime validation
-> repeat until no known phase blocker remains
```

The agent MUST NOT stop merely because typecheck, unit tests, lint, or build
passes. After every substantial implementation pass it must re-read the phase
exit criteria and perform an adversarial self-audit that assumes its own
implementation may still be wrong.

When the self-audit finds an in-scope blocker or high-severity correctness
problem, the default behavior is to fix it and repeat the complete validation
cycle without returning to the owner for routine direction.

The autonomous loop SHOULD include, where applicable:

- reference-first verification against current Home/Core and working dApps;
- domain/data-integrity checks;
- publication and reload paths;
- cache, account-switch, and stale-async behavior;
- React/provider/store lifecycle behavior;
- failure, retry, partial-success, and recovery paths;
- read-only live Core/QDN investigation;
- local runtime/browser smoke;
- embedded Qortium Home validation when the execution environment supports it.

Live evidence must be preferred over inference. If an SSH tunnel, local Core
API, or live QDN resource is already available, agents SHOULD use it directly
for read-only verification instead of asking the owner to manually inspect
state that the agent can inspect itself.

Autonomy has two separate permission layers:

1. **Task authorization** — the prompt or project rules state what the agent is
   allowed to inspect, modify, publish, sign, delete, commit, push, or otherwise
   mutate.
2. **Execution-environment authorization** — the harness/CLI must be configured
   so routine authorized shell, filesystem, network, tunnel, and test operations
   do not pause for manual approval.

Prompt-level wording such as "full access" cannot override a restrictive
sandbox or approval mode. For unattended autonomous work, both layers must be
configured consistently. If the environment still requires manual approval for
an otherwise-authorized routine action, the report must classify that as an
execution-environment limitation rather than a missing implementation decision.

Autonomous execution does NOT grant unlimited external mutation authority.
Unless explicitly authorized, the agent must still stop before publication,
signing, live transactions, destructive deletion, commit/push, release, or
other external mutations. When an owner explicitly grants a bounded test
namespace or deployment target, the agent may use that target only within the
stated scope and must record exact provenance and results.

A phase is NOT complete merely because the autonomous loop reaches a clean local
state. Completion status must distinguish at least:

- **IMPLEMENTED** — code exists;
- **LOCAL/AUTOMATED VERIFIED** — local checks pass;
- **READY FOR OWNER VALIDATION** — no known implementation blocker remains but a
  required owner/live step is unavailable to the agent;
- **COMPLETE** — all required validation levels, including embedded/live owner
  evidence where required, have passed.

The preferred stop conditions for an autonomous phase controller are:

1. **READY FOR OWNER VALIDATION / CLOSURE** — no known in-scope implementation
   blocker remains and only explicit owner/live validation is outstanding;
2. **OWNER DECISION REQUIRED** — a genuine product/architecture decision is
   absent from authoritative specs and cannot be safely inferred;
3. **ENVIRONMENT BLOCKER** — a required capability is unavailable and no
   equivalent verification route exists.

Routine command execution, testing, source inspection, read-only live-node
queries, and in-scope local fixes are not valid reasons to stop when they are
authorized and technically available.

The final phase report MUST record:

- starting worktree state;
- authoritative specs and Qortium references used;
- autonomous cycles performed;
- material findings discovered after initial implementation;
- root causes and fixes;
- tests and final validation results;
- live Core/QDN/runtime evidence actually obtained;
- external mutations performed, if explicitly authorized;
- exact remaining owner validation;
- final phase status using the validation states above.

## 13. Validation Layers Are Not Interchangeable

Plan and report three evidence layers separately:

A. **Automated integrity** — typecheck, unit/integration/contract tests,
   lint/format, production build, production preview, and any project-defined
   verify command.

B. **Adversarial agent audit** — after implementation, the agent deliberately
   stops acting as implementer and attempts to invalidate its own work, looking
   for BLOCKER/HIGH architectural and runtime issues. Confirmed findings are
   fixed and revalidated. An agent self-report alone is not the audit.

C. **Owner product/runtime validation** — real embedded Qortium Home use, real
   user workflows, UX/product correctness, and runtime behavior that tests or
   source inspection cannot prove.

No layer substitutes for another. Owner-found runtime/product defects are
valuable evidence in their own right; they are not merely missed unit tests.

## 14. Autonomous Work Units and Owner Product Audits

Prefer a coherent engineering scope over micro-prompting. When an owner/runtime
review produces several related findings that share architecture or domain
context, group them into one scoped autonomous remediation controller followed
by full cross-feature regression, rather than repeating one tiny issue, one
prompt, and one patch dozens of times.

Do not combine unrelated concerns merely to reduce prompt count. The unit of
autonomous work is coherent engineering scope, not necessarily one bug or one
roadmap phase.

After autonomous implementation, treat the owner product audit as an explicit
cycle: owner runtime/product audit, findings collected and classified by
domain/severity, then a coherent next autonomous scope. Do not interrupt owner
validation with micro-fixes for every minor observation, especially during
beta/hardening periods.

## 15. Platform-Boundary Escalation

When a defect appears to originate in Qortium Home/Core rather than in the dApp:

1. reproduce and trace the production path;
2. identify the first confirmed rejecting/failing layer;
3. inspect current Home/Core source;
4. classify the result as `DAPP BUG`, `PLATFORM BUG`, `CONTRACT MISUSE`, or
   `OWNER DECISION REQUIRED`;
5. avoid inventing a dApp workaround merely to make the symptom disappear;
6. if the correct fix is platform-side, preserve the supported dApp
   architecture, prepare a focused platform patch or report only where
   authorized, keep platform modifications separate from application
   modifications, and record deployment/upstream requirements explicitly.

A dApp must not switch from a proven native platform path to an inferior
fallback solely because a platform implementation bug exists.

## 16. Exit Criteria, Status, and Completion Gates

Derive or state an exit criterion before coding. An agent must not stop merely
because the code compiles, the first test run is green, or the requested files
were changed. It stops only when the exit criterion is satisfied, no known
BLOCKER/HIGH issue remains, required local validation is complete, and remaining
owner/runtime/platform work is stated explicitly. Avoid endless polishing after
the criterion is met.

Use the standard statuses `NOT STARTED`, `IMPLEMENTED`,
`LOCAL/AUTOMATED VERIFIED`, `READY FOR OWNER VALIDATION`, and `COMPLETE`. Add
task-specific terminal states such as `OWNER DECISION REQUIRED`,
`ENVIRONMENT BLOCKER`, and `PLATFORM DEPLOYMENT REQUIRED` when they are the
truth. The final handoff guide defines the report-level completion and terminal
vocabulary; map `READY FOR OWNER VALIDATION` to the owner-live-validation-required
handoff status rather than maintaining two unrelated vocabularies.

Do not mark work `COMPLETE` merely because tests passed, code exists, or a
platform patch exists locally but has not been deployed where runtime proof
requires it. Be precise about which component is complete:

```text
app implementation = ready
platform patch = locally verified
runtime = deployment required
```

## 17. Task Controllers Reference the Standard

Use three distinct layers:

```text
shared standard = HOW the agent works
project docs     = WHAT is true
task controller  = WHAT to achieve now
```

Once mandatory autonomous behavior exists in the canonical standard and shared
AGENTS guidance, controllers reference that behavior instead of duplicating
generic execution instructions. A controller still explicitly states the
repository, current task scope, authoritative docs, unusual constraints,
owner-granted write/commit/deploy authority, task-specific invariants, and the
stop condition. Generic rules need not be copied into every prompt.

This lowers prompt duplication and token cost, reduces contradictory
instructions, and makes workflow maintenance easier. It must not reduce
task-specific safety or architecture requirements to ambiguity.

## 18. Release-Candidate Independent Audit

For a major release candidate, an independent audit distinct from the primary
implementation agent is recommended. The reviewer should approach the code as a
hostile or skeptical reviewer, verify architecture and contracts, inspect
high-risk integration paths, and report findings rather than rewrite large
areas unnecessarily. The implementation agent can then remediate confirmed
findings.

The general principle is that the implementation agent should not be the only
final release reviewer. Agent and model assignments are workflow choices; no
vendor or model is part of this rule.

## 19. Optional Engineering Telemetry and Role Specialization

For substantial autonomous projects, record when practical and available:

- starting and ending API spend or credit;
- request count;
- token count when reported by the environment;
- approximate autonomous agent runtime;
- number of autonomous controllers;
- tests before and after;
- agent-found BLOCKER/HIGH defects;
- owner-found runtime defects;
- independent-audit findings.

Prefer raw measurements over vendor pricing, because pricing changes. This is an
optional engineering telemetry practice for comparing workflow efficiency
across projects, not a mandatory administrative burden.

Different agents or models may be assigned roles by cost, speed, code-generation
ability, context capacity, or architecture/review quality. This is an optional
orchestration strategy, not a platform requirement, and no provider is
universally superior.

## Related Guides

- [`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md)
- [`../../agents/qortium-architecture-and-data-integrity.md`](../../agents/qortium-architecture-and-data-integrity.md)
- [`../../agents/qortium-home-and-bridge.md`](../../agents/qortium-home-and-bridge.md)
- [`../../agents/qdn-publication-discovery-and-scaling.md`](../../agents/qdn-publication-discovery-and-scaling.md)
- [`../../agents/live-qdn-validation.md`](../../agents/live-qdn-validation.md)
- [`primary implementation work model`](../workflows/deepseek-primary-work-model.md)
