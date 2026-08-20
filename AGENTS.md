# Qortium Development Orchestration

This repository is the canonical shared control and knowledge repository for
Qortium development. It contains documentation and workflows, not project
source code or secrets.

## Mandatory operating contract

The canonical standard is the detailed source of truth; this is the minimum.

- Current Qortium Home/Core is the reference truth. Do not design platform
  behavior from memory.
- Autonomous implementation must end with an adversarial self-audit and
  remediation of confirmed BLOCKER/HIGH findings.
- A green automated suite is not enough. Owner product/runtime validation is a
  separate gate before completion.
- Platform-boundary defects must be traced to the first confirmed mismatch and
  classified before any dApp workaround.
- Full-access execution does not imply commit/push/tag/release/publish/deploy/
  issue-closure authority; explicit owner authorization remains required.
- Reports are handoff artifacts and must follow the canonical report-storage
  policy.

Every substantial task MUST begin with
[`agents/00-SESSION-START.md`](agents/00-SESSION-START.md), then be classified
using
[`agents/01-TASK-CLASSIFICATION.md`](agents/01-TASK-CLASSIFICATION.md).
All Qortium dApp work MUST follow the shared
[`docs/architecture/qortium-dapp-development-standard.md`](docs/architecture/qortium-dapp-development-standard.md)
standard.
After classification, read:

1. the matching root-level `projects/<project>.md`;
2. only the relevant routed global guides; and
3. the acting agent's thin role overlay under `agents/roles/`, when applicable.

Global guides are shared and MUST NOT be duplicated per agent. Project-specific
facts belong only under `projects/`.

Keep verified facts, inference, unknowns, and owner decisions clearly separated.

Agent selection and escalation follow
[`docs/workflows/deepseek-primary-work-model.md`](docs/workflows/deepseek-primary-work-model.md).

All AI-generated investigation, audit, implementation, review, runtime,
validation, comparison, and owner-handoff reports MUST follow
[`docs/workflows/report-storage-policy.md`](docs/workflows/report-storage-policy.md).
The final response MUST state the exact absolute saved report path.
Agents MUST NOT invent an alternative report location.

The old workspace-level
`/home/iffi/VsCodec-Projects/Qortium/agents` directory is not canonical and is
outside this repository and this migration.
