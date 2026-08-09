---
name: write-prd
description: >
  Write a Product Requirements Document (PRD) from existing material or a structured interview.
  Integrates the Jobs to be Done (JTBD) framework — job stories (Christensen situational format)
  plus Ulwick outcome statements with traceable IDs — before requirements are written.
  Produces two outputs: a PRD markdown file and a publishable article.
  Use when the user asks to "write a PRD", "draft a PRD", "create a product requirements doc",
  "turn this into a PRD", or invokes "write-prd".
user-invocable: true
allowed-tools: [TaskCreate, TaskUpdate, AskUserQuestion, Read, Write]
---

Transform raw material, an existing spec, or a structured interview into a PRD with JTBD traceability, plus a publishable article. The JTBD gate (Section 2) is mandatory — outcome statements are confirmed before any requirement is written.

**The core thesis:** Requirements without a named job are build-trap entry points. A job story + outcome statements force "what are we hired to do?" before "what are we building?" — closing the gap between discovery and delivery.

**What you produce:**
1. `product/<initiative>/<slug>-prd.md` — PRD with JTBD-OS-NNN requirement traceability, structured in 8 sections:
   - Part I: 1. Define the Product · 2. Jobs to be Done · 3. Determine Requirements · 4. Identify Assumptions & Constraints · 5. Limit the Scope of Work · 6. List Features
   - Part II: 7. Release Criteria · 8. Success Metrics
2. `product/<initiative>/<slug>-article.md` — publishable product-practitioner article derived from the PRD

Always create a task list with these steps so the user knows what you will do:
0. Initialise session state
1. Gather input and orient
2. JTBD gate — produce and confirm job stories + outcome statements
3. Write requirements (Section 3) with JTBD traceability
4. Write remaining sections (1, 4, 5, 6, 7, 8)
5. Write PRD file
6. Write article file

---

## Step 0 — Initialise Session State

Determine the initiative slug: lowercase, hyphens, no spaces (e.g. "Ghost Ads v2" → `ghost-ads-v2`).

If unclear, ask: "What should I name this PRD? (used as the filename, e.g. `my-initiative`)"

Store `PRD_SLUG`. Output files:
- `product/<initiative>/<PRD_SLUG>-prd.md`
- `product/<initiative>/<PRD_SLUG>-article.md`

Create `product/<initiative>/prd-session-state.md`:

```markdown
# PRD Session State

## Output files
- PRD: product/<initiative>/<PRD_SLUG>-prd.md
- Article: product/<initiative>/<PRD_SLUG>-article.md

## Source material
- File: [path or "interview"]

## Initiative slug
PRD_SLUG: 

## JTBD decisions
<!-- Record confirmed job stories and outcome statement IDs here -->

## Requirements decisions
<!-- Record priority decisions and JTBD links confirmed by the user -->

## Open questions (deferred)
<!-- TBDs not yet resolved -->

## Step progress
- [ ] Step 1: Input gathered
- [ ] Step 2: JTBD section confirmed
- [ ] Step 3: Requirements validated
- [ ] Step 4: Remaining sections complete
- [ ] Step 5: PRD file written
- [ ] Step 6: Article file written
```

If this session is a continuation (file already exists), read it first to recover `PRD_SLUG` and resume from where it left off.

---

## Step 1 — Gather Input and Orient

### Path A: Existing material

If the user provides a document, URL, file path, or pastes content:
- Read it in full before doing anything else
- Check for an existing Discovery Paper in `product/<initiative>/` — if found, read it too; the OST desired outcome seeds the job story "When" clause

Diagnose structural gaps — state what you find before proceeding:

| Gap | What to look for |
|---|---|
| Missing customer definition | Who specifically is the customer? Is there a concrete role example? |
| Solution masquerading as requirement | Does the doc describe what to build rather than what job to accomplish? |
| No situational trigger | Can you identify a specific "When" situation for a job story? If not, flag as discovery gap |
| Output metrics in success section | Are success metrics outputs (shipped/deployed) rather than outcomes (behaviour changed)? |

### Path B: No existing material — interview

Ask one question at a time:
1. What are you building?
2. Who is the customer? (concrete example: "a brand manager at a consumer goods company", not "users")
3. What specific situation triggers their need? (this becomes the "When" clause)
4. What business value does this deliver?
5. What are the must-have capabilities?
6. What is explicitly out of scope for this release?

Accept partial answers. Gaps become open questions in Section 4 and deferred items in session state.

After gathering input, update `product/<initiative>/prd-session-state.md`: record source file path, mark Step 1 complete.

---

## Step 2 — JTBD Gate (mandatory)

**This step must be confirmed by the user before any requirements are written.**

**Start by reading `product/<initiative>/prd-session-state.md`** to recall any decisions already made.

### 2.1 Draft Job Stories

Write one job story per key customer type (max 3). Format:

> `When [triggering situation], I want to [motivation], so I can [outcome].`

Rules:
- The "When" clause is a **specific situational trigger** ("When I need to reconstruct a past test configuration after a change was made"), not a persona label ("When I am an analyst")
- The "I want to" is the immediate motivation — what the person is trying to do right now
- The "so I can" is the downstream outcome — what they can accomplish as a result

**If you cannot write a specific "When" clause**, surface this as a discovery gap:
> "The job story 'When' clause is missing — this usually means the customer situation hasn't been observed directly. I can write a hypothesis job story, but flag it as [ASSUMED]. Do you want to proceed with a hypothesis, or pause for research first?"

### 2.2 Draft Outcome Statements

Derive 3–6 measurable need-gaps from the job stories. Format:

> `[direction verb] + [metric/object] + [clarifier]`

Direction verbs: Minimize, Reduce, Increase, Improve, Eliminate, Ensure.

Assign IDs: JTBD-OS-001, JTBD-OS-002… These IDs persist through all revisions.

Example:
| ID | Outcome Statement | Customer Type |
|---|---|---|
| JTBD-OS-001 | Minimize the time needed to reconstruct test configuration state at any historical point | Analyst |
| JTBD-OS-002 | Reduce the risk of applying the wrong randomization unit to an active test | Campaign Manager |

**Cross-reference gate:** Any job story labeled `[ASSUMED]` must have a corresponding `[ASSUMED]` entry in Section 4 that names the discovery debt explicitly (e.g. "Customer situation in job story X is assumed — not yet observed directly"). The two labels create a traceable record of how much of the PRD rests on validated vs. unvalidated claims.

**Present Section 2 (job stories + outcome statements) to the user. Wait for confirmation before proceeding.**

After confirmation: update `product/<initiative>/prd-session-state.md` — record confirmed JTBD IDs, mark Step 2 complete.

---

## Step 3 — Requirements (Section 3)

**Start by reading `prd-session-state.md`** to anchor on confirmed JTBD IDs.

Write the requirements table. For every requirement:

**Requirement format:**
> `As a [customer type], I want [capability], so that [outcome linking to job story].`

**Priority:**
- P1 — Must have; release blocker
- P2 — Important; can slip to next release
- P3 — Guides direction; future capability or architectural guardrail

**JTBD column:** Every P1 requirement must reference at least one JTBD-OS-NNN ID. Before presenting:
- Count P1 requirements with no JTBD link
- If any exist, flag them: "PRD-REQ-NNN has no JTBD link. Either link it to an existing outcome statement or add a new outcome statement for it."

**Acceptance criteria:** ≥3 independently testable criteria per P1 requirement. Use "does", "returns", "displays", "enforces" — not "should".

Assign sequential IDs: PRD-REQ-001, PRD-REQ-002…

Present the requirements table. Wait for confirmation on priority assignments before proceeding.

After confirmation: update `product/<initiative>/prd-session-state.md`, mark Step 3 complete.

---

## Step 4 — Remaining Sections

**Section 3 (Requirements) is already confirmed. Now fill the remaining sections.**

**Start by reading `product/<initiative>/prd-session-state.md`** to work from confirmed artifacts.

Fill sections 1, 4, 5, 6, 7, 8. Discipline checks:

**Section 1 (Define the Product):** One paragraph. What is this release, and what does it solve? No implementation detail.

Two failure modes to catch and rewrite before proceeding:
- **Press-release language** — phrases like "unlock new value", "streamlined experience", "empower users" carry no information. If you cannot replace it with a mechanism ("reduces configuration errors by removing the manual step"), delete it.
- **System design language** — sentences like "adds an audit log table to the configuration service" belong in a tech spec, not a PRD. If the sentence describes what to build rather than what job to accomplish, it is in the wrong document.

**Section 4 (Assumptions & Constraints):** Apply epistemic labels — `[ASSUMED]` for unvalidated, `[BELIEVED]` for theory-grounded, `[KNOWN]` for experimentally validated. Any `[ASSUMED]` job story from Section 2 must have a corresponding entry here naming the discovery debt.

**Section 5 (Scope):** List what is explicitly in scope, then an "Out of Scope" block. If anything from the original input was dropped, it must appear in Out of Scope.

**Section 6 (Features):** One sub-section per feature. Describe what it does; link back to requirements by ID.

**Section 7 (Release Criteria):** Binary pre-ship gates only. If an outcome metric appears here, move it to Section 8 and note the move.

**Section 8 (Success Metrics):** Each lagging indicator must be paired with at least one leading indicator (signal within 2–4 weeks). Format as a table with columns: Metric / Type (Lagging or Leading) / Target / Leading Indicator.

---

## Pre-Write Quality Checklist

Run this before writing any output files:

- [ ] Every P1 requirement has ≥3 testable acceptance criteria
- [ ] Every P1 requirement links to at least one JTBD-OS-NNN ID
- [ ] Job story "When" clause is a situational trigger, not a persona label
- [ ] Outcome statements follow: direction verb + metric/object + clarifier
- [ ] Section 7 contains only binary pre-ship gates (no outcome metrics)
- [ ] Section 8 pairs each lagging KPI with a leading indicator
- [ ] No placeholder text in final PRD output
- [ ] Article "How We Define Success" ends with: "The riskiest assumption behind this release is [X]."

---

## Step 5 — Write PRD File

**Start by reading `product/<initiative>/prd-session-state.md`** — use confirmed written artifacts, not conversation memory.

Write `product/<initiative>/<PRD_SLUG>-prd.md` using `templates/prd-template.md` as scaffold.

Do not leave placeholder italics in the final output — replace every template placeholder with real content.

After writing, confirm:
> "PRD written: `product/<initiative>/<PRD_SLUG>-prd.md` — [N] requirements (PRD-REQ-001 to PRD-REQ-NNN), [N] JTBD outcome statements (JTBD-OS-001 to JTBD-OS-NNN)"

Mark Step 5 complete in session state.

---

## Step 6 — Write Article File

Produce a publishable markdown article for a product practitioner audience. This is not a summary of the PRD — it is a structured piece written to be read standalone.

**Article structure:**

```
# [Initiative Name]: [Short hook — what problem this solves]

## Context

[2–3 paragraphs: what the system does today, what gap or limitation this initiative addresses, why now. Use epistemic posture: distinguish what is known from what is believed.]

## The Job

[The job story(ies) from Section 2.1 as prose narrative. Why this situation matters. What the customer is trying to accomplish and why the current product fails them in that moment.]

## Outcome Statements

[The Ulwick outcome statements from Section 2.2 as a reference block. Brief intro sentence, then the table verbatim from the PRD.]

## The Approach

[Key requirements and design decisions in plain language. Focus on the "why" behind the choices, not the acceptance criteria. 3–5 paragraphs.]

## How We Define Success

[Section 7 release criteria as prose. Section 8 success metrics as a table. Include the leading/lagging pairing. End with: "The riskiest assumption behind this release is [X]."]
```

Write to `product/<initiative>/<PRD_SLUG>-article.md`.

Mark Step 6 complete in session state.

---

## Relationship to Other Skills

| Skill | When to use |
|---|---|
| `product-discovery` | Before this skill. OST desired outcome feeds the job story "When" clause. |
| `write-prd` | This skill. After discovery (or when discovery is in-progress with a hypothesis). |

A Discovery Paper is not required before a PRD. If one exists, the skill reads it to seed job stories and outcome statements. If none exists, the skill creates a hypothesis job story and flags it as `[ASSUMED]`.
