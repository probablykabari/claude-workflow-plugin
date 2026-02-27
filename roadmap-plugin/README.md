# Roadmap Plugin

A Claude Code plugin for managing development roadmaps using structured markdown files.

## Overview

This plugin helps you create, track, and work through development roadmaps stored as markdown files in a `roadmap/` directory. Each file represents a feature or scope of work with prioritized task lists.

## Commands

| Command | Description |
|---------|-------------|
| `/roadmap:init` | Set up the `roadmap/` directory with a `CLAUDE.md` |
| `/roadmap:new [name]` | Create a new roadmap file from the template |
| `/roadmap:status [file]` | Show progress summary for a roadmap file |
| `/roadmap:next [file]` | Work on the next incomplete High Priority item |

## Quick Start

1. Run `/roadmap:init` in your project to set up the `roadmap/` directory
2. Run `/roadmap:new my-feature` to create a roadmap file
3. Edit the file to add your plan and task items
4. Run `/roadmap:next my-feature.md` to start working through items
5. Run `/roadmap:status` to check progress at any time

## Roadmap File Format

```markdown
# Feature: [Feature Name]

## Description

Brief description of the feature.

## Plan

How to complete the items. Include detail for complex tasks.

### Notes

Gotchas or constraints.

### Related Files

- `/path/to/file` [why it's relevant]

### Items

#### High Priority

- [x] Completed task
- [ ] Pending task

#### Low Priority

- [ ] Optional improvement
```

## Installation

Copy or symlink this plugin directory to your Claude Code plugins location, or install via the Claude Code plugin marketplace.
