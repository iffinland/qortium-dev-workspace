# Project — Video Center

## Purpose and scope

Canonical project-specific context for Video Center. Read after
[`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md); use shared
workflow and architecture guides for global rules.

## Repository and local path

- Repository: `iffinland/Video-Center`
- Remote: `git@github.com:iffinland/Video-Center.git`
- Local path: `/home/iffi/VsCodec-Projects/Qortium/projects/Video-Center`
- Primary branch: `main`
- Package/version: `video-center` / `0.1.0`
- Canonical report root: `/home/iffi/VsCodec-Projects/Qortium/docs/video-center/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `ef9232656ff3ce6ba78a38de95be32bdea264be4`
  (`docs: align project guidance with Workflow v2`)
- HEAD equals `origin/main`; the working tree is clean.
- A durable root `README.md` and `docs/RELEASE.md` were added on 2026-08-30.
- Routes cover home, video detail, channel, following, and publishing.

Re-run the Git baseline before each task; this snapshot is not a permanent
claim.

## Product purpose

Video Center is a decentralized video-sharing dApp with channel, following,
publishing, playback/detail, and reaction flows. Its source references
Discussion Boards as an architectural donor, but Video Center remains an
independent product with its own identities and data model.

## QDN application identity

Current `qortium-app.json` declares:

- service: `APP`;
- publishing name: `Video_Center`;
- identifier: `video-center`;
- entry: `index.html`;
- category: `Media`;
- version: `0.1.0`.

The manifest repository/homepage point to `QortiumDev/video-center`, while the
actual Git remote is `iffinland/Video-Center`. This is a verified provenance
mismatch requiring an owner/release decision; do not silently rewrite either
identity during unrelated work.

Manifest permissions include QDN search/fetch/list/status/URL, publication,
selected-account/name access, `SEND_COIN`, and `FETCH_NODE_API`. Presence in a
manifest does not authorize an agent to publish or transact.

## Authority and entity model

Verify the current architecture and reaction foundations in source before
changing publisher authority, entity ownership, operations, indexes, or
compatibility behavior. Donor patterns are references only; Discussion Boards
identifiers, trust anchors, or migration rules MUST NOT be copied implicitly.

## Home/Core dependencies

Verify current Home bridge contracts and Core QDN/media behavior before
platform-dependent work. Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
  (local owner changes present; re-fetch/re-verify as needed)
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

## Key commands

```bash
npm ci
npm run typecheck
npm run test
npm run build
npm run lint
npm run format:check
git diff --check
```

## Live validation

Validate routing from `_qdnBase`, playback/media retrieval, channel identity,
following, reactions, selected-account behavior, publishing approval, refresh,
and direct routes in embedded Home and, when claimed, the exact deployed QDN
resource. Use the applicable read-only Core endpoint/SSH tunnel for live QDN
evidence. `http://127.0.0.1:24891` was the reachable preview endpoint during
the 2026-08-30 audit; it is environment-specific and must be rechecked.

Automated architecture tests, mocks, local preview, and build output do not
prove embedded or deployed behavior.

## Known limitations and decisions required

- Manifest GitHub provenance conflicts with the actual remote.
- Live publication and deployed-build provenance were not verified.
- Durable architecture/operator documentation remains limited; README and
  release gates now exist.
- Owner decision is required before correcting publication/repository metadata
  or performing any release/publication.

## Mandatory project rules

- Preserve application identity and entity authority unless an approved
  migration says otherwise.
- Do not inherit another project's trust anchor or namespace.
- Do not publish, send coins, commit, push, tag, deploy, or release without
  explicit owner authorization.
- Save generated reports only under the canonical report root above.
