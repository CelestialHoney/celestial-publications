# Project Setup: To Do & Reasoning

## To Do

- [x] Decide: Monorepo vs. Polyrepo
- [x] Decide: Repository & project naming conventions
- [x] Decide: Directory structure
- [x] Decide: Branching strategy (Draft -> Proposed -> Published)
- [x] Decide: Collaboration & permissions model
- [x] Decide: Writing format conventions (e.g. one sentence per line)
- [x] Decide: Research & data management approach
- [x] Decide: Bibliography management (submodule vs. direct .bib)
- [x] Decide: YAML frontmatter schema
- [x] Finalize: YAML frontmatter schema fields (add series/part/category, review all fields)
- [x] Decide: Large asset handling (Git LFS)
- [x] Decide: PR template & editorial checklist
- [x] Decide: Automation & tooling (conversion scripts, linters, spellcheck)
- [ ] Set up Vale config for prose linting, spellcheck, and YAML frontmatter validation on `/articles/`
- [ ] Set up GitHub Actions CI to run Vale on PRs touching `/articles/`

## Reasoning Log

### 1. Monorepo vs. Polyrepo
**Status:** Decided
**Thinking:** A monorepo consolidates all articles, thinkpieces, and research into one repo with shared config, CI, and assets. A polyrepo gives each major project its own repo with full isolation and granular permissions. An organizational model (GitHub Org with teams) is also an option.
**Trade-offs:**
- *Monorepo:* Lower admin overhead, shared assets/references, easier global progress tracking. Can get unwieldy if collaborators shouldn't see each other's projects.
- *Polyrepo:* Maximum isolation, project-specific permissions. More repos to manage.
- *Org model:* Team-based access tiers, but adds GitHub admin complexity.
**Outcome:** Monorepo. Nothing here will be too sensitive for work colleagues to see, so granular permissions are unnecessary. If a project grows large enough to warrant its own repo, it will be split out at that time.

### 2. Repository & Project Naming Conventions
**Status:** Decided
**Thinking:** Descriptive kebab-case names incorporating a keyword or date (e.g. `smith2024-geopolitics-series`) make purpose immediately clear to humans and automation alike.
**Trade-offs:**
- Date-based prefixes help with chronological sorting but can feel rigid.
- Keyword-only names are more flexible but may collide.
**Outcome:** Keyword-only, kebab-case names. No date prefixes. The repo is small enough (personally written articles) that collisions are unlikely.

### 3. Directory Structure
**Status:** Decided
**Thinking:** Folders should reflect content maturity and separate concerns: creative output, research context, and admin/config. Originally proposed status-based folders (`/drafts/`, `/proposed/`, `/published/`), but since branches handle the editorial lifecycle (see #4), folders should organize by content type instead.
**Trade-offs:**
- Status-based folders give visual progress but create file rename noise in git history and duplicate the branch-based lifecycle.
- Content-based folders keep files in place — branches are the source of truth for status.
**Outcome:** Content-based organization. Branches handle lifecycle, folders handle content type:
- `/articles/` — All articles. Series/categories get their own subdirectory (e.g. `/articles/ai-ethics-series/part-1-foundations/`). Standalone articles sit directly under `/articles/` (e.g. `/articles/one-off-thinkpiece/`). Series/category membership is also tagged in frontmatter (`series`, `part`, `category` fields) for queryability, but folder structure is the primary grouping.
- `/research/` — Notes, transcripts, interview material
- `/assets/` — Images, figures, charts
- `/.github/` — PR templates, CODEOWNERS

### 4. Branching Strategy
**Status:** Decided
**Thinking:** A "Progressive Stability" model mapping the editorial lifecycle to branches. Originally proposed a three-tier model (topic → proposed branch → main), but a separate long-lived `proposed` branch adds overhead without much benefit for a personal/small-team repo.
**Trade-offs:**
- Three-tier (topic → proposed → main) is rigorous but slow for the expected volume.
- Two-tier (topic → main via PR) is simpler — the PR itself serves as the "proposed" state.
**Outcome:** Two-tier branching. The PR is the "proposed" stage:
- `draft/article-name` — writing in progress
- Open PR to `main` — article is proposed/under review
- Merge to `main` — approved. Done as far as this repo is concerned (publication or Slack review happens outside the repo).
- `hotfix/description` — quick corrections to approved work on `main`

### 5. Collaboration & Permissions Model
**Status:** Decided
**Thinking:** Owner acts as "Integration Manager" — collaborators contribute via PRs, owner has final merge authority. Enforced via:
- Branch protection rules on `main` and `proposed` (require approved review + status checks)
- CODEOWNERS file auto-requesting owner review on `/published/` and `/proposed/` changes
**Trade-offs:**
- Strict protection prevents accidents but can bottleneck on owner availability.
- Trusted editors could be granted merge rights on `proposed` to reduce bottleneck.
**Outcome:** All PRs into `main` (and other protected branches) require owner as CODEOWNER reviewer. No trusted editors at this time. Will revisit if collaboration scales.

### 6. Writing Format Conventions
**Status:** Decided
**Thinking:** "One sentence per line" in Markdown makes git diffs surgical — changing one sentence doesn't mark the whole paragraph as changed. Simplifies review and conflict resolution significantly.
**Trade-offs:**
- Looks unusual to writers used to wrapping paragraphs naturally.
- Requires contributor onboarding/agreement.
- Rendered output is unaffected (Markdown joins lines into paragraphs).
**Outcome:** One sentence per line. Document this convention in CLAUDE.md and README so contributors and tooling follow it.

### 7. Research & Data Management
**Status:** Decided
**Thinking:** Research context needs its own strategy:
- Sensitive material (interview transcripts) should be `.gitignore`d or stored outside the repo — git history is permanent even after deletion.
- Non-sensitive notes go in a flat, searchable `/thoughts/` or `/research/` directory.
- Raw datasets tracked via Git LFS or DVC to avoid bloating the repo.
**Trade-offs:**
- Keeping everything in-repo is convenient but risks committing sensitive data.
- External storage adds tooling complexity.
**Outcome:** Research notes and transcripts go in `/research/`. Not expecting sensitive data for current topics — add a README note that truly sensitive data should not be committed (git history is permanent). No LFS/DVC for now; revisit if research data becomes bulky.

### 8. Bibliography Management
**Status:** Decided
**Thinking:** Two approaches for managing references:
- *Submodule:* Bibliography lives in its own repo, linked as a submodule. Multiple projects share one source of truth.
- *Direct:* Single `references.bib` in the repo root. Simpler setup, works well for a monorepo.
- Naming convention for keys: first four letters of surname + last two digits of year (e.g. `Smit24`).
**Trade-offs:**
- Submodules add complexity (collaborators must `git submodule update`).
- Direct .bib is simpler but doesn't share across repos if you go polyrepo.
**Outcome:** Single `references.bib` file in the repo. Simpler approach fits the monorepo decision. No submodules.

### 9. YAML Frontmatter Schema
**Status:** Decided
**Thinking:** Each Markdown file gets metadata at the top. Originally included `status` and `owner_signoff`, but those are redundant with the branch/PR workflow. `last_updated` is redundant with git history. Added `series`/`part`/`category` for content grouping, `description` for summaries, and `published_date` for tracking publication outside the repo.
**Trade-offs:**
- Dropped `status`, `owner_signoff`, `last_updated` — covered by branches and git history.
- Added `published_date` since git commits won't know when an article is published externally.
**Outcome:** Use YAML frontmatter. Branch/folder location is the source of truth for editorial status. Finalized schema:
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

### 10. Large Asset Handling
**Status:** Decided
**Thinking:** Git LFS stores binary files (images, figures, video) on a remote server with small pointers in the repo. Keeps the repo lightweight and fast to clone.
**Trade-offs:**
- Requires LFS setup on each collaborator's machine.
- GitHub has LFS storage/bandwidth limits on free plans.
- Alternative: store assets externally (S3, CDN) and reference by URL.
**Outcome:** Deferred. Not needed right now. Will revisit if large assets become a concern.

### 11. PR Template & Editorial Checklist
**Status:** Decided
**Thinking:** A `.github/pull_request_template.md` auto-populates PR descriptions with a checklist. Original proposal was heavy (style guide adherence, citation checks, etc.) — better suited for external collaborators. For a personal/small-team repo, keep it lightweight and focused on context. Single template for all PR types.
**Outcome:** Lightweight single template. Checklist filled out by the PR submitter to confirm they've done each item:
```markdown
## Summary
<!-- What is this article about? -->

## Type
<!-- article | revision | research | other -->

## Checklist
- [ ] One sentence per line
- [ ] Frontmatter complete and accurate
- [ ] Research notes linked (if applicable)
- [ ] Spellcheck/proofread
```

### 12. Automation & Tooling
**Status:** Decided
**Thinking:** Start minimal, add as pain points emerge. Prose linting and spellcheck provide the most value upfront. PDF conversion, bib validation, and dashboards can wait.
**Outcome:** Vale (already installed locally) as the single tool handling prose linting, spellcheck, and YAML frontmatter validation. GitHub Actions CI runs Vale on PRs that touch `/articles/`. Everything else (PDF conversion, bib cleanup, dashboard generation) deferred until needed. Frontmatter format is YAML.
