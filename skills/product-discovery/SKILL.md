---
name: product-discovery
description: Use when a PM needs to validate a product initiative before speccing or building — especially when a solution has been proposed before the opportunity is proven, when the financial model is being treated as a forecast, when success metrics exist but failure thresholds do not, or when the team is about to commit engineering to something that hasn't cleared discovery. Works for any domain.
---

# Product Discovery — From Mission to Product Master Doc

## Overview

This skill makes you a structured thinking partner for a PM doing discovery. You walk through five sequential steps, ask hard questions at each one, surface assumptions the PM hasn't examined, and assemble a Product Master Doc from what emerges. You do not fill in a template. You run a dialogue that produces the template as an output.

**The core principle:** A product outcome is only valid if it is *derivable* from the company's mission and North Star. An opportunity is only valid if it is a *value gap*, not a feature request. A financial model is only valid if its claims are *labeled by what kind of claim they are*. And no phase launches without a pre-agreed definition of failure.

**Works for any domain.** Consumer apps, B2B SaaS, two-sided marketplaces, internal tools, ML products, infrastructure. The questions adapt; the structure does not.

---

## The Five Steps

Run them in order. Do not skip to step 3 because the PM already has an outcome statement. The mission stack in step 1 is what makes that outcome statement *earn* its place rather than assert it.

```
Step 1 → Mission & North Star alignment
Step 2 → Epistemic inventory (what kind of claims are we making?)
Step 3 → Product outcome definition + metric hierarchy
Step 4 → Opportunity Solution Tree (value gaps, not features)
Step 5 → Kill switches and the Open Risks Register
         ↓
         Assemble Product Master Doc
```

---

## Step 1: Mission → North Star → Product Outcome Stack

**What you do:** Before the PM names a single opportunity, establish why the product exists and what the company optimises for. In a two-sided market this step is non-optional — the interests of each side are in tension and must be named explicitly.

**Ask the PM:**

1. What is the mission of your product? Not what it does — why it exists. What would be worse in the world if your team stopped showing up?
2. What is your North Star metric? Is it causally connected to the company's North Star, or is it a local metric that looks good in team reviews but is orthogonal to what the business actually cares about?
3. If your product serves more than one type of customer (end users *and* paying partners, for example): what does success look like for each side? Where are those interests in tension?

**Build this table with the PM before anything else:**

| Layer | Statement |
|---|---|
| Company North Star | [what the business optimises for] |
| Product mission | [why this product exists, in one sentence] |
| Success condition | [what must be simultaneously true for both sides of the market] |
| Failure condition | [what looks like success on one metric but is actually failure] |

**The failure condition row is the one most PMs leave blank.** A product that generates impressive revenue while quietly degrading the end-user experience that makes that revenue possible is in the failure condition. Name it before moving forward.

**Gate:** The product outcome statement in Step 3 must be *derivable* from this table. If it isn't, it goes back here.

---

## Step 2: Epistemic Inventory — Map vs. Territory

**What you do:** Before the PM shows you any data, ask them to label every significant claim in the initiative with one of three labels. This is the alignment mechanism between the map (what the document says) and the territory (what is actually true).

**The three labels:**

- **[KNOWN]** — empirically validated. A randomised controlled experiment with a clean holdout. A peer-reviewed finding. A number from a database that has been QA'd. If someone challenges it, you can show them the methodology.
- **[BELIEVED]** — theory-grounded and proxy-evidenced. You have a mechanism and analogous evidence, but you have not validated it directly at this system or at this scale.
- **[ASSUMED]** — implicit and unvalidated. Required for the logic to hold, but not yet examined. These are the claims that will hurt you most if they turn out to be wrong.

**Ask the PM to label:**
- The core evidence for the problem existing
- Every major claim in the financial model
- The CVR or conversion assumptions in any projection
- Any "pilot result" or "early signal" cited as validation
- The claim that the solution will work for the stated opportunity

**The rule:** An [ASSUMED] claim cannot be the foundation of a go/no-go decision. It needs at minimum a cheapest-possible test that could make it [BELIEVED] before any engineering commitment.

**Common failure pattern to surface:** Financial models routinely contain [ASSUMED] CVR figures presented as conservative estimates. "Conservative" in the absence of any baseline data is not conservative — it is an assumption wearing a haircut. Name it.

---

## Step 3: Product Outcome Definition + Metric Hierarchy

**What you do:** Write one sentence that defines what the product is supposed to accomplish. This sentence is not invented — it is derived from the Step 1 table. Then build a metric hierarchy that flows from it.

**The outcome sentence format:**

> *[Product] enables [customer] to [do what], such that [measurable condition], while [constraint that protects the other side of the market or the platform].*

Every word is load-bearing. Push back if:
- The sentence describes what gets shipped rather than what changes in the world ("launches X" = output, not outcome)
- The measurable condition is an output metric (features shipped, experiments run, models deployed)
- There is no constraint — in a two-sided market, an outcome that optimises one side without naming the other is incomplete

**The metric hierarchy:**

| Category | Role | Rule |
|---|---|---|
| Primary (causal) | Proves the outcome sentence is true | Must be grounded in a counterfactual — incremental metrics over attributed ones |
| Secondary (proxy) | Acceptable for rollout gating within an experiment window | Document the assumption that connects it to the primary |
| Guardrail | Must not degrade | In high-risk phases, the guardrail is co-primary — not secondary |
| Leading indicator | Gives signal in 2–4 weeks | Required — a quarter without a leading indicator is a quarter without a feedback loop |

**Ask:** For every metric on the PM's list — is this an outcome or an output? If it is an output, what outcome does it proxy for, and what assumption connects them?

---

## Step 4: Opportunity Solution Tree

**What you do:** Map the opportunity space from the outcome downward. Every opportunity is a *value gap* — a specific place where the product fails to deliver its stated outcome for a specific customer segment, with a hypothesis about why. It is not a feature. It is not a capability the team wants to build.

**The framing test:**
- "Add cart placement" — solution. Not an opportunity.
- "53% of purchase-bound events occur on a surface the product cannot reach, leaving the highest-intent moment in the customer journey completely unaddressed" — opportunity. Names the gap, the customer state, the mechanism, the downstream consequence.

**For each opportunity the PM identifies, require:**

1. **The gap:** What specifically fails, for whom, through what mechanism, with what downstream consequence.
2. **The evidence:** Labeled [KNOWN], [BELIEVED], or [ASSUMED].
3. **The Four Risks** (Cagan — *Inspired*): Rate Value / Usability / Feasibility / Viability as High / Medium / Low. Any High rating without a named mitigation path = blocker to speccing. Do not advance.
4. **The riskiest assumption:** The single assumption that, if wrong, invalidates the solution-opportunity link entirely. Not the full list — the one that kills the proposal if it fails.

**Gate:** An opportunity with [ASSUMED] evidence and a High Four Risks rating does not advance to the Execute section. It needs discovery first. Name what discovery is required and what would make it [BELIEVED].

**In a two-sided market:** For every opportunity, ask which side of the market it primarily serves, and what the impact is on the other side. An opportunity that creates value for partners at the expense of end users is not a valid opportunity — it is a failure condition entry point (see Step 1).

---

## Step 5: Kill Switches and the Open Risks Register

**What you do:** Define failure before success. For every phase of a phased rollout, require a pre-agreed kill switch threshold — a specific number, documented before the experiment launches, that triggers a specific action if crossed.

**The kill switch requirement:**

For each phase, the PM must specify:
- Which metric triggers the kill switch
- What threshold value activates it
- What action it triggers (pause / halt permanently / adjust configuration)
- Who owns the decision

**Push back hard on:**
- "We'll monitor and adjust" — this is not a kill switch, it is a promise to have a meeting
- Kill switches that exist but have no number — "if checkout abandonment increases significantly" is not a kill switch
- Kill switches that are defined post-experiment — by then the team is anchored to sunk cost

**The Open Risks Register:**

Every significant risk in the document goes into a register with: severity (H/M/L), owner, status, next action. High-severity risks without a named mitigation path are **blockers** — not risks to monitor. Name them as blockers explicitly.

**The highest-severity risk is usually the one the financial model depends on most.** If 79% of projected revenue lives in Phase 3 (or Phase N), and Phase 3 has an unproven assumption with no kill switch threshold defined, that is not a risk — it is a structural gap in the initiative that must be closed before anyone commits to building.

---

## Assembling the Product Master Doc

Once all five steps are complete, assemble the document in this order. Do not skip sections. Each has a specific job.

```
Header block
  — Title, authors, date, status
  — Open questions table (unresolved items from discovery, with owner)

Purpose and Scope
  — What this doc IS (discovery paper, pre-spec alignment)
  — What this doc is NOT (PRD, spec, engineering commitment)
  — Scope boundary: what the team owns directly vs. co-owns vs. influences

Context: Defining the Product Outcome
  — The outcome sentence (Step 3)
  — Why this framing (ownership boundary, what team directly drives)
  — Metric hierarchy table (primary / secondary / guardrail / leading)

Understand
  — 01 The System: the mechanism through which changes produce outcomes
  — 02 What We Know: epistemic inventory (Step 2), organised by body of evidence
      Each claim labeled [KNOWN] / [BELIEVED] / [ASSUMED]
      Each subsection: what was done, what was learned, what it implies

Identify
  — 03 Opportunity ↔ Solution Tree (Step 4)
      Desired outcome box (verbatim from Step 3)
      Each opportunity: gap / evidence / Four Risks / riskiest assumption / risks

Execute
  — 04 Initiative Scoring: table comparing solutions on evidence level,
      expected impact, effort, priority
  — 05 Experiment Design Principles: validation methodology, randomisation unit,
      SUTVA considerations, success definition hierarchy, guardrails, decision rules
  — 06 Kill Switches (Step 5): per-phase threshold table
  — 07 Open Risks Register: severity / owner / status / next action

Appendix
  — Financial model with epistemic labels on every assumption
  — Source materials
  — Glossary
```

---

## Tone and Epistemic Standards

- Write in "we" — this is a team alignment document, not a PM memo
- Every causal claim carries its label: **[KNOWN]**, **[BELIEVED]**, **[ASSUMED]**
- No "unlock value", "drive growth", "leverage synergies" without a named mechanism
- Financial projections are labeled as belief systems, not forecasts, unless the evidence warrants [KNOWN]
- The document states what failure looks like before it states what success looks like

---

## Common Failures This Skill Prevents

| Failure | What it looks like | What prevents it |
|---|---|---|
| Solution before opportunity | Initiative framed as "build X" not "gap Y exists" | OST framing in Step 4 |
| [ASSUMED] presented as [KNOWN] | Financial model treated as forecast | Epistemic labeling in Step 2 |
| Output metric as success | "We shipped it" = success | Outcome definition in Step 3 |
| No failure threshold | "We'll monitor" instead of a number | Kill switches in Step 5 |
| North Star drift | Product optimises local metric disconnected from company metric | Mission stack in Step 1 |
| Two-sided market optimised one-sided | Partner revenue at expense of end-user experience | Failure condition row in Step 1 table |
| Premature speccing | PRD written before opportunity is validated | Four Risks gate in Step 4 |

---

## Framework References

- **Melissa Torres — *Continuous Discovery Habits*:** Opportunity Solution Tree structure. Opportunity-first framing. Solutions as hypotheses behind validated opportunities.
- **Marty Cagan — *Inspired*:** Four Risks (Value, Usability, Feasibility, Viability) as the gate before speccing. Missionary vs. mercenary teams.
- **Melissa Perri — *Escaping the Build Trap*:** Outcome over output. Strategy deployment chain (Vision → Strategic Intent → Initiative → Option). The build trap is entered at the moment of premature commitment, not at the moment of building.
