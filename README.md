# Qortium Development Workspace

This repository is the canonical shared control and operational knowledge base
for AI-assisted Qortium development. It centralizes task routing, verified
global development rules, project context, reusable issue and handoff
templates, and thin agent role overlays.

## Knowledge model

ChatGPT, Codex, DeepSeek, and future agents share one global guide set under
`agents/`; they do not maintain separate copies. ChatGPT can coordinate,
review GitHub-backed evidence, and plan work. Local agents such as Codex can
inspect project workspaces, implement authorized changes, and return structured
evidence. DeepSeek can perform bounded investigation and secondary analysis.
GitHub provides durable collaboration history, while local workspaces hold
checked-out project and Qortium platform repositories.

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
│   ├── decisions/
│   ├── deepseek/
│   └── workflows/
└── templates/
    ├── PROJECT-CONTEXT.md
    ├── AUDIT-ISSUE.md
    ├── IMPLEMENTATION-ISSUE.md
    └── OWNER-HANDOFF.md
```

## Onboarding a project

Keep the project's source code and detailed implementation documentation in its
own repository. Create one root-level project context file from
[`templates/PROJECT-CONTEXT.md`](templates/PROJECT-CONTEXT.md), record verified
identity, architecture, dependencies, commands, and validation requirements,
then route work through
[`agents/00-SESSION-START.md`](agents/00-SESSION-START.md). Add or change global
guidance only when a rule is reusable across Qortium projects.

## Public-repository boundary

Never store project source code, generated release artifacts, user data, or
confidential operational material here. Secrets, credentials, private keys,
wallet seeds, API keys, server credentials, and private infrastructure details
MUST NEVER be committed. Project source remains in its own repository.
