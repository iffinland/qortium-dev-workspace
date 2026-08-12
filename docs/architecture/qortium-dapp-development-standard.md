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

## 4. One Issue Per Fresh DeepSeek Conversation

DeepSeek work uses:

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

DeepSeek must not commit, push, publish, release, close issues, perform live
mutations, or modify unrelated work unless explicitly instructed.

If the first implementation fails live validation:

1. give the exact live failure back to the same issue-focused session;
2. allow one focused correction;
3. if it still fails, use Codex as an independent audit/rescue agent.

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
  metadata, URLs, and deletion;
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

## Related Guides

- [`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md)
- [`../../agents/qortium-architecture-and-data-integrity.md`](../../agents/qortium-architecture-and-data-integrity.md)
- [`../../agents/qortium-home-and-bridge.md`](../../agents/qortium-home-and-bridge.md)
- [`../../agents/qdn-publication-discovery-and-scaling.md`](../../agents/qdn-publication-discovery-and-scaling.md)
- [`../../agents/live-qdn-validation.md`](../../agents/live-qdn-validation.md)
- [`../workflows/deepseek-primary-work-model.md`](../workflows/deepseek-primary-work-model.md)
