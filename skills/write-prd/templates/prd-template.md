## Authors:

**Audience:**

**Status:** Draft / In Review / Final

**Related Discovery Paper:** *(link if one exists)*

---

# Part I — The Product Problem

## 1. Define the Product

*State the purpose of this PRD and the scope of the release. A PRD is owned by Product Management and provides the business requirements for a single, shippable release (typically weeks to 2–3 months). Be concise.*

## 2. Jobs to be Done

### 2.1 Job Stories

*One job story per key customer type (max 3). Format: "When [triggering situation], I want to [motivation], so I can [outcome]." The "When" clause is a specific situational trigger — not a persona label.*

| Customer Type | Job Story |
| :---- | :---- |
| *e.g. Analyst* | *When I need to review a past test result after a configuration change, I want to know exactly what the configuration was at each point in time, so I can reconstruct the analysis accurately.* |

### 2.2 Outcome Statements

*3–6 measurable need-gaps derived from the job stories above. Format: [direction verb] + [metric/object] + [clarifier]. Each ID persists through revisions and is referenced in requirements.*

| ID | Outcome Statement | Customer Type |
| :---- | :---- | :---- |
| JTBD-OS-001 | *Minimize the time needed to [measurable object] [clarifier]* | *Customer Type* |
| JTBD-OS-002 | *Reduce the risk of [measurable object] [clarifier]* | *Customer Type* |

## 3. Determine Requirements

*List all product requirements. Every P1 requirement must reference at least one JTBD-OS-NNN ID. Use the "so that" clause to link to the job outcome.*

| ID | # | Pri | Requirement | JTBD | Acceptance Criteria |
| :---- | :---- | :---- | :---- | :---- | :---- |
| PRD-REQ-001 | 1 | P1 | *As a [customer type], I want [capability], so that [outcome linking to job story].* | JTBD-OS-001 | - Criterion 1<br>- Criterion 2<br>- Criterion 3 |

*Priority guide: P1 = must have, release blocker; P2 = important, can slip; P3 = future direction / guardrail*

## 4. Identify Assumptions & Constraints

| Key Assumptions | Key Constraints |
| :---- | :---- |
| *[ASSUMED] assumption text* | *constraint text* |

## 5. Limit the Scope of Work

*Describe what is in scope for this release. Be explicit.*

- *in-scope item 1*
- *in-scope item 2*

**Out of Scope for This Release:**

- *item 1*
- *item 2*

## 6. List Features

*Describe each feature in the release. Use sub-sections (6.1, 6.2…) for distinct features.*

### 6.1 Feature Name

*Description.*

---

# Part II — Delivery

## 7. Release Criteria

*Binary pre-ship gates only. Each criterion is a testable pass/fail condition that must be true before shipping. Do not include post-launch KPIs here — those belong in Section 8.*

- **[Criterion name]:** *testable condition*

## 8. Success Metrics

*Post-launch KPIs that define what success looks like after shipping. Each lagging indicator must be paired with a leading indicator (signal within 2–4 weeks).*

| Metric | Type | Target | Leading Indicator |
| :---- | :---- | :---- | :---- |
| *metric name* | *Lagging / Leading* | *target value* | *paired leading metric* |
