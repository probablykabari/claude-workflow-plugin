---
name: status
description: Show roadmap progress — all roadmaps from the index, or detailed view for a specific file
argument-hint: "[optional: filename like feature-name.md, or 'all' for full overview]"
allowed-tools: Read, Glob
---

Show roadmap progress. Behavior depends on the argument:

- **No argument** — show the overall index summary (fast, no file reads required)
- **Filename argument** — show detailed progress for that specific file
- **`all` argument** — show detailed progress for every roadmap file

---

## No Argument: Index Overview

1. Check if `roadmap/index.json` exists:
   - If it does not exist, tell the user: "No index found. Run `/roadmap:sync` to build it, or pass a filename for a single-file view."
   - Then stop.

2. Read `roadmap/index.json`.

3. Display a summary table:

```
# Roadmap Overview
Last updated: [index.updated]

| Feature              | High Priority  | Low Priority   | Status       |
|----------------------|---------------|----------------|--------------|
| User Authentication  | ████░░ 3/5    | ██░░░░ 1/3     | in_progress  |
| Dark Mode            | ██████ 3/3    | ████░░ 2/3     | in_progress  |
| Onboarding Flow      | ░░░░░░ 0/4    | ░░░░░░ 0/2     | not_started  |

Overall: 6 / 17 items complete across 3 roadmaps
Active: 2  |  Not started: 1  |  Complete: 0
```

Use block characters to fill progress bars: `█` for done, `░` for remaining (6 chars wide).

4. If the index is empty, tell the user: "Index is empty. Run `/roadmap:sync` to populate it."

---

## Filename Argument: Detailed File View

1. Read the specified file from `roadmap/[filename]`.

2. If the file doesn't exist, tell the user and list available `.md` files in `roadmap/` (excluding `CLAUDE.md`).

3. Parse and display:

```
# [Feature Name]

[Description — first paragraph of the Description section]

## Progress

### High Priority
  ✅ 3 / 5 complete
  ⬜ 2 remaining:
     - [ ] Task one
     - [ ] Task two

### Low Priority
  ✅ 1 / 3 complete
  ⬜ 2 remaining:
     - [ ] Task three
     - [ ] Task four

Overall: 4 / 8 items complete (50%)
```

4. If all items are complete, congratulate the user: "All items complete! This roadmap is done."

---

## `all` Argument: All Files Detailed

Run the Filename view for every `.md` file in `roadmap/` (excluding `CLAUDE.md`), separated by horizontal rules.
