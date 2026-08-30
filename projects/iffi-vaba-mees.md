# Project — iffi-vaba-mees

## Purpose and scope

Canonical project-specific context for the `iffi_vaba_mees` personal Qortium
dApp. Read it after
[`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md). Shared rules
remain in the canonical workspace guides.

## Repository and local path

- Repository: `iffinland/iffi_vaba_mees`
- Remote: `git@github.com:iffinland/iffi_vaba_mees.git`
- Local path: `/home/iffi/VsCodec-Projects/Qortium/projects/iffi_vaba_mees`
- Primary branch: `main`
- Package/version: `iffi-vaba-mees-website` / `0.1.0`
- Canonical report root:
  `/home/iffi/VsCodec-Projects/Qortium/docs/iffi-vaba-mees/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `336eafc532129a156e90b370889b1c3f482200df`
  (`Fix QDN owner mutations and update project documentation`)
- HEAD equals `origin/main`.
- The working tree contains owner changes across QDN hooks, detail pages,
  domain services, identity, resource, and site-configuration code. Preserve
  them.
- No `qortium-app.json` was found.
- A thin root `AGENTS.md` and durable `docs/RELEASE.md` were added on
  2026-08-30.

This is a dated snapshot. Establish a fresh Git baseline before editing.

## Product purpose and current implementation

The project is a personal Qortium dApp with blogs, galleries, videos, projects,
life-story entries, a guestbook, support, and social interaction flows. The
repository `README.md` is the durable project overview; current source remains
authoritative for behavior.

## Identity, QDN entities, and authority

Current source resolves the site owner dynamically from the selected account
and embedded application publisher identity. `src/utils/siteConfig.js` avoids a
hardcoded owner wallet and validates resolved publisher names/address.

Copied identifier helpers currently include:

- `b.` blogs;
- `p.` posts;
- `c.` comments;
- `i.` images;
- `v.` videos;
- `f.` files.

The exact QDN application publishing name, identifier, live URI, and deployed
build provenance are **UNKNOWN** in this context. Do not infer them from the
repository name or from donor code. Publisher identity, entity ownership,
mutation authority, service, and overwrite semantics MUST be verified in
current source and live QDN before identity-sensitive changes.

## Home/Core dependencies

- Verify publisher/selected-account delivery from current Home source.
- Verify name resolution, QDN search/fetch, media service, and resource status
  from current Core source.
- Home remains the application-zoom authority.

Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

Re-verify these repositories before platform-dependent work.

## Key commands

```bash
npm ci
npm run build
npm run lint
git diff --check
```

The build script is Vite-only and does not itself prove a complete typecheck.
Use additional project-appropriate checks when the task requires them.
Backup/restore scripts do not authorize overwriting owner work.

## Live validation

Validate embedded publisher resolution, selected-account transitions,
authorized and unauthorized owner mutations, resource fetches, media, deep
links, refresh, and persistence through embedded Home and the exact deployed
resource when such behavior is claimed. Use applicable read-only live
Core/QDN evidence via the verified SSH tunnel. The 2026-08-30 preview endpoint
was `http://127.0.0.1:24891`; verify environment and reachability before reuse.

Mocked tests, static review, local preview, and build success are not proof of
live identity or QDN persistence.

## Known limitations and decisions required

- Canonical publication identity and deployed provenance are not documented.
- No canonical manifest was found.
- Owner mutation code is currently under active uncommitted development.
- Release/publication identity must be confirmed before deployment work.

## Mandatory project rules

- Never replace dynamic publisher authority with a hardcoded wallet/name.
- Never trust embedded payload authors or mutable display names alone for owner
  mutations.
- Preserve owner changes and audit any donor-derived identifiers against this
  project's actual data model.
- Do not commit, push, publish, deploy, transact, or release without explicit
  owner authorization.
- Save reports only under the canonical report root above.
