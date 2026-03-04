# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Project Overview

Collaborative workspace for drafting, reviewing, and publishing written content

## Development Workflow

### Spec-Driven Development (Speckit)

This project uses spec-driven development. Before implementing features:

1. `/speckit-constitution` - Define project principles (do this first, once)
2. `/speckit-specify <description>` - Write feature spec
3. `/speckit-clarify` - Resolve ambiguities
4. `/speckit-plan` - Create implementation plan
5. `/speckit-tasks` - Break into tasks
6. `/speckit-implement` - Execute tasks

### Issue Tracking (Beads)

This project uses beads for local issue tracking:

```bash
bd create --title="Task name" --type=task  # Create issue
bd list --status=open                       # List open issues
bd show <id>                                # View issue details
bd update <id> --status=in_progress         # Start work
bd close <id>                               # Complete issue
bd sync                                     # Sync with git
```

## Commit Format

```
type(scope): description
```

Types: `feat`, `fix`, `refactor`, `docs`, `chore`, `test`
