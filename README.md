# Qortium Development Workspace

This repository is the canonical shared control and operational knowledge base
for AI-assisted Qortium development. It centralizes task routing, verified
global development rules, project context, reusable issue and handoff
templates, and thin agent role overlays.

The durable cross-project rules are summarized in the
[Qortium dApp Development Standard](docs/architecture/qortium-dapp-development-standard.md).

## Knowledge model

ChatGPT, Codex, DeepSeek, and future agents share one global guide set under
`agents/`; they do not maintain separate copies. ChatGPT scopes, plans, and
reviews. DeepSeek is the default cost-efficient local implementation agent for
routine development—it investigates, implements, and hands off locally. Codex
escalates for high-risk architecture, data-integrity work, repeated failures,
and independent release audits. GitHub provides durable collaboration history,
while local workspaces hold checked-out project and Qortium platform
repositories.

The canonical hierarchy is:

1. current checked-out Qortium Home/Core source for platform behavior;
2. each project's own source and documentation for implementation state;
3. root-level `projects/<project>.md` for shared project context;
4. global guides under `agents/` for reusable workflows; and
5. thin `agents/roles/` overlays for agent-specific operating constraints.

Facts must be labeled as verified, inferred, unknown, or requiring an owner
decision. Project-specific facts must not be promoted into global guidance.

## Structure

```text
qortium-dev-workspace/
├── README.md
├── AGENTS.md
├── agents/
│   ├── README.md
│   ├── 00-SESSION-START.md
│   ├── 01-TASK-CLASSIFICATION.md
│   ├── qortium-native-app-workflow.md
│   ├── qortium-architecture-and-data-integrity.md
│   ├── qortium-home-and-bridge.md
│   ├── qdn-publication-discovery-and-scaling.md
│   ├── issue-driven-audit-and-refactor.md
│   ├── runtime-diagnostics-and-performance.md
│   ├── live-qdn-validation.md
│   ├── qavs-versioning-and-release.md
│   ├── git-generated-files-and-hygiene.md
│   ├── final-report-and-owner-handoff.md
│   └── roles/
│       ├── CHATGPT.md
│       ├── CODEX.md
│       └── DEEPSEEK.md
├── projects/
│   └── discussion-boards.md
├── docs/
│   ├── architecture/
│   │   └── qortium-dapp-development-standard.md
│   ├── decisions/
│   ├── deepseek/
│   └── workflows/
│       ├── deepseek-primary-work-model.md
│       └── report-storage-policy.md
└── templates/
    ├── PROJECT-CONTEXT.md
    ├── AUDIT-ISSUE.md
    ├── IMPLEMENTATION-ISSUE.md
    ├── OWNER-HANDOFF.md
    ├── DEEPSEEK-TASK.md
    └── DEEPSEEK-REVIEW.md
```

## Default agent workflow

```
ChatGPT scopes and reviews
→ DeepSeek investigates and implements locally
→ owner/runtime validation
→ GitHub
→ Codex escalation when required
```

The full operating model—including risk levels, escalation rules, and pilot
measurements—is defined in
[`docs/workflows/deepseek-primary-work-model.md`](docs/workflows/deepseek-primary-work-model.md).

## Onboarding a project

Keep the project's source code and detailed implementation documentation in its
own repository. Create one root-level project context file from
[`templates/PROJECT-CONTEXT.md`](templates/PROJECT-CONTEXT.md), record verified
identity, architecture, dependencies, commands, and validation requirements,
then route work through
[`agents/00-SESSION-START.md`](agents/00-SESSION-START.md). Add or change global
guidance only when a rule is reusable across Qortium projects.

## Report storage

AI-generated work reports (audits, investigations, implementations, reviews,
runtime diagnostics, validations, comparisons, and owner handoffs) MUST be
stored under the canonical workspace report root:

```
workspace-root/docs/<project-slug>/
```

Application repository `docs/` directories are reserved for durable
source-controlled project documentation (architecture, user guides, API docs,
release instructions, migration specs).

See [`docs/workflows/report-storage-policy.md`](docs/workflows/report-storage-policy.md)
for the full policy, including directory layout, filename rules, and required
final report path disclosure.

## Public-repository boundary

Never store project source code, generated release artifacts, user data, or
confidential operational material here. Secrets, credentials, private keys,
wallet seeds, API keys, server credentials, and private infrastructure details
MUST NEVER be committed. Project source remains in its own repository.
