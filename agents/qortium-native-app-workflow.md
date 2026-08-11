# Qortium-Native Application Workflow

## Purpose

Define a clean workflow for discovering and building a new application directly
for current Qortium Home and Core behavior.

## Use when

Use for `NEW_QORTIUM_APP` and `PRODUCT_DISCOVERY`, including a new product whose
vision originated in an older application.

## Do not use when

Do not use this as a Qortal porting checklist. Do not copy an old Qortal
codebase and progressively replace its runtime. For an existing Qortium
application, use the audit/refactor guide.

## Prerequisites

- Product owner and target users.
- Access to current checked-out Home/Core sources.
- Intended repository location and delivery environment.

## Required inputs

### Product definition

- Problem and target users.
- Minimum usable flows.
- Owner-visible success criteria.
- Non-goals.
- Required concepts or data from an older product.

### Application identity

- Application display name.
- Intended QDN publishing name.
- Application identifier and resource namespace.
- Collision-avoidance strategy.
- Historical compatibility or data-migration requirements.

## Workflow

### 1. Extract requirements, not legacy runtime

From an older application MAY reuse:

- product vision;
- functional requirements;
- UX flows;
- useful domain concepts;
- explicitly validated data.

MUST NOT assume its wrappers, dependencies, routes, bridge actions,
authentication hooks, publication behavior, fallback branches, or version
scheme apply to Qortium.

### 2. Define success before architecture

Document:

- first usable version;
- primary happy paths;
- failure/retry paths;
- owner-visible acceptance checks;
- required embedded or live validation.

### 3. Design authoritative entities

For each entity define:

- immutable entity ID;
- creator;
- authoritative publisher;
- wallet/name validation;
- mutable and immutable fields;
- owner and moderator permissions;
- conflict ordering;
- deletion/tombstone semantics;
- validation and quarantine behavior.

Use
[`qortium-architecture-and-data-integrity.md`](qortium-architecture-and-data-integrity.md).

New applications MUST be Architecture V2-native from the first implementation.
Do not start with a V1 whole-state write model and later add V2 shadow
entities, compatibility publications, or parallel authority systems.

### 4. Design independent operations

Evaluate independent authenticated records for edits, reactions, votes,
moderation, tips, roles, deletion, and membership/access changes. MUST NOT
republish an unrelated full parent snapshot merely to record an operation.
Before defining an application protocol, inspect whether current Core/Home
already provides a suitable native capability and verify its actual bridge
boundary.

### 5. Design QDN identity and scaling

Define service/name/identifier families, prefix partitions, pagination,
budgets, concurrency, partial data, unavailable resources, and caches. Indexes,
directories, and snapshots MUST be derived and rebuildable.

### 6. Define restricted access accurately

Distinguish:

- UI restriction;
- authorization;
- encryption;
- confidentiality.

Public unencrypted QDN data MUST NOT be described as private or confidential
solely because the official UI hides it.

### 7. Verify Home integration

From current Home source verify bridge detection, selected account, registered
names, active publisher, read/write actions, approval/signing, display settings,
language, embedded base routing, share parameters, and clipboard constraints.

### 8. Define publication paths

Separate small inline payloads from current verified source-token/file-path
large-file flows. Define readiness, retries, exact verification, and recovery.
MUST NOT default large files to in-browser base64 without memory and bridge
analysis.

### 9. Design runtime observability

Define startup phases, explicit loading states, timeouts, retry budgets,
stale-result rejection, first useful render, and an optional bounded in-app
diagnostic mechanism.

### 10. Plan release authority

Identify current QAVS source, version authority, synchronization points, RC
policy, provenance, tags, GitHub Release, and QDN deployment. Verify current
rules rather than assigning fields from memory.

### 11. Bootstrap the implementation

Choose current tooling from verified project requirements. Do not assume
`create-qortal-app`, qapp-core, `GlobalProvider`, Qortal authentication hooks,
or Qortal routes. Centralize Home/QDN clients, keep UI bridge-free, and add
validation with each slice.

### 12. Perform browser runtime smoke validation

Successful typecheck, build, lint, formatting, and static inspection are NOT
sufficient evidence that a Qortium dApp is runtime-correct.

For any change that affects the application shell, providers, contexts,
routing, bridge integration, authentication initialization, global state,
external-store subscriptions, or startup/runtime initialization, perform a
browser runtime smoke test before declaring the work complete.

At minimum verify:

- the application mounts successfully;
- the initial public route renders usable UI;
- there are no uncaught application errors in the browser console;
- provider/context initialization does not enter render/update loops;
- external-store snapshots remain stable while state is unchanged;
- basic public-route navigation does not crash;
- refresh/direct-route startup behaves as intended for the current routing model.

When the implementation depends on Qortium Home bridge or embed behavior, local
browser validation MUST be followed by an embedded Qortium Home runtime test at
the required validation level. A local Vite/preview success alone does not prove
Qortium integration correctness.

If direct browser or embedded runtime access is unavailable, the report MUST
state that runtime validation remains unperformed; build/typecheck success MUST
NOT be reported as equivalent runtime validation.

## Mandatory rules

- Current checked-out Home/Core behavior MUST be re-verified before dependent
  implementation.
- Every feature MUST satisfy the canonical standard's Architecture V2-native
  foundation checklist before implementation.
- Web2 infrastructure MUST NOT be introduced by habit when Qortium-native
  capabilities meet the requirement.
- Compatibility MUST be explicit, bounded, and tested.
- User-visible runtime success criteria MUST coexist with architecture tests.
- Browser/runtime smoke validation is mandatory for app-shell/provider/router/
  bridge/startup changes before completion may be claimed.
- A new app MUST NOT inherit an old app's version automatically.

## Validation

- Review the entity/operation model and identifier constraints.
- Test unauthorized publishers, duplicates, conflicts, missing data, partial
  discovery, stale responses, and large datasets.
- Run compile/build/lint/static checks applicable to the project.
- Run browser runtime smoke validation for app startup and user-visible routing.
- Validate at the levels defined in `live-qdn-validation.md`.
- Confirm first usable flows in the actual intended runtime.

## Completion criteria

- Product and non-goals are explicit.
- Authority, identifiers, operations, scaling, Home integration, observability,
  and release policy are designed from current evidence.
- No unreviewed Qortal runtime assumptions entered the implementation.
- Required browser/runtime smoke validation has passed, or the report explicitly
  marks it as outstanding because the required environment was unavailable.
- Owner-visible acceptance criteria pass at required validation levels.

## Related files

- [`qortium-architecture-and-data-integrity.md`](qortium-architecture-and-data-integrity.md)
- [`qortium-home-and-bridge.md`](qortium-home-and-bridge.md)
- [`qdn-publication-discovery-and-scaling.md`](qdn-publication-discovery-and-scaling.md)
- [`runtime-diagnostics-and-performance.md`](runtime-diagnostics-and-performance.md)
- [`qavs-versioning-and-release.md`](qavs-versioning-and-release.md)
- [`../docs/architecture/qortium-dapp-development-standard.md`](../docs/architecture/qortium-dapp-development-standard.md)
