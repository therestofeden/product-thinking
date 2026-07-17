---
name: product-master-doc
description: >
  Generate a Product Master Doc following the UIE framework (Understand → Identify → Execute).
  Use when a PM has completed discovery — or has notes, prior experiments, and a rough problem space —
  and needs to produce the full structured document. Works for any domain: consumer products, B2B SaaS,
  two-sided marketplaces, ML products, infrastructure, internal tools, adtech.
  Triggers on: "write the product master doc", "generate the discovery doc", "write up what we know",
  "turn this into a discovery paper", "UIE doc for X", "product doc for [initiative]",
  "pre-PRD document for [initiative]", or any request to produce a structured discovery document
  from prior notes, a conversation, or a document the PM has shared.
  For ZMS/adtech-specific documents with auction mechanics and ML model examples, use zms-discovery-paper instead.
---

# Product Master Doc — UIE Framework

This skill generates a structured Product Master Doc for any product initiative. The framework — **Understand → Identify → Execute** — applies to consumer products, B2B SaaS, two-sided marketplaces, ML products, infrastructure, and internal tools.

A Product Master Doc is a **pre-PRD alignment tool**. Its job is to:
- State the product outcome precisely before identifying any solution
- Separate what the team knows from what it believes from what it assumes
- Surface value gaps that constitute validated opportunities
- Apply the Four Risks as a gate before any speccing begins
- Define what failure looks like — with a number — before the experiment launches

It does not design experiments in full detail. It does not commit to solutions. It creates the conditions under which good speccing can happen.

---

## Orientation: Gather Context First

Before generating anything, ask or extract from available materials:

1. **What is the initiative?** One sentence — not the solution, the thing being worked on.
2. **What system or product does it plug into?** What is the mechanism through which changes produce outcomes?
3. **What prior work exists?** Experiments, analyses, research notes, adjacent projects.
4. **What opportunities or hypotheses does the team already have?** Don't generate from scratch if the team has prior thinking.
5. **Who is the audience?** (PM + science/engineering alignment? Leadership? External?)
6. **What is the team's scope?** What do they own directly vs. co-own vs. influence?
7. **Is this a two-sided market?** Paying partners and end users with potentially misaligned interests?

If the user has shared a document, notes, or analysis — extract what you can and only ask for what's missing.

---

## Document Structure

Generate in this exact order. Do not skip sections.

---

### Header Block

```
[Initiative Name] | [Product / System Area]
Authors: [names]
Collaborators: [names]
Status: [In progress / Draft / Final]

Purpose. This Product Master Doc structures the discovery and opportunity space for [initiative].
It is not a PRD and it is not a spec. Its goal is to align the team around the right product
outcome, surface the specific value gaps that constitute validated opportunities, and gate
solutions behind a riskiest-assumption test before any engineering commitment is made.

Scope. [Team accountability boundary — what this team owns directly vs. co-owns vs. influences.]
```

---

### Step Zero: Mission Stack

Present as a four-row table before anything else. The product outcome sentence that follows must be derivable from this table — not invented independently.

| Layer | Statement |
|---|---|
| Company / Platform North Star | [what the business optimises for] |
| Product mission | [why this product exists, one sentence] |
| Success condition | [what must be simultaneously true — for all sides of the market] |
| What "failure" looks like | [what looks like success on one metric but is actually failure] |

**The failure row is non-negotiable.** In a two-sided market: the product that generates revenue on one side while degrading the experience that makes the other side valuable is in the failure condition. Name it explicitly before any opportunity is framed.

> **Consumer example:** "High engagement metrics + declining repeat purchase rate = we optimised for attention, not commerce."
>
> **B2B example:** "High contract renewal rate + low product adoption = we're renewing on relationship, not value. The churn cliff is coming."
>
> **Two-sided marketplace example:** "High attributed partner revenue + degraded end-user conversion = build trap entry. Attribution is lagging; user conversion is honest."

---

### Context: The Product Outcome

**Product Outcome:** One sentence, bolded. Derived from the Mission Stack. Format:

> *[Product] enables [customer] to [do what], such that [measurable condition], while [constraint protecting the other side of the market or the platform].*

Every word is load-bearing:
- Describes what changes in the world, not what gets shipped
- Names a specific customer segment, not "users"
- States a measurable condition in outcome terms, not output terms
- Carries a constraint — in a two-sided market, an outcome without a constraint on the other side is incomplete

**Why this framing.** [Ownership boundary: what does this team's work directly drive? What is downstream and co-owned? This tells you where to look for opportunities — only in the layer this team owns.]

**How we measure it:**

| Category | Metric(s) | Rule |
|---|---|---|
| Primary (causal) | [Incremental metric grounded in counterfactual] | If it moves, the outcome moved. Incremental > attributed > output. |
| Secondary (proxy) | [Faster-signal proxy] | Acceptable for rollout gating under stated assumptions — document the assumption. |
| Guardrail | [What must not degrade] | Elevate to co-primary when a phase concentrates most financial or platform risk. |
| Leading indicator | [2–4 week signal] | Required. A quarter without one is a quarter without a feedback loop. |

---

### U — Understand

*Deep understanding of the system, the prior evidence, and the market before identifying any opportunity.*

#### 01 The System

The core mechanism — the formula, rule, or process through which this initiative's changes would translate into outcomes.

Derive the opportunity space from the mechanism: if parameter X is wrong, what happens to which customer? If signal Y is missing, what is the downstream consequence? Be specific about direction and magnitude where available.

End with a **core question** that flows from the Product Outcome: *"Does [mechanism] currently deliver [outcome] for [customer]? If not, where specifically does it fail?"*

> **Consumer example:** "Recommendation ranking scores items by predicted CTR. When predicted CTR is decoupled from actual purchase intent — as it is for items with high browse-to-buy ratios — we surface content that generates engagement but not commerce. The question: does our ranking currently deliver purchase-quality intent, or engagement-quality intent?"
>
> **B2B example:** "Onboarding completion drives activation, which drives 90-day retention. The mechanism is linear: features adopted in week one predict whether the customer reaches their first value milestone. The question: does the current onboarding sequence deliver the right feature exposure for each customer segment, or are we routing all customers through the same path regardless of their use case?"

#### 02 What We Know

Apply **epistemic labels** to every factual claim. Non-negotiable.

- **[KNOWN]** — empirically validated (shipped A/B result, RCT, peer-reviewed finding, QA'd database number)
- **[BELIEVED]** — theory-grounded and proxy-evidenced, not directly validated at this system
- **[ASSUMED]** — implicit, unvalidated, required for the logic to hold

Organise by body of prior evidence (2.1, 2.2, 2.3...). Each subsection:
- What was done (briefly)
- What was learned — with epistemic label
- What it implies for this initiative

Apply epistemic labels to financial model assumptions too. A CVR assumption derived from adjacent data is [BELIEVED]. One with no prior measurement is [ASSUMED]. "Conservative" in the absence of any baseline is not conservative — it is an assumption wearing a haircut.

Close with a **headroom assessment**: does the team believe substantial improvement is still achievable in this direction, and why?

---

### I — Identify

*Where specifically does the product fail to deliver its stated outcome, and why? Opportunities as value gaps.*

#### 03 Opportunity Solution Tree

**Desired Outcome:** [Restate the product outcome verbatim. This is the anchor for all opportunities that follow.]

Then list numbered opportunities. Each opportunity is a **value gap** — not a feature, not a solution, not a capability the team wants to build.

**Framing discipline:**
- "Add a retention email flow" = solution. Not an opportunity.
- "Customers who complete onboarding but don't reach their first value milestone in 30 days have a 4x higher churn rate — and 60% of them never saw the one feature that correlates most strongly with retention" = opportunity. Gap named, segment named, mechanism named, consequence named.

**For each opportunity:**

> **Opportunity N: [Value gap headline — what the product gets wrong and for whom]**
>
> **The gap:** [2–4 sentences. What specifically fails? For which customer? Through what mechanism? What is the downstream consequence for that customer and for the business?]
>
> - **Evidence:** `[known / believed / assumed]` — [source + magnitude + what it directly supports]
> - **Solution:** [The specific intervention — a hypothesis, not a commitment]
> - **Four Risks** (Cagan): `[value: H/M/L]` · `[usability: H/M/L]` · `[feasibility: H/M/L]` · `[viability: H/M/L]`
> - **Riskiest assumption:** [The single assumption that, if wrong, invalidates the solution-opportunity link — not the full list, the one that kills it]
> - **Risks:** `[high / medium / low]`
>   - [Risk 1: mechanism + mitigation path, or "no mitigation identified — BLOCKER"]

**Severity rule:** Any opportunity with a High risk or High Four Risks rating and no named mitigation = **blocker**. Do not advance to Execute. Name what discovery is needed to unblock it.

**Two-sided market check:** For every opportunity — which side does it primarily serve? What is the impact on the other side? Surface any opportunity that creates value for one side at the expense of the other.

---

### E — Execute

*Prioritise interventions, design the validation approach, define decision criteria. Execute only against validated opportunities.*

#### 04 Initiative Scoring

| Solution / Intervention | Opportunity addressed | Evidence level | Expected impact | Effort | Priority |
|---|---|---|---|---|---|

- One row per solution from the OST
- Opportunity column: links explicitly back to the numbered opportunity
- Evidence level: [KNOWN] / [BELIEVED] / [ASSUMED]
- Expected impact: magnitude estimate with epistemic label — "TBD with [team]" if genuinely unknown
- Effort: Low / Medium / High with a one-line justification
- Priority: ranked relative to other solutions

If one phase concentrates most of the financial upside, name it explicitly. Prior phases exist to de-risk the high-value phase — frame them as such, not as equal steps.

#### 05 Kill Switches

For each phase of a phased rollout: a pre-agreed threshold, documented before the experiment launches, that triggers a specific action if crossed. Not "we'll monitor and adjust."

| Phase | Trigger metric | Threshold | Action if crossed | Owner |
|---|---|---|---|---|
| [Phase N — surface or mechanism] | [specific metric] | [specific number] | [pause / halt / escalate] | [name] |

An undefined kill switch threshold is an **open blocker**. It goes in the Open Risks Register at High severity with an owner and deadline.

#### 06 Experiment Design Principles

A numbered list governing how solutions will be validated. Always address:

1. **Validation approach:** What methodology fits this question? (A/B; holdout; geo-experiment; Budget Split for auction or pricing changes; qualitative interviews for usability; shadow mode for ML changes) Name which and why — matched to the causal question, not defaulted to the easiest option.
2. **Randomisation unit:** What is the correct unit? Does treating one unit affect another? Name the SUTVA violation mechanism if one exists.
3. **Success definition:**
   - Primary: causal outcome metric
   - Secondary: proxy metrics acceptable for rollout, with stated assumptions
   - Guardrails: what must not degrade — elevated to co-primary if the phase carries most risk
4. **Decision rule:** Go / no-go / extend / iterate — with specific numbers. "If primary metric improves >X% and all guardrails hold" not "if results are positive."

---

### 07 Open Risks Register

| Risk | Severity | Owner | Status | Next action |
|---|---|---|---|---|
| [Risk description] | High / Med / Low | [name] | Open / In progress / Resolved | [specific next step with deadline] |

High severity risks without a mitigation path are **blockers**, not risks to monitor. Name them as such. The highest-severity risk is usually the one the financial model depends on most — and the one most likely to be left vague.

This document is **living** until the pilot reads out. Every phase gate and risk resolution updates it.

---

### Appendix

- [Reference 1] — [what it contributes and which section it supports]
- Financial model — [assumptions labeled by epistemic type; state which assumptions the experiment must test]

---

## Tone and Formatting

- Write in **"we"** — this is a team alignment document, not a PM memo
- **[KNOWN]**, **[BELIEVED]**, **[ASSUMED]** bolded inline on every significant claim
- Opportunity headlines bolded, framed as value gaps for a specific customer
- **[value: M]** · **[feasibility: L]** etc. inline for Four Risks
- No "unlock value", "leverage synergies", "drive growth" without a named mechanism
- The document states what failure looks like before what success looks like
- Financial projections are belief systems with labeled assumptions, not forecasts

## What This Document Is NOT

- A PRD — no acceptance criteria, no implementation detail, no sprint planning
- A solution proposal — solutions appear as hypotheses only, behind validated opportunities
- A strategy deck — no market size slides, no competitive positioning
- An experiment plan — design principles only; the full experiment design is a separate document

## Output Format

Generate as well-formatted Markdown. If the user asks for a Google Doc, produce clean Markdown they can paste. If they ask for a Word doc, the docx skill can convert it.
