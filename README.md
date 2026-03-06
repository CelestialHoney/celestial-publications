# celestial-publications

A personal repository for articles and thinkpieces authored by Celeste Aronow.
Co-authors and collaborators contribute via pull requests, but all content is led and approved by the repository owner.

## Prerequisites

| Tool | Purpose | Install (MacOS) |
|------|---------|---------|
| [Git](https://git-scm.com/) | Version control | `brew install git` |
| [Dolt](https://www.dolthub.com/repositories) | Database backend for issue tracking | `brew install dolt` |
| [beads](https://github.com/steveyegge/beads) | Local issue tracking | See [beads install guide](https://github.com/steveyegge/beads#installation) |
| [Vale](https://vale.sh/) | Prose linting and spellcheck | `brew install vale` |

## Getting Started

```bash
# Clone the repository
git clone https://github.com/CelestialHoney/celestial-publications.git
cd celestial-publications

# Initialize beads issue tracking
bd init

# Start the Dolt server (needed for beads)
cd .beads/dolt && dolt sql-server --host 127.0.0.1 --port 3307 &
cd -

# Verify everything works
bd list              # Should list open issues
vale articles/       # Should run without errors
```

## Directory Structure

```
celestial-publications/
├── articles/          # All articles; series get subdirectories
├── research/          # Notes, transcripts, interview material (do not commit sensitive data)
├── assets/            # Images, figures, charts
├── .github/           # PR template, CODEOWNERS
├── references.bib     # Shared bibliography (BibTeX)
├── .vale.ini          # Prose linting config
└── .beads/            # Issue tracking database
```

## Writing Conventions

**One sentence per line** in all Markdown prose.
This keeps git diffs precise and makes review easier.
Rendered output is unaffected.

Every article must include YAML frontmatter:

```yaml
---
title: "Article Title"
description: "One-line summary or subtitle"
authors: ["Name"]
topics: ["tag1", "tag2"]
category: "broad grouping"
series: "Series Name"       # omit for standalone articles
part: 1                     # omit for standalone articles
target_publication: "Blog, etc."
published_date:             # filled in when published
---
```

## Branching & Review

| Branch | Meaning |
|--------|---------|
| `draft/article-name` | Work in progress |
| PR open to `main` | Article proposed / under review |
| Merged to `main` | Approved |
| `hotfix/description` | Quick corrections to approved work |

All PRs to `main` require approval from the repository owner via CODEOWNERS.

## Commit Format

```
type(scope): description
```

| Type | Use for |
|------|---------|
| `draft` | New article content or significant additions |
| `revise` | Edits to existing prose |
| `research` | Notes, transcripts, references |
| `fix` | Typos, grammar, broken links |
| `meta` | Frontmatter, config, CI, templates |
| `chore` | Repo maintenance, tooling, cleanup |

Scope is the article or series name in kebab-case.
Omit scope for repo-wide changes.

Examples:
- `draft(climate-ethics): outline and first two sections`
- `fix(team-retros): correct attribution typo`
- `meta: add Vale config`
