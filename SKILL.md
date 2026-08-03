---
name: council
description: Use when facing a real decision (build/kill/price/hire/ship/pivot). Convenes a 7-seat C-suite board that debates, votes, and returns one owned decision.
---

# Council — think like a company, not like a solo founder

A solo founder has one brain and one bias. A company has seats that are *paid to disagree*.
This skill forces the decision through 7 seats, a vote, and a written record.

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
Append to `decisions/YYYY-MM-DD-<slug>.md` using `templates/decision.md`.
Then check open records: any past decision whose kill-switch date has passed gets flagged
to the user in one line ("kill-switch due: X").

## Rules
- Seats disagree by construction. If all 7 agree, the framing is wrong — reframe once.
- Every seat must name a falsifier. Opinions without a falsifier are struck.
- Cap output: the whole council fits on one screen. Board meetings are short or they are theatre.
- Language: council runs in the user's chat language; the written record is English.

## Pitfalls
- Don't let CEO speak first — it anchors the board. Order: Customer → CFO → CTO → CMO → COO → Risk → CEO.
- Don't invent numbers. If a seat needs data nobody has, that becomes the first move.
- DEFER is a real answer but must carry a date, otherwise it's a KILL wearing a costume.
