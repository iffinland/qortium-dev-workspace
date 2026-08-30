# Project — NodeFM Station

## Purpose and scope

Canonical project-specific context for NodeFM Station. Read after
[`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md). Global
governance belongs in this workspace. The copied local `agents/` directory and
completed bootstrap prompt were retired; the project root `AGENTS.md` is a thin
router to this canonical workspace.

## Repository and local path

- Repository: `iffinland/nodefm-station`
- Remote: `git@github.com:iffinland/nodefm-station.git`
- Local path: `/home/iffi/VsCodec-Projects/Qortium/projects/nodefm-station`
- Primary branch: `main`
- Package/version: `nodefm-station` / `0.1.0`
- Canonical report root:
  `/home/iffi/VsCodec-Projects/Qortium/docs/nodefm-station/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `6628a658b293f03bd0077f848a0d965314d3c4c4`
  (`docs: align NodeFM guidance with Workflow v2`)
- HEAD equals `origin/main`.
- The working tree contains owner changes across playlist, listener
  submission, request-show, library/cover, scheduling, persistence, tests, and
  playlist-editor files. Preserve them.
- `qortium-app.json` names NodeFM at version `0.1.0`.

This snapshot is dated. Re-run Git status and inspect the current source before
every task.

## Product purpose and priority

NodeFM is a Qortium-native scheduled 24/7 Auto-DJ radio station. Current source
and 2026-08-28 through 2026-08-30 reports show active beta/hardening work,
listener playlists, cold-start improvements, request-show workflows, and
multi-resource persistence beyond the older phase labels in `README.md` and
`docs/ROADMAP.md`.

Core product capabilities include:

- deterministic radio timeline and default rotation;
- scheduled programs with Week/Agenda views;
- immutable playlist versions and public/listener playlists;
- global audio engine and music library;
- QDN media addition/upload flows;
- listener likes, submissions, Request Show, messaging, and tips/donations.

The older README/roadmap phase labels are not a reliable current completion
ledger until separately reconciled. Current source plus canonical saved reports
take precedence for an operational snapshot.

## Explicit non-goal

The future Q-Music-style community music platform is a separate project. Do not
expand NodeFM into general creator publishing, creator profiles, broad social
music discovery, or a general community-playlist platform without a distinct
owner-approved product task. Old Q-Music code may inform requirements or
visuals but MUST NOT become NodeFM's architecture foundation.

## Authoritative durable project documentation

Within the application repository, use these durable specifications while
checking all behavior against current source:

- `docs/PROJECT-VISION.md`
- `docs/ARCHITECTURE.md`
- `docs/QORTIUM-DATA-MODEL.md`
- `docs/RADIO-TIMELINE-SPEC.md`
- `docs/PLAYER-SPEC.md`
- `docs/ADMIN-SPEC.md`
- `docs/ROADMAP.md` (planning history; completion labels may be stale)
- `docs/RELEASE.md`

AI work reports belong under the canonical report root, not the application
`docs/` directory.

## QDN identities and authority

Current code uses multiple `nodefm-*` identifier families and QDN resources for
station state, schedules/playlists, media, listener submissions, and related
operations. Do not reduce this to one generic document or list identifiers from
memory. For each task, verify the exact service, identifier derivation, entity
schema, publisher authority, overwrite/append semantics, and confirmation path
from current source and `docs/QORTIUM-DATA-MODEL.md`.

The exact live QDN application URI and deployed-build provenance are not
verified in this context. A manifest name is not proof of a current deployment.

## Home/Core dependencies

NodeFM depends on current Home bridge contracts for resource fetch/search/URL,
selected account/names, publication/approval, media, and embedded behavior. It
depends on Core for QDN discovery, pagination, fetch/status, identifiers,
services, names, and transactions. Trace contract mismatches to the first
confirmed boundary before adding an application workaround.

Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
  (local owner changes present; behind `origin/main` at inspection)
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

These revisions are traceability points only and must be refreshed for
platform-dependent work.

## Key commands

```bash
npm ci
npm run test
npm run build
npm run lint
npm run format:check
git diff --check
```

Use focused Vitest scopes when useful, then the complete relevant checks.

## Live validation

Validate cold/warm start, continuous playback, refresh/resume, timeline
transitions, schedule/program changes, playlist version/readback, listener
submission and moderation state, Request Show, selected-account behavior,
media URLs, tips/payments, and direct embedded routes at the layers material to
the task. QDN state and Core behavior require read-only live evidence through
the intended SSH-tunnel endpoint; bridge and playback UX require embedded Home.

The workstation preview endpoint verified during the 2026-08-30 audit was
`http://127.0.0.1:24891`. It is environment-specific. Verify current source,
configuration, and reachability before reuse. Mock/unit/integration tests,
local preview, builds, and exact artifacts do not prove live Home or deployed
QDN compatibility.

## Known limitations and owner decisions required

- README/roadmap top-level status was reconciled on 2026-08-30; the roadmap
  remains historical/planning context rather than a live task ledger.
- Exact live application URI and deployment provenance remain unverified.
- Current owner changes span several persistence/playlist workflows.
- Publication, payment, moderation, and release actions require exact separate
  authorization and runtime evidence.

## Mandatory project rules

- Preserve deterministic timeline and audio-engine ownership boundaries.
- Do not introduce a required centralized streaming server, continuously
  running backend player, or hidden daemon unless the owner explicitly changes
  the architecture; live state is deterministic and clock-derived.
- A track without verified valid duration is not schedule-eligible. Do not
  guess missing duration to make a schedule pass.
- A Request Show occurrence must resolve to one deterministic/canonical lineup,
  not independent random selections on different clients. Use defined fallback
  behavior when eligible liked tracks are insufficient.
- Keep timeline/domain logic and raw QDN operations out of visual components,
  and retain one global audio engine.
- Preserve immutable-version and publisher-authority guarantees; derived
  indexes or embedded authors MUST NOT establish authority.
- Do not silently broaden a station task into the future Q-Music product.
- Do not commit, push, publish, deploy, transact, tag, or release without
  explicit owner authorization.
- Save generated reports only under the canonical report root above.
