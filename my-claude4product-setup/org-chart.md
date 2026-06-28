# Agent Org Chart

---

## Diagram 1 — Functional Clusters

```mermaid
graph TD
  subgraph GOV["⚖️ Capability Governance"]
    CA["caronte\n📋 registry\n🗂️ org-chart"]
  end

  subgraph DISC["🔍 Discovery & Strategy"]
    STR["strategist\n📄 zms-discovery-paper"]
    PA["product-analyst"]
    ADS["adtech-scientist\n📄 fourier-tutor"]
    KOH["kohavi\n📄 zms-discovery-paper\n📄 fourier-tutor"]
    PW["prfaq-writer"]
    PR["prfaq-researcher"]
  end

  subgraph DEL["🚀 Delivery"]
    PM["product-manager\n📄 write-brd\n📄 brainstorming\n📄 writing-plans"]
    PJM["project-manager"]
    PE["principal-engineer\n📄 TDD\n📄 subagent-driven-dev"]
    DW["documentation-writer"]
    OG["ogilvy\n👥 audience-register adapter"]
    MA["marchoi\n📊 WBR Area 4 · Auction Health"]
  end

  subgraph QI["✅ Quality & Integrity"]
    FC["fact-checker\n📄 verification-before-completion"]
    KOH2["kohavi\n📄 systematic-debugging"]
    PE2["principal-engineer\n📄 code-review"]
  end

  subgraph GTM["📣 Growth & GTM"]
    GE["gtm-expert"]
    PA2["product-analyst"]
  end

  subgraph OPS["⚙️ Internal Ops"]
    ITPM["internal-tools-pm"]
    ITE["internal-tools-engineer"]
    MD["master-delegator\n📄 dispatching-parallel-agents"]
  end

  subgraph PERS["🌅 Personal Layer"]
    MIG["mignolo\n📬 daily brief · Gmail+Chat\n⏰ 9AM Berlin cron"]
  end

  GOV -.governs.-> DISC
  GOV -.governs.-> DEL
  GOV -.governs.-> QI
  GOV -.governs.-> GTM
  GOV -.governs.-> OPS
  GOV -.governs.-> PERS
```

---

## Diagram 2 — Delivery Flow & Feedback Loops

Solid arrows = main delivery path. Dashed arrows = feedback and loop-back. Labels name the trigger for each loop.

```mermaid
flowchart TD
    CA(["⚖️ caronte\nGovernance · weekly curation"])

    subgraph DISC["🔍 Discovery & Evidence"]
        STR["🎯 strategist\nMission · priorities · go/no-go\nSkills: zms-discovery-paper · write-brd"]
        PA["🔬 product-analyst\nResearch · validation · evidence\nSkills: zms-discovery-paper"]
        KOH["📊 kohavi\nA/B design · causal inference · power calc\nSkills: zms-discovery-paper · fourier-tutor"]
        ADS["⚡ adtech-scientist\nML models · bidding · attribution · Databricks\nSkills: zms-discovery-paper · fourier-tutor"]
    end

    subgraph SPEC["📋 Spec & Delivery"]
        PM["📋 product-manager\nPRDs · stories · acceptance criteria\nSkills: write-brd · brainstorming · writing-plans"]
        PJM["📌 project-manager\nJTBD · sequencing · task owners\nSkills: writing-plans"]
        PE["🛠️ principal-engineer\nCode · architecture · feasibility\nSkills: TDD · subagent-driven-dev · code-review"]
        DW["📝 documentation-writer\nREADMEs · guides · launch copy\nSkills: verification-before-completion"]
        FC["✅ fact-checker\nCode-grounded accuracy · file:line citations\nSkills: verification-before-completion"]
        OG["👥 ogilvy\nAudience-register adaptation · prose layer only\nOpt-in · never auto-fires"]
        MA["📊 marchoi\nWBR Area 4 · Prophet anomaly model · Ogilvy pass\nWeekly cron · ad-hoc on request"]
    end

    subgraph TOOLS["⚙️ Internal Tools"]
        ITPM["🔧 internal-tools-pm\nTooling backlog · capability gaps"]
        ITE["⚙️ internal-tools-engineer\nBuilds scripts · agents · automations"]
    end

    GE["📣 gtm-expert\nPositioning · messaging · launch"]

    %% Governance
    CA -. governs .-> STR

    %% ── Main delivery path ──────────────────────────────────────────
    STR ==>|"direction set"| PM
    PM ==>|"PRD approved"| PJM
    PJM ==>|"JTBDs assigned"| PE
    PE ==>|"surface shipped"| DW
    DW ==>|"doc drafted"| FC

    %% ── Continuous discovery loop ────────────────────────────────────
    STR <-->|"continuous discovery"| PA
    PA -->|"evidence → spec"| PM
    PM -.->|"open questions"| PA

    %% ── Experiment learn loop ────────────────────────────────────────
    PM -->|"experiment needed"| KOH
    KOH <-->|"data analysis"| ADS
    ADS -.->|"findings → adjust spec"| PM
    KOH -.->|"results → re-prioritise OST"| STR

    %% ── PRFAQ loop (see Diagram 3 for detail) ────────────────────────
    PM -->|"PRFAQ requested"| PW["✍️ prfaq-writer\nDraft · revise"]
    PW <-->|"annotate / revise\n(N rounds)"| PR["🔍 prfaq-researcher\nCritique · axiom check"]
    PR -.->|"clean export"| PM
    DW -->|"doc needs audience adaptation"| OG
    PW -->|"PRFAQ needs audience adaptation"| OG
    MA["📊 marchoi\nWBR Area 4 · Monday cron\nProphet · Ogilvy pass"] -->|"dispatch analyst"| ADS
    MA -->|"exec prose pass"| OG

    %% ── Quality gate loops ───────────────────────────────────────────
    FC -.->|"doc errors found"| DW
    DW -.->|"code errors found"| PE
    FC -.->|"spec axiom violation"| PM

    %% ── Strategy escalation loop ─────────────────────────────────────
    PM -.->|"scope conflict"| STR
    PE -.->|"feasibility block"| PM

    %% ── Internal tools unblock loop ──────────────────────────────────
    PE -.->|"capability gap"| ITPM
    PJM -.->|"capability gap"| ITPM
    ITPM ==> ITE
    ITE -.->|"tool ready → unblock"| PE

    %% ── Launch path ─────────────────────────────────────────────────
    PJM -->|"ship-ready"| GE

    %% ── Personal layer ──────────────────────────────────────────────
    MIG(["🌅 mignolo\nDaily personal brief · Gmail+Chat\n⏰ 9AM Berlin cron"])
    CA -. governs .-> MIG
```

---

## Diagram 3 — PRFAQ Critique Loop

```mermaid
flowchart LR
    INPUT(["👤 Input\nraw idea or draft"])
    PW["✍️ prfaq-writer\nDraft or revise\nround N"]
    PR["🔍 prfaq-researcher\nAnnotate · check causal claims\nflag axiom violations"]
    GATE{{"Another\nround?\ndefault cap: 2"}}
    EXPORT(["📄 Export\nprfaq-final.docx\nprfaq-annotated.docx"])

    INPUT -->|"raw idea → mode: draft"| PW
    INPUT -->|"existing draft → mode: revise"| PW
    PW -->|"draft rN"| PR
    PR -->|"annotated rN"| PW
    PW -->|"revised rN+1"| GATE
    GATE -->|"yes — researcher\ncritiques again"| PR
    GATE -->|"no — export"| EXPORT
```

---

## Diagram 4 — Mignolo → Caronte Feedback Loop

How Caronte learns what's missing from the stack by watching what you actually do each day.

```mermaid
flowchart LR
    GMAIL(["📧 Gmail\nGoogle Chat\nGoogle Calendar"])
    MIG["🌅 mignolo\nDaily brief · 9AM Mon–Fri\nWrites YYYY-MM-DD.txt\n+ digest JSON"]
    DIGEST[("📁 digests/\nYYYY-MM-DD.json\nthreads + tier1_subjects\n~500 bytes · kept indefinitely")]
    CA["⚖️ caronte\nWeekly curation · 8AM Monday\nMignolo Feed second pass"]
    REG[("📋 registry.md\nactive · rejected · candidates\ncuration log")]
    CHAT(["💬 Chat\nPROMOTE proposals\nuser approval required"])

    GMAIL -->|"reads yesterday"| MIG
    MIG -->|"Step 8: compress + write"| DIGEST
    DIGEST -->|"reads last 30\nevery Monday"| CA
    CA -->|"clusters recurring topics\ncount ≥ 3 → gap detected"| CHAT
    CHAT -->|"approved → candidate"| REG
    REG -->|"registry context\nfor next curation"| CA
```

---

## Agent Reference

| Agent | Role | Invoke when | Skills | Model |
|---|---|---|---|---|
| caronte | HR director · capability auditor | Considering a new skill or agent; every Monday (cron) | registry · org-chart | opus |
| master-delegator | Orchestrator | Complex goals needing parallel sub-tasks | dispatching-parallel-agents | — |
| strategist | Mission setter · go/no-go | Any new initiative; direction unclear | zms-discovery-paper · write-brd | opus |
| product-analyst | Evidence · research · validation | Claim needs proof; problem space unclear | zms-discovery-paper · competitive-analysis · analyze-feedback · market-sizing | sonnet |
| product-manager | PRDs · stories · acceptance criteria | Direction set; spec needed | brainstorming · write-brd · writing-plans | opus |
| project-manager | JTBD decomposition · sequencing | PRD exists; work needs queuing | writing-plans | sonnet |
| principal-engineer | Architecture · code · feasibility | Any code-writing or technical design task | TDD · systematic-debugging · verification-before-completion · code-review · subagent-driven-dev · using-git-worktrees | opus |
| documentation-writer | READMEs · guides · API refs | New surface shipped; GTM needs assets | verification-before-completion | sonnet |
| fact-checker | Code-grounded accuracy review | Doc about system ready for final review | verification-before-completion | opus |
| kohavi | A/B testing · causal inference | Experiment design; result interpretation; causal claim | systematic-debugging · zms-discovery-paper · fourier-tutor · analyze-test | sonnet |
| adtech-scientist | Bidding · attribution · ML · Databricks | Any adtech analytical or modeling question | zms-discovery-paper · fourier-tutor · write-query · analyze-cohorts | sonnet |
| prfaq-writer | PRFAQ drafting and revision | PRFAQ loop round — draft or revise | — | sonnet |
| prfaq-researcher | Causal claims · axiom violations | PRFAQ loop round — annotate draft | — | sonnet |
| gtm-expert | Positioning · launch · channels | Project nears ship-readiness | — | sonnet |
| internal-tools-pm | Team tooling backlog | Agent reports a capability gap | — | sonnet |
| internal-tools-engineer | Builds team scripts and automations | internal-tools-pm has a spec ready | — | sonnet |
| ogilvy | Audience-register adapter · prose layer only | Finished document needs rewriting for named stakeholder audience | proofread | sonnet |
| marchoi | Data analyst · WBR Area 4 · Prophet anomaly model · Ogilvy exec pass | Weekly cron fires; any ad-hoc data analysis requested | write-query · analyze-test · analyze-cohorts | sonnet |
| mignolo | Daily personal brief · Gmail+Chat triage · 9AM cron | Daily 9AM cron fires; can be invoked on-demand | — | sonnet |
