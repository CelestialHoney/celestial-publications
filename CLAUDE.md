# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Project Overview

Monorepo for drafting, reviewing, and approving personal and work-related articles and thinkpieces.
Articles are written in Markdown, reviewed via Pull Requests, and published externally (blog, Slack #writers-room, Google Docs, etc.).

## Directory Structure

- `/articles/` — All articles. Series get subdirectories (e.g. `/articles/ai-ethics-series/part-1/`). Standalone articles sit directly under `/articles/`.
- `/research/` — Notes, transcripts, interview material. Do not commit sensitive data (git history is permanent).
- `/assets/` — Images, figures, charts.
- `/.github/` — PR templates, CODEOWNERS.
- `references.bib` — Shared bibliography (BibTeX). Key format: first four letters of surname + last two digits of year (e.g. `Smit24`).

## Branching Strategy

- `draft/article-name` — work in progress
- Open PR to `main` — article is proposed/under review
- Merge to `main` — approved (publication happens outside this repo)
- `hotfix/description` — quick corrections to approved work

## Writing Conventions

- **One sentence per line** in all Markdown prose. This makes git diffs precise and review easier. Rendered output is unaffected.
- Use kebab-case for all directory and file names.

## YAML Frontmatter

Every article Markdown file must have YAML frontmatter:

```yaml
---
title: "Article Title"
description: "One-line summary or subtitle"
authors: ["Name"]
topics: ["tag1", "tag2"]
category: "broad grouping"
series: "Series Name"       # omit for standalone articles
part: 1                     # omit for standalone articles
target_publication: "Blog, Slack #writers-room, etc."
published_date:             # filled in when published outside the repo
---
```

Branch/folder location is the source of truth for editorial status, not frontmatter. If frontmatter drifts, correct it to match.

## Linting

This project uses Vale for prose linting, spellcheck, and frontmatter validation on `/articles/`.

```bash
vale articles/    # Lint all articles
```

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

Types (editorial-focused):
- `draft` — new article content or significant additions
- `revise` — edits to existing prose (rewording, restructuring)
- `research` — adding notes, transcripts, references
- `fix` — typos, grammar corrections, broken links
- `meta` — frontmatter updates, config, CI, templates
- `chore` — repo maintenance (gitignore, tooling, cleanup)

Scope: article or series name in kebab-case, or omit for repo-wide changes.

Examples:
- `draft(climate-ethics): outline and first two sections`
- `revise(climate-ethics): tighten argument in section 3`
- `research(ai-series): add interview transcript from Dr. Smith`
- `fix(team-retros): correct attribution typo`
- `meta: add Vale config`
- `chore: update PR template`
