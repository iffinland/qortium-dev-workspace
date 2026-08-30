# Project — Qortium United Community

## Purpose and scope

Canonical project-specific context for Qortium United Community (QUC). Read it
after [`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md). Global
workflow, architecture, and validation rules remain in shared guides.

## Repository and local path

- Repository: `iffinland/Qortium-United-Community`
- Remote: `git@github.com:iffinland/Qortium-United-Community.git`
- Local path:
  `/home/iffi/VsCodec-Projects/Qortium/projects/Qortium-United-Community`
- Primary branch: `main`
- Package/version: `qortium-united-community` / `0.1.0-beta.1`
- Canonical report root:
  `/home/iffi/VsCodec-Projects/Qortium/docs/qortium-united-community/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `7c68ca9cd1e1221d73cdce77246c1521bdaed27b`
  (`docs: add canonical Workflow v2 entry and release gates`)
- HEAD equals `origin/main`.
- The working tree contains owner changes in rich-text display, layout/sidebar,
  global styles, home/post/project pages, image assets/preview, and tests.
  Preserve them.
- No repository `qortium-app.json` was found.
- A thin root `AGENTS.md` and durable `docs/RELEASE.md` were added on
  2026-08-30.
- The repository README describes the first official beta; prior independent
  pre-beta/release audit recorded zero BLOCKER/HIGH findings in its authorized
  scope. That historical audit is not proof of the current dirty tree or live
  deployment.

This is a dated operational snapshot. Establish a fresh baseline before every
task and never overwrite owner changes based on an older release-candidate
inventory.

## Product and architecture state

QUC is a multi-domain community dApp. Current source includes posts/comments,
forum topics/replies, support, polls/votes, projects, wiki, events, reactions,
role snapshots, media references, and owner tombstones through a
publisher-aware validated QDN runtime.

Current architecture decisions retained from owner-approved work:

- identifier families use `qucp-*`; legacy `qucp-v1-*` is rejected;
- production roles are exactly `SysOp`, `Admin`, and `User`;
- SysOp-anchored role snapshots and admin-managed domains fail closed when
  authority history is incomplete, invalid, or ambiguous;
- derived indexes/caches and embedded payload authors do not establish entity
  authority;
- publication confirmation distinguishes accepted-but-unconfirmed writes from
  confirmed persistence;
- mock/demo/placeholder data is prohibited in production flows, while test
  fixtures may mock external boundaries;
- public unencrypted QDN data is not confidential merely because UI access is
  restricted.

Verify current source before applying any of these decisions to a new domain or
release.

## QDN application identity

Owner-recorded live identity:

- service: `APP`;
- publishing name: `Qortium-Unified-Community`;
- identifier: `Community-Portal`;
- URI: `qdn://APP/Qortium-Unified-Community/Community-Portal`.

The exact source/build currently published at this URI remains **UNVERIFIED**.
Do not claim release provenance from the identity alone.

Current data defaults:

- namespace: `qucp-*`;
- service: `DOCUMENT` where used by the current implementation;
- SysOp trust anchor:
  `QWifxJWGbJZ6Yo6kiimFkBGcm4AxQefdUm`, configured in
  `src/config/qortiumTrust.ts`.

Recheck all identity, service, and trust facts in source before a release or
identity-sensitive migration.

## Product decisions and deferred work

Retained domains include Posts, comments, Forum, Support, Polls, Projects,
Wiki, and the public donation/funding direction. Post reactions remain a
required feature. The Moderator role/subsystem is not part of the intended
product; dormant vocabulary may be removed only in a separately scoped task.

Known deferred work from the beta audit includes:

- concurrent account-refresh ordering (`M3`);
- creator-bound Post delete/restore and Poll close lifecycle controls (`M5`);
- Not Found routing, dependency/engine debt, rich-text link-policy alignment,
  and dormant vocabulary cleanup;
- donation/funding redesign and final data architecture;
- final license selection. `GPL-3.0-only` is not an approved assumption.

Treat these as recorded candidates, not automatically authorized next tasks.

## Home display ownership

The centralized adapter at `src/services/qortium/homeTextSize.ts` handles the
Home `textSize` contract. It maps the six Home values to root app presentation,
applies initial settings, handles live events, and gives live events precedence
over a slower bridge read. Home remains the sole `appZoom` authority; QUC MUST
NOT add competing local scaling for Home-controlled zoom.

Revalidate current Home source whenever this contract is material.

## Home/Core dependencies

Verify current source for QDN search/fetch/publish/status, name-to-address
resolution, prefix pagination, media service support, identifier constraints,
transaction confirmation, selected account, Home routing, and display events.

Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
  (local `main`, owner changes present, behind `origin/main` at inspection)
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

These are traceability points, not permanent capability targets.

## Key commands

```bash
npm ci
npm run test
npm run build
npm run lint
git diff --check
```

Use focused tests plus the complete relevant checks. Backup/restore commands do
not authorize replacing owner changes.

## Live validation

For platform-bound behavior, validate through embedded Home and the exact live
QDN resource as applicable. Include selected-account/name transitions,
authorized/unauthorized writes, role-history degradation, publication
confirmation/readback, refresh/deep links, media, display settings, and current
domain lifecycles.

Use the applicable read-only Core endpoint through the SSH tunnel for QDN and
Core evidence. The workstation preview endpoint verified during the 2026-08-30
audit was `http://127.0.0.1:24891`; determine intended environment and confirm
current source/configuration plus reachability before reuse. Port `12391` is a
Qortal endpoint in the inspected dual-runtime configuration and MUST NOT be
assumed to be Qortium.

Automated checks, mocks, local preview, and build success do not prove embedded
Home or deployed QDN compatibility.

## Unknowns requiring owner or live evidence

- exact source/build published at the recorded live URI;
- final donation/funding data architecture;
- whether comments or wiki require reactions;
- final detailed SysOp/Admin/User permission matrix;
- exact boundaries for dormant moderation cleanup;
- final license selection.

## Mandatory project rules

- Preserve the `qucp-*` namespace and fail-closed authority model unless an
  approved migration proves a different design.
- Do not restore obsolete production roles or legacy `qucp-v1-*` behavior.
- Do not treat an old audit, test suite, or historical clean tree as evidence
  for current live behavior.
- Do not commit, push, publish, deploy, transact, tag, or release without
  explicit owner authorization.
- Save generated reports only under the canonical report root above.
