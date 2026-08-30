# Project — Blogs

## Purpose and scope

Canonical project-specific context for the Qortium Blogs application. Read it
after [`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md). Global
workflow and architecture rules remain in shared guides. The obsolete local
porting guide has been retired; the project root `AGENTS.md` is a thin router to
this canonical workspace.

## Repository and local path

- Repository: `iffinland/Blogs`
- Remote: `git@github.com:iffinland/Blogs.git`
- Local path: `/home/iffi/VsCodec-Projects/Qortium/projects/Blogs`
- Primary branch: `master`
- Package/version: `qortium-blog` / `0.1.0`
- Canonical report root: `/home/iffi/VsCodec-Projects/Qortium/docs/blogs/`

## Current state

Verified snapshot on 2026-08-30:

- HEAD: `f94a10ed29bff905fe1e0a3ee1d7850c8fe11f2a`
  (`Polish thumbs-up reactions and home post filtering`)
- HEAD equals `origin/master`.
- The working tree contains owner changes in application, localization,
  blog-service, style, taxonomy, test, and report files. Preserve them.
- A durable root `README.md` and `docs/RELEASE.md` were added on 2026-08-30.
  No `qortium-app.json` was found.
- Vite uses the relative base `./`.

This is a dated operational snapshot. Re-run the Git baseline before every
task and do not infer current state from this section after the repository
advances.

## Product purpose and current implementation

The source implements Qortium-native blog and post creation/editing, comments,
global search, rich text, QDN media/embeds, reactions, shared categories/tags,
selected-account behavior, and Qortium Home display settings. Routes include
home plus blog/post create and edit flows.

## QDN identities and entity model

Current identifier helpers use these prefixes:

- `b.` blogs;
- `p.` posts;
- `c.` comments;
- `i.` images;
- `v.` videos;
- `f.` files.

The exact application publishing name, identifier, live URI, and deployed
build provenance are **UNKNOWN** because no canonical manifest or verified live
publication evidence was found. Do not invent them from directory/package
names. Verify service, identifier, publisher authority, overwrite behavior,
and payload schemas from current source plus live QDN before identity-sensitive
work.

## Authority and Home/Core dependencies

- Use selected-account and current QDN publisher evidence; embedded payload
  authors alone do not establish authority.
- Verify Home bridge actions and response shapes from current Home source.
- Verify Core search, fetch, pagination, identifier, and service behavior from
  current Core source.
- Home owns application zoom. The app may adapt text-size/display settings but
  MUST NOT create a competing zoom authority.

Current shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
  (local `main`, owner changes present, behind `origin/main` at inspection)
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

These are traceability points, not frozen platform targets.

## Key commands

```bash
npm ci
npm run build
npm run test
npm run lint
npm run format:check
git diff --check
```

Use only scripts currently defined in `package.json`. Backup/restore scripts do
not authorize destructive restoration.

## Live validation

For QDN, identity, persistence, or Home-bound behavior, use the applicable
read-only Core endpoint/SSH tunnel and embedded Home in addition to automated
checks. The workstation preview endpoint verified during the 2026-08-30
workspace audit was `http://127.0.0.1:24891`; determine the intended
environment and verify reachability before reuse. A local preview, mock, unit
test, integration test, or build is not proof of live Home/QDN compatibility.

## Known limitations and decisions required

- Application publication identity and deployed provenance remain unknown.
- Durable architecture/data-model documentation and a QAVS manifest remain
  missing; README and release gates now exist.
- The retired project-local porting guide is not shared governance authority.
- The owner must decide publication identity and release scope before a first
  or replacement publication.

## Mandatory project rules

- Preserve the current identifier and publisher authority model unless a
  separately approved migration proves compatibility.
- Do not treat taxonomy indexes, reactions, or embedded authors as entity
  authority without current-source verification.
- Do not commit, push, publish, deploy, transact, or release without explicit
  owner authorization.
- Save generated reports only under the canonical report root above.
