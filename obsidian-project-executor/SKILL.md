---
name: obsidian-project-executor
description: Execute software projects with an Obsidian-backed project plan, feature/gap notes, implementation leaf logs, test-gated completion, and optional graph/vector/sync refresh. Use when asked to continue a tracked project plan, update Obsidian project management notes, close feature or gap items only after tests pass, or apply the same disciplined workflow across coding tools.
---

# Obsidian Project Executor

Use this skill when a project is managed through Obsidian notes and the user expects development progress to be reflected in a project plan index, feature/gap notes, and detailed implementation logs.

## Required Inputs

Discover these from the repo or ask only if they cannot be inferred:

- `vault_dir`: Obsidian vault root.
- `project_plan_index`: operator-facing plan note.
- `source_specs`: source-of-truth docs for feature/gap status.
- `implementation_logs_dir`: Obsidian folder for leaf execution notes.
- `materialize_command`: optional command that regenerates Obsidian project notes from source specs.
- `refresh_commands`: optional graph/vector/index refresh commands.
- `sync_command`: optional privacy-safe backup or mirror command.

Do not invent paths. Search first with `rg --files`, `rg`, `find`, or repo docs.

## Core Rules

- Drive work from the live Obsidian project plan, not memory.
- Treat source specs as the canonical status source when the project has a generator/materializer.
- Do not mark a feature/gap done until implementation and tests pass.
- Keep implementation logs as leaf notes with enough detail to reconstruct the work later.
- Preserve private vault content. Never push or sync notes outside the configured allowlist.
- Never overwrite unrelated user changes.

## Selection Priority

When the user says “continue”:

1. Continue any explicitly requested item.
2. Otherwise choose the earliest unchecked P0/P1 gap or in-progress feature that unlocks visible operator value.
3. Prefer loops that improve reliability or user control:
   - portal/operator controls
   - memory quality/lifecycle
   - source ingestion/pipeline
   - feedback
   - rumination/review
   - auth/security
   - tests and runtime observability

## Before Coding

Before editing files, state briefly:

- **Purpose**: why this item matters.
- **Algorithm**: what behavior will change.
- **Tests**: unit/integration/runtime checks that prove it.

Then implement without waiting unless the user asked for planning only.

## Implementation Workflow

1. Read the relevant Project Plan item, source spec row, and existing code/tests.
2. Inspect current behavior before assuming a gap is real.
3. Make the smallest code change that satisfies the acceptance criteria.
4. Add or update focused tests first.
5. Run focused tests, then broader tests if the touched surface is shared.
6. Update source specs and/or child note frontmatter only after tests pass.
7. Create or update an implementation leaf note.
8. Run materializer/refresh commands if configured.
9. Verify the Project Plan index now reflects the new status.
10. Run runtime/API/UI smoke checks when the change is user-facing.
11. Run privacy-safe sync/backup if configured.

## Implementation Leaf Note

Each completed item should get one note in `implementation_logs_dir`.

Recommended frontmatter:

```yaml
---
title: "<ITEM> <Short Title> Implementation"
category: "implementation-log"
implementation_target: "<ITEM-ID>"
implementation_status: "done"
test_status: "verified"
completed_at: "<ISO timestamp>"
status: "active"
related:
  - "[[Project Plan Index]]"
  - "[[<Feature Or Gap Note>]]"
---
```

Recommended sections:

- `Purpose`
- `Design Decision`
- `Main Processing Flow`
- `Data And State`
- `Operator/API Behavior`
- `Implementation Summary`
- `Files Changed`
- `Tests`
- `Runtime Smoke`
- `Residual Risk`

Implementation logs are not status receipts. They should explain how the subproject works.

## Status Rules

- `done` or `closed`: implemented and verified.
- `in_progress`: partially implemented or verified only in part.
- `planned` / `open`: accepted but not complete.
- `blocked`: only when progress is genuinely impossible without external input.

If the Project Plan is generated, update source specs/frontmatter and rerun the materializer. Do not hand-edit generated tables except to fix the generator.

## Verification Minimum

Use the smallest useful tests first:

```bash
# syntax / type checks if available
<project test command for touched files>

# focused tests
<focused test command>

# broader sweep when shared behavior changes
<full or package test command>
```

For UI/API changes, add one smoke check:

```bash
curl -sS <local-api-health-or-brief-endpoint>
```

For generated Obsidian plans, verify the target item is checked:

```bash
rg -n "<ITEM-ID>|<Item title>" "<project_plan_index>"
```

## Privacy And Sync

Before any backup or Git sync:

- Confirm the sync command is allowlist-based or project-safe.
- Do not push private vault notes, raw archives, local absolute paths, tokens, or personal data.
- If a privacy check fails, fix the offending generated content rather than bypassing the guard.

## Useful Progress Report

When asked for project completion percentage, compute it from the Project Plan:

- feature done / total
- gap done / total
- total done / total

Report exact counts and percentages. Do not estimate by feel.

