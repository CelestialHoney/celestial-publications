# Article Notes: LLMs Can't Automate Away the Human Experience

**Working title:** "LLMs are proving that it is impossible to automate away the human experience"
**Author:** Celeste Aronow
**Context:** First article as A11y Specialist at 8th Light
**Audience:** Buyer-focused — companies that need accessibility consulting

---

## Core Argument

The promise of automation in accessibility has never been fully realized — and LLMs haven't changed that.

Before LLMs, automated a11y audit tools (axe, Lighthouse, etc.) could only catch a fraction of real WCAG violations and user-facing issues.
LLMs and newer tools like the SilkTide extension (with built-in visual screen reader simulation) have raised the ceiling, but not enough.
The SilkTide visual screen reader misrepresents what real screen readers (NVDA, JAWS, VoiceOver) actually read, sound like, and how they behave — depending on it distorts the picture.
Even when LLMs are used to identify and suggest fixes, there are still serious misses, and the fixes cannot be applied automatically without a skilled engineer manually verifying with a real screen reader.

**The conclusion:** Despite all LLM and tooling advances, any org that wants a genuinely accessible product *must* work with a human specialist.
**The pitch:** 8th Light can be that specialist.

---

## Key Points / Ideas

### What automated tools *can* do (establish the baseline fairly)

Automated tools are genuinely good at detecting:
- Heading hierarchy violations
- Color contrast failures
- Missing alt text on images (in many cases)

Setting this baseline honestly matters — it makes the argument more credible when you turn to what they miss.

### What automated tools miss (false negatives)

Specific categories they struggle with:
- Appropriate ARIA label usage
- Interactive element accessibility (focus management, keyboard operability)
- Many WCAG guidelines that require understanding context and user flow, not just markup inspection

*Research task:* Use Gemini Deep Research to find concrete "big hitter" WCAG violations that automated tools miss — chosen specifically to make a business reader think "Oh gosh, we might have that." (Travis's framing.) Find a stat on what percentage of issues automated tools miss to use as a risk-framing hook.

### What automated tools invent (false positives)

Not just a miss problem — a wasted-effort problem.
Travis's framing: "Not only are the things out there still there, you're still exposed — all the energy you're putting into this, for what."
The SilkTide example in the raw notes below is a concrete instance of this.

### Humanization strategy — two axes

Celeste's framing from the writing sync:
1. The end user who has a disability or accommodation need
2. Celeste's own experience as an engineer using these tools

Practical constraint: keep the personal narrative to a few sentences or a small paragraph.
Enough to humanize; not enough to pull focus from the core argument.

---

## Buyer Angle

**Target reader:** Engineering lead, product owner, or technical decision-maker who genuinely wants to do right by their users.
They've probably already run some automated tooling (axe, Lighthouse, maybe an LLM audit). They feel like they've tried. They don't know what they're missing.

**Emotional arc for the reader:**
1. *Concern* — help them feel genuine care for the users their product is failing right now, not as a compliance problem but as real people
2. *Recognition* — "yes, that's exactly what we've been doing" — naming the false confidence trap without shaming them
3. *Hope and confidence* — a good specialist can make a real difference; this is solvable

**Problems this piece helps buyers solve:**
- "We've done automated audits but aren't sure if we're actually accessible"
- "We don't know what we don't know about our disabled users' experience"
- "We want to do the right thing but don't know how to get there"

**The business case — three angles:**

*1. Revenue*
Disability is not a niche market — it is one of the largest underserved markets.
~$XXXb people globally live with some form of disability (WHO — verify current figure).
In the US alone, the disability community has an estimated $XXXb in disposable income (American Institutes for Research — verify current figure).
These users actively choose products that work for them and drop ones that don't — accessibility is a competitive advantage, not just a compliance checkbox.
An inaccessible product isn't just ethically wrong; it is leaving a massive addressable market on the table.
Framing: if your product is inaccessible, you're not competing for millions of users who are actively looking for something usable.
A specialist who closes that gap doesn't cost you money — they unlock revenue.

*2. Legal risk — ADA and EAA*
In the US, the Americans with Disabilities Act (ADA) applies to digital products.
Web accessibility lawsuits have increased dramatically year over year — $XXX filed in [year] (verify current figures).
The EU Accessibility Act (EAA) came into full effect in June 2025, applying to digital products and services sold in the EU.
Non-compliance is no longer just an ethical failure — it is a legal and financial liability.
"We ran automated tools" is not a defensible position. Tools have known, documented coverage gaps.
Only a genuine audit with human validation can establish a meaningful compliance posture.

*3. B Corp certification*
B Corp accreditation evaluates companies on social and environmental impact, including how they treat all stakeholders — workers, communities, customers.
Accessibility is directly relevant to B Corp's equity and inclusion criteria.
Genuine WCAG compliance signals that an org walks the talk on inclusion — not just internally but in the products they ship to the world.
For companies pursuing or holding B Corp status, accessibility isn't optional optics. It's part of the standard.
(Worth noting: "compliance theater" — passing automated tools without real validation — won't satisfy this either. B Corp asks for substance.)

---

## Rough Outline

Based on the emotional arc (concern → recognition → hope) and the writing sync discussion:

1. **Hook** — concrete "big hitter" WCAG violation or stat on what percentage of issues automated tools miss; framed as a risk signal for business readers
2. **What automation can do** — set the baseline fairly (heading hierarchy, contrast); acknowledge the genuine value
3. **What it misses (false negatives)** — specific WCAG categories with concrete examples
4. **What it invents (false positives)** — the wasted-effort argument; the SilkTide example
5. **Why the gap is unfixable without lived experience** — the nervous system problem; LLMs understand rules but cannot feel the experience
6. **What a real specialist brings** — the pitch; Celeste as the argument made flesh

*Note: Many sections have room to expand into standalone articles. Keep this one focused and tight — personal platform is the place to explore overflow ideas.*

---

## Open Questions

- Find a concrete scene: a real audit moment where a tool said "pass" and lived experience said otherwise. (Celeste to source.)
- What does 8th Light uniquely offer that automation cannot replace?
- Is there a good frame for explaining *why* screen reader simulation is fundamentally different from the real thing (for a non-technical buyer)?
- What percentage / rough stats exist on how much automated tools miss? (Worth citing if available — and frame it as a risk signal: "they missed X% of issues.")
- Disability market size stats to include: how many users, what spending power, what conversion/retention impact of accessibility? (Need citations.)
- **B Corp nonprofit equivalent:** B Corp certification is specifically for for-profit companies. Research whether a nonprofit equivalent exists. (Came up in a conversation with Jenny — Celeste to follow up.)
- **Concrete "big hitter" WCAG violations:** Research which specific WCAG violations automated tools are known to miss that would resonate with a business reader. Use Gemini Deep Research. Goal: a short list of violations that make a reader think "Oh gosh, we might have that."

---

## Raw Notes / Brainstorm

### On the visual screen reader problem (SilkTide and similar)
The distortion is all three: what gets announced, the order of announcements, and how it sounds.
Real screen readers (NVDA, JAWS, VoiceOver) each have distinct behavior, voice characteristics, and announcement patterns.
A visual simulation flattens all of this into a single approximation that doesn't match any of them.
This means a developer or auditor relying on a simulated screen reader is testing against something that no real user experiences.

**Two failure modes — both costly:**

1. *False negatives* — the tool misses real issues.
   Real users experience friction, confusion, or complete blockers that never showed up in any report.
   The org ships thinking they're compliant. They're not.

2. *False positives* — the tool invents issues that don't exist.
   Concrete example: the SilkTide integrated screen reader flagged what appeared to be serious problems.
   Hours (potentially days at scale) were spent investigating and trying to fix them.
   When tested against a real screen reader, the problems weren't there.
   The tool was wrong. The human experience was fine. The time was gone.

Both failure modes have real costs — the second is particularly insidious because it *looks like diligence*.
You can waste enormous engineering time chasing ghosts while the actual user experience problems go unexamined.

### On LLM fixes — the nervous system problem
LLMs can follow the guidelines quite well — they understand WCAG criteria at a rule level.
What they lack is the ability to understand the *practical impact* of the specifics of a given circumstance.
They don't have human nervous systems. They cannot feel what it's like to navigate a page with NVDA and hit a confusing landmark, or to lose track of focus.
The misses aren't just "wrong rule applied" — they're subtler: a fix that is technically correct but practically disorienting, or a violation that the LLM doesn't flag because the guideline text doesn't capture the experiential failure.

### On who the specialist needs to be
Ideally: a trained accessibility engineer who also has lived disability experience.
These aren't separable qualities — they reinforce each other.
Trained engineers know the guidelines and can navigate tooling.
But lived experience means you feel the failures that tools can't detect: the disorientation, the lost context, the moment a flow breaks down in a way that's hard to articulate but immediately apparent.
Celeste is both: a disabled military veteran with accommodation needs, becoming 8th Light's a11y specialist.
This is not incidental — it is the core of the argument made flesh.
The article can speak in first person about this: "I am the thing automation is trying to replace. It can't."

### On automation vs. human validation — the false confidence trap
Automation is a force multiplier: it speeds up the work and amplifies how much can be done, how fast.
But it cannot validate the actual human experience — only a human can do that.
The danger is that automation without human validation creates false confidence.
Orgs can technically check off the list — every automated tool returns green — while still shipping an experience that is genuinely inaccessible.
This is "WCAG compliance theater": the appearance of accessibility without the substance.
True WCAG compliance requires validating what it actually *feels like* to use the product with a screen reader, keyboard only, high contrast mode, etc.

---

## Editorial Process

- **Final review:** Shawn reviews articles before they go up on the 8th Light website.
- Get his eye on a near-final draft before publishing.

