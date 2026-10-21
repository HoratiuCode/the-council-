# council

![council](assets/council.png)

A skill that makes you think like a company instead of like one guy at 2am.

Give it a decision, it seats a 7-person board (Customer, CFO, CTO, CMO, COO, Chief Risk, CEO),
makes them disagree, runs a pre-mortem, votes, and returns **one owned decision** with a
kill-switch date and a first move you can do in 48h. Every call is written to `decisions/`.

This skill is **portable** — it runs unchanged on Claude Code, Hermes, and OpenClaw.
Only the install path and trigger command differ.

## Install

> The skill folder must be named `council` (matching `name:` in SKILL.md). The source folder
> here is named "the council " with a trailing space; the commands below copy it and rename it.

### Hermes
```bash
cp -r "the council " ~/.hermes/skills/council
```
Then: `skill_view(name='council')` — or just ask "should I build X?" and it triggers.

### Claude Code
```bash
cp -r "the council " ~/.claude/skills/council
```
Then: `/council` (slash command) or let Claude auto-activate it on a matching request.
`effort: high` in the frontmatter raises Claude's reasoning budget for the council.

### OpenClaw / ClawHub
```bash
clawhub install council          # or import the GitHub repo via the web importer
```
Trigger: natural language — the `description` field is matched against your request.
For ClawHub publishing the license is MIT-0; drop the copyright line in LICENSE if you publish.

## Layout
```
council/
  SKILL.md              procedure: frame → seat → red team → vote → decide → record
  references/seats.md   the 7 seats + optional guests (Legal, Competitor, Chief Scientist)
  templates/decision.md the written record
  decisions/            your decision log (kill-switch tracked)
  assets/council.png    the board
```

## Why it works
- Seats are **paid to disagree** — no single-brain bias.
- Every opinion needs a **falsifier**, or it's struck.
- Every decision needs a **kill-switch** — no zombie projects.
- The board is short. Long board meetings are theatre.

## License
MIT — Copyright (c) 2026 Soljunge. (ClawHub publishes under MIT-0; no attribution required there.)
