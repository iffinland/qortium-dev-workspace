# Project — Community Discussion Boards

## Purpose and scope

Canonical context for the local Community Discussion Boards prototype. Read
after [`../agents/00-SESSION-START.md`](../agents/00-SESSION-START.md). It is
not the `Discssion-Boards` repository and MUST NOT inherit that project's
identity or release state.

## Repository and local path

- Local path:
  `/home/iffi/VsCodec-Projects/Qortium/projects/community-discussion-boards`
- Package/version: `community-discussion-boards` / `0.1.0`
- Canonical report root:
  `/home/iffi/VsCodec-Projects/Qortium/docs/community-discussion-boards/`
- Independent Git repository/remote/branch: **NONE VERIFIED**

The directory was untracked under the broader Qortium workspace at the
2026-08-30 inspection. Git facts from the parent workspace MUST NOT be
misrepresented as this project's repository baseline.

## Current state

Verified snapshot on 2026-08-30:

- Local source, dependencies, and build output exist; the directory occupied
  approximately 82 MB.
- A thin root `AGENTS.md`, durable `README.md`, and promotion/release gates were
  added on 2026-08-30; they do not create a Git or publication identity.
- Routes and state cover topics, threads, posts, replies, edits, tombstones,
  restores, pending confirmation, load progress, Home display settings, and
  deep links.
- The initial implementation was adapted from donor project `qortium-boards`
  at recorded revision `e4a1bec`; donor facts remain historical evidence only.
- Existing architecture/audit/implementation reports are under the canonical
  report root above.

## Development identity and data model

Current configuration declares:

- application name: `Community_Discussion_Boards`;
- application identifier: `Community_Discussion_Boards`;
- display name: `Community Discussion Boards`;
- schema: `qortium.community-discussion-boards.v1`;
- data service: `JSON`;
- generated manifest version: `0.1.0`.

These values are **DEVELOPMENT DEFAULTS**, not verified published identity.
They MUST be finalized and checked against QAVS/Home/Core constraints before a
first publication.

## Authority and compatibility boundaries

Current source must be inspected for publisher and operation authority before
any write-sensitive task. Donor identifiers, trust anchors, permissions,
migrations, or compatibility assumptions MUST NOT be copied merely because
some code was adapted. Derived lists and embedded payload authors do not by
themselves establish ownership.

## Home/Core dependencies

The source performs bridge detection, selected-account/publishing-name access,
QDN operations, Home display integration, and deep-link routing. Verify each
material contract from current Home and Core source.

Shared reference revisions on 2026-08-30:

- Qortium Home: `927d932bdf29e9641e15519ff0309316ac6afe46`
- Qortium Core: `d0da4036263a057d6f1d25356d19427170d8f93b`

## Key commands

```bash
npm ci
npm run test
npm run build
```

Also inspect the complete local tree and run `git diff --check` only after the
project has an independent Git repository. Do not report the parent workspace
status as project validation.

## Live validation

When the prototype is prepared for runtime evaluation, validate bridge
detection, selected account/name, create/edit/delete/restore authority, pending
confirmation, refresh/readback, deep links, and display settings in embedded
Home. Use read-only live Core/QDN evidence through the applicable SSH tunnel.
The 2026-08-30 preview endpoint was `http://127.0.0.1:24891`; verify the
environment and endpoint before reuse.

Automated tests, local build/preview, and mocks do not prove embedded Home or
live QDN behavior.

## Known limitations and owner decisions required

- There is no independent version-control boundary or remote.
- Application identity is a development default; live publication is unknown.
- Generated `dist/` and installed dependencies coexist with unversioned source.
- Owner decision required: promote into a dedicated repository with approved
  identity/governance, or archive/remove it in a later explicitly authorized
  migration.

## Mandatory project rules

- Treat the prototype as unversioned and unpublished until evidence proves
  otherwise.
- Do not apply Discussion Boards release status, SysOp, namespace, or V2
  compatibility claims to this project.
- Do not delete, archive, initialize/push a repository, publish, or deploy
  without explicit owner authorization.
- Save generated reports only under the canonical report root above.
