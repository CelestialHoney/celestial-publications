---
name: clean-transcript
description: >
  Use when cleaning meeting transcripts (Google Meet/Gemini, Otter.ai, etc.)
  for inclusion in the research/ directory. Interactively reviews sensitive
  content, then makes surgical edits to a copy in two committed phases:
  structural cleanup (committed) and filler cleanup (left unstaged for review).
---

# Clean Transcript

## User Input

```text
$ARGUMENTS
```

The argument is a file path to a raw transcript. If empty, ask the user for the path.

## Phase 1: Scan

Read the transcript at the provided path. Identify and categorize:

| Category | What to flag |
|---|---|
| **Names** | All people mentioned. Note speakers vs. third parties |
| **Contact info** | Emails, phone numbers, mailto links |
| **Platform artifacts** | Calendar/survey/transcript-tab links, bot footers, "Get tips" links |
| **Small talk** | Greetings, weekend chat, off-topic banter (usually at start) |
| **Internal business** | OKRs, HR, scheduling, role transitions, manager talk, client details, hours |
| **Logistics** | Repo setup, PR mechanics, branch naming, tooling config |
| **Personal anecdotes** | Stories naming private individuals or revealing personal details |
| **Misheard words** | Auto-transcription errors (e.g., "a flight" for "8th Light", misspelled names) |

## Phase 2: Review (MANDATORY — never skip)

1. Present all findings organized by category
2. For each **name**, ask whether to **keep** or **redact**
3. For each **section** flagged for removal, describe it and let the user confirm or override
4. Ask the user about **misheard words** they may recognize
5. **Wait for explicit user confirmation** before any edits

## Phase 3: Structural Edit and Commit

1. **Copy** the original to the research folder. Derive a kebab-case filename from the meeting title and date (e.g., `writing-sync-2026-03-09.md`) unless the user specifies one
2. Make **surgical edits** to the copy using the Edit tool or minimal string replacements. NEVER rewrite the file from scratch.

Apply changes by category:

- **Redacted names** — Replace with anonymized phrasing that preserves context (e.g., "my partner Thomas has ADHD" becomes "some neurodivergent people")
- **Contact info / platform artifacts** — Remove entirely
- **Removed sections** — Replace with italicized note: `*[small talk removed]*`, `*[internal scheduling removed]*`, etc.
- **Misheard words** — Direct replacement throughout (avoid replacing legitimate uses)
- **Personal anecdotes** — Generalize the point without naming individuals

3. `git add` and `git commit` the cleaned file. Use commit format: `research(scope): add cleaned meeting transcript on <topic>`

## Phase 4: Filler Cleanup

Make a **second pass** over the committed file, removing conversational filler:

- **Filler words** — "um", "uh", "like" (when filler), "you know", "I mean", "sort of", "kind of" (when not meaningful)
- **Stutters and false starts** — "I I", "the the", "we we should", abandoned sentence beginnings
- **Unnecessary repeated words** — "really really", "very very"

Use the Edit tool for each removal. Preserve the speaker's meaning and tone — only remove words that add no content. Do NOT `git add` or commit these changes.

## Phase 5: Review Prompt

Tell the user:
1. The structural cleanup (redactions, removals, misheard words) is committed
2. The filler cleanup is applied but **unstaged** so they can review it
3. Suggest: `git diff` to see filler changes, then `git add -p` to accept selectively

## Critical Rules

- NEVER rewrite the file from scratch — always copy-then-edit so the diff is reviewable
- NEVER skip Phase 2 — every transcript has different sensitivity needs
- NEVER reformat or restructure the document layout
- NEVER remove content the user did not approve in Phase 2
- Preserve all timestamp headers and original formatting
- When fixing misheard words, check context to avoid replacing legitimate uses

## Example

```
/clean-transcript /Users/me/Downloads/Meeting-Notes-by-Gemini.md
```
