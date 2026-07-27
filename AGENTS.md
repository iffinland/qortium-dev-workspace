# Qortium Development Orchestration

This repository is the canonical shared control and knowledge repository for
Qortium development. It contains documentation and workflows, not project
source code or secrets.

Every substantial task MUST begin with
[`agents/00-SESSION-START.md`](agents/00-SESSION-START.md), then be classified
using
[`agents/01-TASK-CLASSIFICATION.md`](agents/01-TASK-CLASSIFICATION.md).
After classification, read:

1. the matching root-level `projects/<project>.md`;
2. only the relevant routed global guides; and
3. the acting agent's thin role overlay under `agents/roles/`, when applicable.

Global guides are shared and MUST NOT be duplicated per agent. Project-specific
facts belong only under `projects/`.

Before platform-dependent implementation, verify current Qortium Home and Core
source. Keep verified facts, inference, unknowns, and owner decisions clearly
separated.

Agents MUST NOT commit, push, tag, release, publish, deploy, close issues, or
perform other external mutations without explicit owner authorization.

Agent selection and escalation follow
[`docs/workflows/deepseek-primary-work-model.md`](docs/workflows/deepseek-primary-work-model.md).

The old workspace-level
`/home/iffi/VsCodec-Projects/Qortium/agents` directory is not canonical and is
outside this repository and this migration.
