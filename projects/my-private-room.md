# Project — my-private-room / My File Office

## Purpose and scope

Canonical project context for the repository directory `my-private-room`, whose
current package/product name is My File Office. Read after
[`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md).

## Repository and local path

- Repository: `iffinland/my-private-room`
- Remote: `git@github.com:iffinland/my-private-room.git`
- Local path: `/home/iffi/VsCodec-Projects/Qortium/projects/my-private-room`
- Primary branch: `main`
- Package/version: `my-file-office` / `0.1.0`
- Canonical report root:
  `/home/iffi/VsCodec-Projects/Qortium/docs/my-private-room/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `651152e36a429ca44a6889f87b01818395456101`
  (`fix: replace misleading privacy claims with development notice`)
- HEAD equals `origin/main`.
- Owner changes are present in the dashboard, file service/types, QDN search,
  QDN services, and reference-store implementation/tests. Preserve them.
- A durable root `README.md` and blocked `docs/RELEASE.md` gate were added on
  2026-08-30. No `qortium-app.json` was found.
- Current routes are the access gate and dashboard.

This is a dated snapshot; re-check Git before every task.

## Product and privacy boundary

The current application is a file-office/reference prototype. Current source
explicitly records that QDN `FILE` resources are public and that Qortium Home
does not currently provide private-resource semantics for this flow. A local
gate, private-looking UI, or application name does **not** make QDN content
confidential.

Never describe this application as secure private storage without a separately
verified encryption, key-management, threat-model, and live-runtime design.

## QDN identities and entity model

- File metadata/resource prefix: `mpr_`
- Service used for file resources: `FILE`
- Metadata encoding: JSON
- Reference prefix: `mpr_ref_`
- Reference schema: `qortium.mpr.qdn-ref.v1`
- References point to original QDN resources rather than republishing their
  content.

The publication script defaults to service `APP` and name/identifier
`MyFileOffice`, but these values are environment-overridable. They are script
defaults, **not** verified live deployment identity. No publication is
authorized by their presence.

## Authority and Home/Core dependencies

Verify selected-account/name authority, reference ownership, overwrite
semantics, and approval behavior from current source and live runtime. Verify
QDN service/search/fetch/status behavior from current Core and bridge contracts
from current Home.

Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

## Key commands

```bash
npm ci
npm run build
npm run lint
git diff --check
```

`npm run qdn:publish` is a live mutation command and MUST NOT be run without
explicit owner authorization for the exact target identity and artifact.

## Live validation

Use read-only Core/QDN evidence through the applicable SSH tunnel to validate
public resource discovery, metadata, status, and references. Use embedded Home
for selected account, approvals, routing, resource selection, refresh, and
readback. The workstation preview endpoint verified on 2026-08-30 was
`http://127.0.0.1:24891`; determine intended environment and recheck it.

Mocks, unit/integration tests, local preview, and build output do not prove
deployed persistence, Home compatibility, or confidentiality.

## Known limitations and owner decisions required

- Public QDN storage is not private storage.
- The existing `qdn:publish` helper is not an approved release path: current
  source sends only `dist/index.html` and uses an unsupported encrypted-vault
  description. Remediate it in a separate implementation task before use.
- Canonical live application identity and deployed provenance are unverified.
- Product naming differs between directory and package/UI lineage.
- The owner must choose the intended privacy/security architecture and final
  publication identity before release claims.

## Mandatory project rules

- Do not publish user files while claiming confidentiality that QDN does not
  provide.
- Do not republish referenced content unless an approved feature explicitly
  requires and authorizes it.
- Do not run the publish script, commit, push, deploy, transact, or release
  without explicit owner authorization.
- Save generated reports only under the canonical report root above.
