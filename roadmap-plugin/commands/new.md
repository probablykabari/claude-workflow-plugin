---
name: new
description: Create a new roadmap file from the standard template
argument-hint: "[optional: feature name like 'user-authentication']"
allowed-tools: Read, Write, Glob
---

Create a new roadmap markdown file in the `roadmap/` directory using the standard template.

## Steps

1. Check that `roadmap/` directory exists:
   - If it doesn't exist, tell the user: "The `roadmap/` directory doesn't exist. Run `/roadmap:init` first."
   - Then stop.

2. Determine the feature name:
   - If an argument was provided, use it as the feature name
   - Otherwise, ask the user: "What is the name of this feature or work scope?"

3. Derive the filename:
   - Convert the feature name to kebab-case (e.g., "User Authentication" → `user-authentication.md`)
   - Full path: `roadmap/[kebab-case-name].md`

4. Check if the file already exists:
   - If it does, tell the user and ask: "A roadmap file for '[name]' already exists. Open it instead?"
   - If yes, read and display the file contents

5. Create the file with this exact template (replace placeholders with actual values):

```markdown
# Feature: [Feature Name]

## Description

[Brief description of the feature or work scope — what it does and why it's needed.]

## Plan

[Summary of how to complete the items below. Add sub-sections with expanded detail for complex tasks.]

### Notes

[Any gotchas, constraints, or things to keep in mind.]

### Related Files

- [Add relevant file paths and why they're referenced]

### Items

#### High Priority

- [ ] [First task]
- [ ] [Second task]

#### Low Priority

- [ ] [Optional improvements or nice-to-haves]
```

6. Tell the user: "Created `roadmap/[filename]`. Edit it to fill in your plan and items, then use `/roadmap:next` to start working through them."
