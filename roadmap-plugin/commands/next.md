---
name: next
description: Find the next incomplete High Priority item in a roadmap file and immediately start working on it
argument-hint: "[optional: filename like feature-name.md]"
allowed-tools: Read, Write, Edit, Bash, Glob
---

Identify the next item to work on from a roadmap file and begin implementing it.

## Steps

1. Find roadmap files:
   - Use Glob to find all `roadmap/*.md` files (exclude `CLAUDE.md`)
   - If no files found, tell the user: "No roadmap files found. Run `/roadmap:init` to set up the directory."

2. Determine which file to use:
   - If an argument was provided and matches a file, use it directly
   - If a single file exists, use it automatically
   - If multiple files exist, display a numbered list and ask the user to choose

3. Read the chosen file.

4. Find the next incomplete item:
   - Look for `- [ ]` items in the **High Priority** section first
   - If High Priority is fully complete, look in **Low Priority**
   - If all items are complete, tell the user and stop

5. Display the item and context:
   ```
   ## Next Item: [item text]

   **From**: [filename] — High Priority

   **Plan context**: [Relevant excerpt from the Plan section if it mentions this item]

   **Related files**: [List from Related Files section]

   **Notes**: [Contents of Notes section if present]

   Starting now...
   ```

6. Immediately begin working on the item:
   - Use the Plan section, Related Files, and Notes to guide implementation
   - Read referenced files before making changes
   - Implement the item following the plan

7. After completing the work, mark the item as done:
   - Edit the roadmap file to change `- [ ] [item text]` to `- [x] [item text]`

8. Update `roadmap/index.json` (incremental — do not re-read other roadmap files):
   - Read `roadmap/index.json` if it exists; if not, create a new index object: `{"updated": "[today's date]", "roadmaps": []}`
   - Find the entry whose `file` matches the current roadmap filename
   - If no entry exists for this file, count all `- [x]` and `- [ ]` items in the file (already in memory) to build a new entry
   - If an entry exists, increment the appropriate done counter (`high.done` or `low.done`) by 1
   - Recompute `status`:
     - `"not_started"` — all done counts are 0
     - `"complete"` — all done counts equal their totals
     - `"in_progress"` — otherwise
   - Set `"updated"` to today's date
   - Write the updated JSON back to `roadmap/index.json`

9. Confirm to the user: "Marked '[item]' as complete. Run `/roadmap:status` to see updated progress, or `/roadmap:next` to continue."
