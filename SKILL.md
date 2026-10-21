---
name: council
description: Use when facing a real decision (build/kill/price/hire/ship/pivot). Convenes a 7-seat C-suite board that debates, votes, and returns one owned decision with a kill-switch and a <48h first move. Portable across Claude Code, Hermes, and OpenClaw.
version: 1.1.0
license: MIT
compatibility: Claude Code (~/.claude/skills), Hermes (~/.hermes/skills), OpenClaw/ClawHub. Requires write access to a local decisions/ log.
effort: high
metadata:
  openclaw:
    emoji: "\U0001F465"
    homepage: https://github.com/soljunge/council
    always: false
    requires:
      bins: []
    envVars: []
  hermes:
    triggers:
      - "should I build"
      - "ship or wait"
      - "what do I price this at"
      - "is this idea dead"
      - "which of these do I do first"
---

# Council — think like a company, not like a solo founder

A solo founder has one brain and one bias. A company has seats that are *paid to disagree*.
This skill forces the decision through 7 seats, a vote, and a written record.

It runs **identically on Claude Code, Hermes, and OpenClaw** — same procedure, same
decision log. Only the install path and trigger command differ (see *Runtimes* below).

## When to convene
Trigger on: "should I build X", "ship or wait", "what do I price this at", "is this idea dead",
"which of these 3 do I do first", or any message where the user is clearly circling a decision.
Do NOT convene for tasks (writing code, fixing a bug). Only for **decisions**.

## Procedure

### 1. Frame (1 line)
Restate the decision as a binary or a ranked choice. If it isn't decidable, say so and stop.
Add: reversibility (one-way / two-way door), deadline, cost of being wrong.

### 2. Seat the board
Load `references/seats.md`. Each seat speaks **max 3 lines**: position, strongest reason,
the one number/fact that would flip them. No hedging, no "it depends".
Default board: CEO, CTO, CFO, CMO, COO, Chief Risk, Customer (empty chair).
Small/cheap decision → cut to CEO + CFO + Customer.

### 3. Red team
Chief Risk gets a second pass: write the post-mortem *as if it already failed in 90 days*.
One paragraph. This is mandatory — no council without it.

### 4. Vote
Each seat: BUILD / KILL / DEFER, plus confidence 1-5.
Report the tally. Dissent is quoted, never averaged away.

### 5. Decision
CEO seat rules — the vote advises, it does not bind. Output:
- **Decision:** one sentence
- **Because:** max 3 bullets
- **Kill-switch:** the metric + date that reverses this
- **First move:** something doable in <48h
- **Not doing:** what this decision explicitly buys out of

### 6. Record
Resolve **this skill's own directory** at runtime (the folder containing this SKILL.md) and
write the record to `<skill_dir>/decisions/YYYY-MM-DD-<slug>.md` using `templates/decision.md`.
If that directory is not writable, fall back to `./decisions/` (create it).
Then check open records: any past decision whose kill-switch date has passed gets flagged
to the user in one line ("kill-switch due: X").

## Runtimes (Claude · Hermes · OpenClaw)

The skill folder must be named **`council`** (matching `name:` above) so the runtime discovers it.
The source folder here has a trailing space ("the council "); the install commands below
rename it to `council` on copy.

### Hermes
```bash
cp -r "the council " ~/.hermes/skills/council
```
Trigger: `skill_view(name='council')` — or just ask "should I build X?" and it auto-fires.
Decision log: `~/.hermes/skills/council/decisions/`.

### Claude Code
```bash
cp -r "the council " ~/.claude/skills/council
```
Trigger: the `/council` slash command, or auto-activation when the description matches.
Decision log: `~/.claude/skills/council/decisions/`.
(`effort: high` in frontmatter raises Claude's reasoning budget for the council.)

### OpenClaw / ClawHub
```bash
clawhub install council        # or import the GitHub repo via the web importer
```
Trigger: natural language — the `description` field is matched against the request.
Decision log: the skill's installed directory `decisions/` (or `./decisions/` fallback).
The `metadata.openclaw` block declares runtime requirements (emoji, homepage). No external
bins or env vars are needed. For ClawHub publishing the license is MIT-0; drop the
copyright line in LICENSE if you publish.

## Rules
- Seats disagree by construction. If all 7 agree, the framing is wrong — reframe once.
- Every seat must name a falsifier. Opinions without a falsifier are struck.
- Cap output: the whole council fits on one screen. Board meetings are short or they are theatre.
- Language: council runs in the user's chat language; the written record is English.

## Pitfalls
- Don't let CEO speak first — it anchors the board. Order: Customer → CFO → CTO → CMO → COO → Risk → CEO.
- Don't invent numbers. If a seat needs data nobody has, that becomes the first move.
- DEFER is a real answer but must carry a date, otherwise it's a KILL wearing a costume.
