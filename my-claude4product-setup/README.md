# my-claude4product-setup

I've been building a Claude Code setup for PM work — a team of specialised agents that handle research, writing, data analysis, experimentation design, and a daily personal brief. This folder is the public version of that setup, released incrementally alongside a LinkedIn series.

Each post introduces one agent. You can drop the files directly into your own Claude Code configuration with minimal edits.

---

## The stack

A team of named agents, each with a defined role, wired together through a shared dispatcher. The system covers product discovery, spec writing, data analysis, experiment design, audience adaptation, and personal productivity. Caronte (the HR director) maintains the org chart and curates the roster weekly — including a feedback loop from Mignolo's daily briefs.

## Org chart

→ [org-chart.md](org-chart.md) — functional clusters, delivery flow, and a full agent reference table

## Agent files

→ [agents/](agents/) — one `.md` file per agent, released one per post

Each file is a Claude Code agent definition. To use one: place it in `.claude/agents/` inside your project (or `~/.claude/agents/` for global use), fill in the `{{PLACEHOLDER}}` values, and invoke it from Claude Code.

| Agent | What it does | Released |
|---|---|---|
| [mignolo](agents/mignolo.md) | Daily personal brief — triages Gmail and Google Chat into a structured morning summary | 2026-06-21 |
| [caronte](agents/caronte.md) | HR director — gatekeeps new agents and skills, curates the stack weekly, surfaces capability gaps from Mignolo's briefs | 2026-06-28 |

## Changelog

→ [CHANGELOG.md](CHANGELOG.md)
