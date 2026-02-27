---
name: init
description: Initialize the roadmap/ directory with a CLAUDE.md containing format rules and workflow guidance
argument-hint: "[optional: path to project root, defaults to current directory]"
allowed-tools: Read, Write, Glob
---

Set up the `roadmap/` directory in the user's project so Claude understands how to work with roadmap files.

## Steps

1. Determine the target directory:
   - If an argument was provided, use it as the project root
   - Otherwise use the current working directory

2. Check if `roadmap/` directory exists at that root. If not, use the Write tool to create `roadmap/.gitkeep` (this implicitly creates the directory).

3. Check if `roadmap/CLAUDE.md` already exists:
   - If it does, tell the user and ask if they want to overwrite it
   - If confirmed or not present, write the CLAUDE.md

4. Write `roadmap/CLAUDE.md` using the Write tool with this exact content (write it literally, do not interpret it):

    # Roadmap Directory

    This directory contains development roadmap files. Each `.md` file represents a feature or scope of work.

    ## File Format

    Every roadmap file follows this structure:

        # Feature: [Feature Name]

        ## Description

        Brief description of the feature or work scope.

        ## Plan

        Summary of how to complete the items. Include explanations for complex tasks.

        ### Notes

        Gotchas, constraints, or things to keep in mind.

        ### Related Files

        - This work should be completed in the `/some/folder` directory
        - `/path/file` [reason why this file is referenced]

        ### Items

        #### High Priority

        - [x] A completed task
        - [ ] An incomplete task

        #### Low Priority

        - [x] A completed task
        - [ ] An incomplete task

    ## Working With Roadmap Files

    When asked to work on a roadmap item:

    1. Read the full file first — the **Plan** section explains how items should be implemented
    2. Check **Related Files** for relevant paths and context
    3. Read **Notes** for constraints and gotchas
    4. Work through **High Priority** items before **Low Priority** items
    5. After completing an item, mark it done: change `- [ ]` to `- [x]`

    ## Conventions

    - Items marked `- [x]` are complete; do not re-implement them
    - Items marked `- [ ]` are pending
    - High Priority items should always be done before Low Priority items
    - The Plan section may have sub-sections with expanded detail for specific items

5. Tell the user: "Roadmap directory initialized. You can now create roadmap files with `/roadmap:new` or place `.md` files in the `roadmap/` folder manually."
