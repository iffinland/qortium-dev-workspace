# Report Storage Policy

## Purpose

Define the single mandatory storage location for all AI-generated work reports
produced during Qortium development.

## Canonical report root

All AI-generated work reports MUST be stored under:

```
/home/iffi/VsCodec-Projects/Qortium/docs/<project-slug>/
```

Agents MUST NOT place these reports in an individual application repository's
`docs/` directory.

## Report categories and directory layout

Use these standard report-type subdirectories when applicable:

| Directory                                   | Report type                                             |
| ------------------------------------------- | ------------------------------------------------------- |
| `docs/<project-slug>/audits/`               | audit reports                                           |
| `docs/<project-slug>/investigations/`       | investigation reports                                   |
| `docs/<project-slug>/implementations/`      | implementation reports                                  |
| `docs/<project-slug>/runtime/`              | runtime diagnostics                                     |
| `docs/<project-slug>/validation/`           | live-QDN validation reports                             |
| `docs/<project-slug>/reviews/`              | DeepSeek reviews, Codex reviews                         |
| `docs/<project-slug>/handoffs/`             | owner handoffs                                          |

Also covered by this policy:

- comparison reports;
- pilot measurements;
- temporary technical findings that must be retained.

Do not create every directory in advance. Create only the required project and
report-type directories when a report is actually written.

## Project slug rules

- Use lowercase kebab-case matching the project name (e.g. `video-center`,
  `blogs`, `discussion-boards`, `iffi-vaba-mees`).
- The slug is derived from the project's repository or workspace directory name.

## File naming

Use the format:

```
YYYY-MM-DD-<task-or-issue>-<report-type>.md
```

Examples:

```
docs/video-center/audits/2026-07-27-thumbnail-discovery-audit.md
docs/blogs/runtime/2026-07-27-startup-runtime-report.md
docs/iffi-vaba-mees/reviews/2026-07-27-issue-12-review.md
docs/discussion-boards/handoffs/2026-07-27-issue-16-handoff.md
```

Use lowercase kebab-case throughout.

## Report storage vs. project documentation

### Workspace report storage

Use:

```
/home/iffi/VsCodec-Projects/Qortium/docs/<project-slug>/
```

For:

- audit reports;
- investigation reports;
- architecture review reports;
- implementation reports;
- runtime diagnostics;
- live-QDN validation reports;
- comparison reports;
- DeepSeek reviews;
- Codex reviews;
- owner handoffs;
- pilot measurements;
- temporary technical findings that must be retained.

### Project repository documentation

Use:

```
/home/iffi/VsCodec-Projects/Qortium/projects/<project>/docs/
```

Only for durable source-controlled documentation such as:

- project architecture;
- data-model documentation;
- user or operator guides;
- release instructions;
- migration specifications;
- API documentation;
- permanent diagnostics documentation;
- documentation that is part of the application repository itself.

## Directory creation behavior

- Missing `docs/<project-slug>/` directories are created automatically when the
  first report for that project is written.
- Missing report-type subdirectories are created automatically when the first
  report of that type is written.
- Agents MUST NOT pre-create unused directories.

## Prohibited locations

Agents MUST NOT write AI-generated work reports into:

- any application repository's `docs/` directory;
- the `qortium-dev-workspace/docs/` directory (reserved for workspace
  documentation);
- any `projects/<project>/` tree (reserved for project context files);
- any temporary or scratch directory outside the canonical root.

## Existing reports

This policy applies immediately to all new reports. Existing reports will be
inventoried and migrated in a separate task. Do not move, rename, or delete
existing reports during policy rollout.

## Required final report path disclosure

Every final report MUST include the exact absolute path where it was saved:

```
Report saved:
/home/iffi/VsCodec-Projects/Qortium/docs/<project-slug>/<report-type>/<filename>
```

If no report file was created, state:

```
Report saved:
Not created — <reason>
```

Agents MUST NOT claim that a report was saved unless the file exists on disk.

## Related files

- [`../workflows/deepseek-primary-work-model.md`](deepseek-primary-work-model.md)
- [`../../agents/final-report-and-owner-handoff.md`](../../agents/final-report-and-owner-handoff.md)
- [`../../agents/00-SESSION-START.md`](../../agents/00-SESSION-START.md)
- [`../../templates/DEEPSEEK-TASK.md`](../../templates/DEEPSEEK-TASK.md)
- [`../../templates/OWNER-HANDOFF.md`](../../templates/OWNER-HANDOFF.md)
