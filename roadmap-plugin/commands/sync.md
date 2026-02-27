---
name: sync
description: Rebuild roadmap/index.json by scanning all roadmap files — use after manual edits to roadmap files
argument-hint: ""
allowed-tools: Read, Write, Glob
---

Rebuild `roadmap/index.json` by reading every roadmap file and counting their task items.

## Steps

1. Use Glob to find all `roadmap/*.md` files, excluding `CLAUDE.md`.

2. If no files found, tell the user: "No roadmap files found. Run `/roadmap:init` to set up the directory."

3. For each file, read it and count:
   - All `- [x]` items under `#### High Priority` → `high.done`
   - All `- [ ]` items under `#### High Priority` → derive `high.total = high.done + high.remaining`
   - Same for `#### Low Priority`
   - Extract the feature name from the `# Feature: [name]` heading

4. Compute `status` for each entry:
   - `"not_started"` — `high.done + low.done == 0`
   - `"complete"` — `high.done == high.total` AND `low.done == low.total`
   - `"in_progress"` — otherwise

5. Build the index object:
   ```json
   {
     "updated": "[today's date as YYYY-MM-DD]",
     "roadmaps": [
       {
         "file": "feature-name.md",
         "feature": "Feature Name",
         "status": "in_progress",
         "high": { "total": 5, "done": 3 },
         "low":  { "total": 2, "done": 0 }
       }
     ]
   }
   ```
   Sort entries by status: `in_progress` first, then `not_started`, then `complete`.

6. Write the object to `roadmap/index.json`.

7. Display a brief confirmation:
   ```
   Index rebuilt: [n] roadmaps indexed
     [n] in_progress
     [n] not_started
     [n] complete

   Run `/roadmap:status` for an overview.
   ```
