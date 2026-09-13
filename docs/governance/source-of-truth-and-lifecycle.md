# Source of Truth and Documentation Lifecycle

## Purpose

Define where Qortium facts and rules belong, how conflicts are resolved, and
how active guidance is separated from project documentation and historical
reports.

## Authority by subject

### Platform behavior

Use this order:

1. current checked-out Qortium Home source;
2. current checked-out Qortium Core source;
3. verified runtime behavior tied to an exact environment and revision;
4. current project source and tests;
5. canonical shared guidance;
6. historical reports and prior conversation.

Runtime evidence proves what the observed environment did. It does not prove
that a different source revision or deployed artifact behaves identically.
Record provenance when the distinction matters.

### Project implemented behavior

Use this order:

1. current project source and Git history;
2. durable project documentation in the application repository;
3. `projects/<project-slug>.md` in this repository;
4. historical task reports.

Owner decisions govern desired product behavior and authorization, separately
from this factual source order. Existing code cannot overrule owner intent;
report implementation gaps and verify platform feasibility. Shared coordination
roles and handoff follow `/home/iffi/VsCodec-Projects/AI-Orchestration/AGENTS.md`.

Project context summarizes verified current facts and routing. It MUST NOT
override current source, and stale snapshots MUST be dated and labeled.

### Shared workflow and governance

Use this order:

1. current local `qortium-dev-workspace` working tree for active editing;
2. approved committed revision in this repository;
3. GitHub mirror of the approved revision;
4. legacy workspace or project-local agent guidance only as migration evidence.

Pending uncommitted governance content is locally authoritative for the active
review session but is not an approved published standard until reviewed and
committed.

## Content ownership

| Content                                                                                    | Canonical location                                 |
| ------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| Minimum agent contract and routing                                                         | `AGENTS.md`, `agents/`                             |
| Workflow v2 execution contract                                                             | `docs/workflows/workflow-v2.md`                    |
| Reusable dApp architecture rules                                                           | `docs/architecture/`                               |
| Agent-specific constraints                                                                 | `agents/roles/`                                    |
| Current shared project context                                                             | `projects/<slug>.md`                               |
| Reusable task/report shapes                                                                | `templates/`                                       |
| Durable application architecture/API/operator/release docs                                 | application repository `docs/`                     |
| AI audits, investigations, implementations, runtime reports, validation, reviews, handoffs | `/home/iffi/VsCodec-Projects/Qortium/docs/<slug>/` |
| Platform implementation truth                                                              | current Home/Core repositories                     |

Global rules MUST NOT be copied into application repositories. A project
`AGENTS.md` is a thin entry point containing only project-specific deltas and a
route to this repository.

## Fact state

Separate:

- **VERIFIED CURRENT** — checked against current source or measured runtime;
- **VERIFIED HISTORICAL** — true for a recorded revision/environment;
- **INFERENCE** — supported but not directly proven;
- **UNKNOWN** — evidence is unavailable;
- **OWNER DECISION** — product or authority choice not derivable from source.

Do not call a dated report “stale” merely because it is historical. The problem
is presenting historical evidence as current guidance without provenance.

## Document lifecycle

### Active canonical guidance

Active guidance is linked from `AGENTS.md`, the session router, or the routed
guide index. It must be maintained, internally consistent, and free of
project-specific facts unless the file is under `projects/`.

### Durable project documentation

Application READMEs and `docs/` contain product identity, architecture, data
models, APIs, migration specifications, operator guidance, and reproducible
release/deployment procedures. They do not store AI task reports.

### Historical reports

Reports preserve what was inspected, changed, measured, or concluded at a
specific time. Do not rewrite their evidence to match current behavior. When
moving reports, preserve a path/checksum manifest. Mark supersession through an
index or later report.

### Legacy guidance

Before removing legacy guidance:

1. inventory it;
2. classify reusable, project-specific, obsolete, and historical content;
3. merge reusable rules into canonical destinations;
4. validate incoming references;
5. remove or replace the old active entry point;
6. retain Git history or another recoverable record.

Do not maintain a full “compatibility copy” that agents can mistake for current
authority.

## Local and GitHub lifecycle

The local canonical repository is edited and validated first. GitHub mirrors
only an owner-approved coherent revision.

Required synchronization sequence:

```text
local baseline and dirty-state review
-> scoped edits
-> link/reference/terminology validation
-> complete diff review
-> owner approval for external Git actions
-> commit
-> push
-> verify remote commit equals approved local commit
```

Commit, push, tag, release, publication, deployment, and issue mutation remain
separate permissions. A request to edit documentation does not imply permission
to synchronize GitHub.

## Conflict handling

When two sources conflict:

1. identify the subject: platform behavior, project state, workflow, or
   historical evidence;
2. apply the matching authority order above;
3. inspect current source/runtime rather than choosing the newer-looking prose;
4. label remaining uncertainty;
5. challenge the lower-authority claim with evidence;
6. request an owner decision only when evidence cannot decide the matter.

## Completion criteria

- Every active rule has one canonical location.
- Every active project has one shared project context.
- Application repositories contain only thin agent deltas and durable docs.
- Reports are retained outside application documentation.
- Historical evidence is not presented as current platform truth.
- Local and GitHub governance state can be compared to an exact commit.

## Related files

- [`../../AGENTS.md`](../../AGENTS.md)
- [`../workflows/workflow-v2.md`](../workflows/workflow-v2.md)
- [`../workflows/report-storage-policy.md`](../workflows/report-storage-policy.md)
- [`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md)
