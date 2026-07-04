# How I Write a PRD — and Why I Put the Job Before the Requirements

*A walkthrough of the PRD format I use after discovery is done: seven sections, a mandatory Jobs to be Done gate, and a distinction between release criteria and success metrics that most PRDs collapse into one.*

---

There is a failure mode that sits between good discovery and good delivery. You have done the work — you have an Opportunity Solution Tree, epistemic labels on your claims, the riskiest assumption named. You know what you are building and roughly why. And then you open a blank document to write the PRD and the first thing you do is list requirements.

The requirements come from the solution, not from the job. They describe what the system should do. They do not say who will hire this capability, in what situation, or what they are trying to accomplish that they currently cannot. The acceptance criteria are testable. The connection to the customer's actual problem is implicit, assumed, or missing entirely.

I have written PRDs this way. I have reviewed dozens more that were written this way. The pattern is not laziness — it is that most PRD formats don't ask the job question. They have a "problem statement" section, which tends to collapse the opportunity and the solution into a single paragraph. And then they go straight to requirements.

The format I use now puts the job question as a mandatory gate between the problem statement and the requirements. You cannot write requirements until you have answered: what situation causes the customer to need this, and what specific outcomes does a good solution have to produce? Those answers become the JTBD section — Section 2 of the seven-section structure — and every P1 requirement traces back to a numbered outcome statement in that section.

This is what the format looks like and why each part is structured the way it is.

---

## The Seven Sections

The PRD has two parts: the product problem and the delivery commitments.

**Part I — The Product Problem**

1. Define the Product
2. Jobs to be Done
3. Determine Requirements
4. Identify Assumptions & Constraints
5. Limit the Scope of Work

**Part II — Delivery**

6. Release Criteria
7. Success Metrics

The JTBD section (2) sits deliberately between the product definition and the requirements. Section 1 states what the release is and what it solves. Section 2 forces the job question. Section 3 writes requirements that trace back to Section 2. You cannot credibly fill in Section 3 until Section 2 is confirmed.

One thing this format does not include: a feature list. Features are the answer the design and engineering teams produce in response to the PRD — they belong in a solution design or a tech spec, not in the document that defines the problem. A PRD that lists features has started answering its own question before the question is fully formed. Part I ends at requirements; what to build in order to satisfy those requirements is a downstream decision.

---

## Section 1: Define the Product

The first section has a single job: state what the release is, who it is for, and what problem it closes — in one paragraph, with no implementation detail.

This is harder to write than it sounds. There are two common failure modes.

The first is press release language: "This release will enable our partners to unlock new value through a streamlined configuration experience." This sentence contains no information. It does not state who is affected, what they currently cannot do, or what the release changes. It sounds like a product definition. It is a commitment to nothing.

The second is system design language: "This release adds an audit log table to the experiment configuration service, with a change-tracking layer that persists previous and current state alongside a timestamp and change source." This sentence is accurate. It describes what engineering is building. It is not a product definition — it is a technical specification that has been moved to the wrong document.

A product definition states the customer situation, the gap this release closes, and the scope boundary. It should be readable by someone who does not know the technical implementation and unambiguous to someone who does.

For a configuration tracking release, a well-formed Section 1 might read:

> *Experiment Configuration History gives analysts and campaign managers a complete, point-in-time record of how any test was configured at any moment during its run. Today, when a configuration changes mid-test, there is no way to know what the parameters were at a given point — analyses are run against the current configuration, not the historical one. This release closes that gap. It does not include a configuration comparison UI or a notification system for changes; those are separate releases.*

Three things are in that paragraph: who benefits, what they currently cannot do, and what is not in this release. The third — the scope boundary — anticipates the questions that arise in every first PRD review and answers them before they are asked.

Writing the scope boundary in Section 1 also performs a different function: it forces the author to have made a scope decision before writing. If you cannot state what is out of scope in the opening paragraph, the scope has not been decided yet. That is useful information.

---

## Section 2: Jobs to be Done — the Gate

Section 2 has two sub-layers. The first draws on Clayton Christensen's work; the second on Tony Ulwick's.

**2.1 — Job Stories (Christensen)**

A job story captures the situation in which the customer hires the product. The format is:

> *When [triggering situation], I want to [motivation], so I can [outcome].*

The "When" clause is the hardest part to write well. The instinct is to write a persona — "When I am an analyst" — which tells you nothing about when the need actually arises. The job story is situational, not demographic. A good "When" clause names a specific circumstance: "When I need to review the results of a past test after the configuration has been modified mid-run, I want to reconstruct exactly what the parameters were at each point in time, so I can produce an analysis that reflects what actually happened rather than the current state of the configuration."

That is a different kind of claim than "analysts need audit logs." It specifies the triggering situation (reviewing past results after a configuration change), the immediate motivation (reconstruct historical state), and the downstream outcome (accurate analysis). It is the kind of claim that, if you can't write it, usually means the opportunity hasn't been validated through direct customer contact — you are working from a hypothesis about what the customer needs, not a story you have heard them tell.

When I can't write a specific "When" clause, I write a hypothesis job story and label it [ASSUMED]. That is honest. It also tells the team exactly what discovery work is still owed before the requirements can be considered validated.

**2.2 — Outcome Statements (Ulwick)**

The job stories establish the situation. The outcome statements operationalize it into measurable need-gaps. Ulwick's format is:

> *[direction verb] + [metric/object] + [clarifier]*

Direction verbs: Minimize, Reduce, Increase, Improve, Eliminate, Ensure.

For the same example, the outcome statements might look like this:

| ID | Outcome Statement | Customer Type |
|---|---|---|
| JTBD-OS-001 | Minimize the time needed to reconstruct test configuration state at any historical point | Analyst |
| JTBD-OS-002 | Reduce the risk of applying the wrong randomization unit to an active test | Campaign Manager |
| JTBD-OS-003 | Eliminate the possibility of undetected configuration changes invalidating a running test | Analyst |

These IDs persist through the entire document. They are the traceability layer.

The Ulwick outcome statement is often called clinical. That is a feature. Requirements documents accumulate adjectives — "flexible", "robust", "seamless" — that sound good and measure nothing. An outcome statement like "Minimize the time needed to reconstruct test configuration state at any historical point" is directly connected to a measurable condition: either the analyst can reconstruct the state in a reasonable time or they cannot. You can write acceptance criteria against it. You can design an experiment to test whether it has been achieved.

---

## Section 3: Requirements with Traceability

The requirements table has one column that most PRD formats do not include: JTBD.

| ID | # | Pri | Requirement | JTBD | Acceptance Criteria |
|---|---|---|---|---|---|
| PRD-REQ-001 | 1 | P1 | As a campaign analyst, I want to query the complete configuration history for any test by date, so that I can produce analyses that reflect the actual configuration at the time of observation. | JTBD-OS-001, JTBD-OS-003 | - Does return all configuration states for a given test ID ordered by timestamp<br>- Does include the change source and timestamp for each state transition<br>- Does allow point-in-time reconstruction for any date within the test window |

The JTBD column creates a forcing function. Before I finalize the requirements, I count P1 requirements with no JTBD link. If any exist, I either link them to an existing outcome statement or I ask: why is this a P1 if it doesn't address a named outcome? Usually the answer is that it addresses an outcome that wasn't captured in Section 2 — which means going back to add an outcome statement. The requirement doesn't get dropped; the traceability gets built.

This stops a particular failure mode: requirements that arrive because of how the system is being built, not because of a customer job. A P1 requirement that can't be linked to a customer outcome is often a technical implementation decision that has been promoted to a product requirement. It may be correct — but it should be consciously recognized as such, not obscured by its position in the requirements table.

---

## Section 4: Identify Assumptions & Constraints

Section 4 captures what the team believes to be true that has not been confirmed. Most PRDs have an assumptions section. Most assumptions sections are disclaimers — a list of things written so that the author can claim they were acknowledged, not so that the team can act on them.

The difference between a disclaimer and a working assumption is epistemic status. An assumption you believe to be probably true based on evidence is a different kind of claim than an assumption you are making because you need to make some assumption to proceed. Treating them identically — putting them in the same list with the same weight — obscures the actual risk profile of the release.

The format I use applies a three-level label to every item in Section 4:

**[KNOWN]** — confirmed by direct evidence. A user study, a data pull, a decision from a named stakeholder. You can cite the source. If challenged, you can point to the evidence.

**[BELIEVED]** — grounded hypothesis. You have indirect evidence or strong inference. You are not certain, but you have a reason for the belief that goes beyond "this seems right." A [BELIEVED] item is the kind of claim you would bet on — but you would want to validate it before the next major decision depends on it.

**[ASSUMED]** — required but unvalidated. You need this to be true for the release to make sense, but you do not have evidence for it. An [ASSUMED] item is honest about its epistemic status: it is a bet with unknown odds.

For the configuration tracking example, Section 4 might look like this:

| ID | Label | Assumption / Constraint | Implication if wrong |
|---|---|---|---|
| ASM-001 | [KNOWN] | v1 experiment tests use a fixed configuration after launch — no mid-test changes are permitted by the current UI | No backward-compatibility concern for v1 |
| ASM-002 | [BELIEVED] | Analysts currently reconstruct historical configuration manually using Slack messages and spreadsheets | If wrong, the primary workflow hypothesis is invalid — needs validation before Section 3 can be considered confirmed |
| ASM-003 | [ASSUMED] | The configuration change volume is low enough that a flat audit log table will not require partitioning at launch | If wrong, performance constraints change the technical approach — needs a data pull from engineering before final sign-off |

The "Implication if wrong" column is required. An assumption without an implication is a fact you are not sure about. An assumption with an implication is a decision point: if this turns out to be false, here is what changes. That is the version that is useful to engineering when scoping, to product when deciding what to validate, and to the team when a post-launch finding contradicts a pre-launch assumption.

[ASSUMED] items in Section 4 also interact with the job story labeling in Section 2. If a job story is labeled [ASSUMED] — meaning the team doesn't have direct evidence of the triggering situation — there should typically be a corresponding [ASSUMED] item in Section 4 that makes the discovery debt explicit. The two labels create a traceable record of how much of the PRD rests on validated versus unvalidated claims.

---

## Section 5: Limit the Scope of Work

Section 5 is a formal in-scope / out-of-scope list. Its purpose is to make explicit the decisions that were made when the release was defined — including the things that were considered and deliberately excluded.

There is one rule that distinguishes a working scope section from a formality: anything that was part of the original discussion and was dropped must appear in Out of Scope. Not removed silently. Not left off because it didn't make it into the requirements. Named explicitly, with a brief note on why it was excluded.

This rule prevents what I call the silent de-scope — the version of scope reduction where items disappear from the document without acknowledgment. Silent de-scoping is how scope debt accumulates. A stakeholder who saw the initial proposal remembers the notification system being part of the release. The notification system is not in the PRD, but it is not listed as out-of-scope either. Three months after launch, the question arrives: where is the notification system? The answer is "we de-scoped it" — but that decision was never recorded, so the conversation replays from the beginning.

A scope section for the configuration tracking example might look like this:

**In Scope**
- Point-in-time configuration retrieval for any test created after launch
- Complete audit trail for configuration changes: previous state, new state, timestamp, change source
- Backward compatibility for all existing v1 experiment tests

**Out of Scope**
- Configuration comparison UI — excluded from this release; may be addressed in a follow-on after analyst adoption is measured
- Change notification system — requires a separate notification infrastructure decision; tracked separately
- Retroactive audit trail for tests created before launch — technically infeasible without a migration; recorded as a known gap

The out-of-scope items do not need to be long. They need to exist. The goal is that anyone who reviews the PRD — now or six months from now — can read the out-of-scope list and understand not just what was excluded but why it was excluded and whether there is a plan for it.

Section 5 also performs a function during requirements review. If a stakeholder proposes adding a requirement that is on the out-of-scope list, the conversation is different: the de-scoping decision has already been made and documented. The question is no longer "should we add this?" but "should we revisit the scope decision?" Those are different conversations, and the second one is more honest about what is actually being asked.

---

## Section 6 vs Section 7: Release Criteria and Success Metrics

Most PRDs I have seen collapse these two concerns into one. "Success metrics" or "definition of done" serves as both the ship gate and the post-launch KPI. They are different things and the confusion between them is a significant source of misaligned expectations.

**Section 6 — Release Criteria** is a binary gate. Every criterion is a testable pass/fail condition that must be true before shipping. The audience is engineering and QA. The question is: is the system ready? Not: has the initiative succeeded?

For the configuration tracking example:
- **Configuration storage:** All test configuration parameters (holdout size, premises, countries, randomization unit) are persisted and retrievable for all tests created after launch.
- **Change tracking:** Configuration changes are logged with complete audit information — previous state, new state, timestamp, change source — and no change is observable in the system without an audit record.
- **Backward compatibility:** All existing v1 experiment tests continue to operate without degradation.

These are binary. Either the audit record is complete or it isn't. Either v1 tests continue to work or they don't. There is no "mostly".

**Section 7 — Success Metrics** is a post-launch KPI table. The audience is product and business stakeholders. The question is: is the initiative delivering the outcomes we designed it for?

| Metric | Type | Target | Leading Indicator |
|---|---|---|---|
| % of historical test configurations accurately reconstructable | Lagging | 100% for tests run after launch | Analyst support tickets citing configuration gaps (target: zero) |
| Time to reconstruct test configuration at any historical point | Lagging | < 2 minutes self-serve | API query latency on configuration history endpoint |
| Randomization unit errors in active tests | Lagging | Zero post-launch | Configuration validation errors caught at save time |

The leading indicator column is required. A lagging indicator without a paired leading indicator is a metric you will check after the quarter is over. "100% accurately reconstructable" is a number you can verify — but the event that would tell you mid-quarter that something is wrong is the analyst support ticket rate. Pair the lagging metric with the signal that arrives earlier.

The separation between Section 6 and Section 7 also prevents a specific confusion at launch: declaring a product successful because the release criteria passed. A product can ship cleanly — every criterion green, no regressions, full audit trail — and still fail to deliver the outcome it was designed for. The release criteria tell you the system works. The success metrics tell you it is working for the people it was built for.

---

## Why the JTBD Gate Changes What Gets Built

The practical effect of requiring Section 2 to be confirmed before Section 3 is written is that it slows down one specific thing: the translation of implementation decisions into product requirements.

When teams write requirements without a job story, the requirements tend to describe what the engineering team is building. This is not always wrong — there are features where the engineering decision and the product requirement are genuinely the same. But in my experience, about a third of the P1 requirements in any first draft of a PRD are implementation decisions that have been dressed up as customer requirements. They are correct in the sense that the system needs them to function. They are not customer requirements in the sense that no customer asked for them and the traceability back to a job doesn't exist.

The JTBD gate makes that distinction visible. A requirement that exists because the database schema requires it is different from a requirement that exists because an analyst needs to reconstruct historical state for accurate analysis. The first is a technical constraint. The second is a product commitment. Both may be P1 — but they are P1 for different reasons, and the acceptance criteria for each are written against different standards.

The other effect of the gate is on scope. Outcome statements are bounded. "Minimize the time needed to reconstruct test configuration state at any historical point" is a specific need-gap for a specific customer type in a specific situation. It does not imply a full audit UI, a configuration comparison view, or a change notification system. Those may or may not address the outcome — but they must be argued against the outcome statement, not assumed to follow from the fact that a configuration tracking system is being built.

---

## The Document in Practice

The PRD is not a discovery document. By the time I write it, the opportunity should be validated — or at minimum, the hypothesis job story should be labeled [ASSUMED] and the team should have agreed explicitly to proceed on a bet rather than a validated finding. A PRD for a job story with no "When" clause evidence is a spec for an [ASSUMED] solution. That is a choice a team can make. It should make it explicitly.

The seven-section structure forces that explicitness. Section 1 commits to a scope boundary before any requirements are written. Section 2 asks the job question. Section 4 requires epistemic labeling on assumptions and constraints. Section 6 separates ship gates from success. Section 7 requires a leading indicator for every lagging KPI.

None of this guarantees the right outcome. But it does guarantee that when the experiment reads out — when the analyst tries to reconstruct a historical configuration, or the campaign manager selects a randomization unit, or the analyst receives an unexpected result and needs to understand why — the team will know whether the product delivered what it was designed for, because that design was written down in terms of outcomes before any acceptance criteria were drafted.

---

## The Frameworks, Named

The JTBD section draws on two bodies of work that approach the job question from different directions.

**Clayton Christensen's job-to-be-done theory** — the hiring/firing metaphor, the situational trigger, the idea that customers don't buy products but hire them to do a job in a specific circumstance. The job story format (situational trigger → motivation → outcome) comes from Alan Klement and was developed into a requirement format at Intercom as a replacement for user stories. The key contribution is the "When" clause — it forces specificity about the situation rather than the persona.

**Tony Ulwick's Outcome-Driven Innovation** — the systematic identification of outcome statements as the measurable units of customer need. The direction verb + metric/object + clarifier format. The idea that customers measure their success at completing a job using specific metrics — speed, accuracy, predictability — and that those metrics should be the targets a solution is designed to improve. Ulwick operationalizes what Christensen conceptualizes: the job story identifies the situation; the outcome statements specify what "done well" looks like.

The combination is what makes the JTBD section useful as a gate rather than a preamble. The job story establishes the context. The outcome statements establish the measurement. Requirements can then be evaluated against both: does this requirement arise from a named situation? Does it improve a named outcome? If the answer to both is no, the requirement needs a defense before it takes a P1 slot.

---

*If you have questions about the method or want to discuss how it applies to your own product work, I'm reachable on LinkedIn.*
