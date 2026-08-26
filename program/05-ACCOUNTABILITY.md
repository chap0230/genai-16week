# The Accountability System

You said you need help staying on track and chose maximum structure. This document is the mechanism. It has four parts: what's automated, what's on you, how debt is handled, and how to reset when it breaks.

The last program failed partly because nothing existed to be behind *on* and nothing noticed when you were. Both are now fixed. But read the last section — **the honest limits** — because no amount of scheduling substitutes for the two human commitments at the bottom of this page.

---

## 1. What's automated

Three scheduled tasks now run in Claude. They replaced the old `genai-daily-study` 7am task, which has been deleted.

| Task | When | What it does |
|---|---|---|
| `genai-morning-brief` | Weekdays 6:00 AM | Verifies today's material against live sources, then delivers **only today's AM block** — under 450 words, opening with 3 multiple-choice questions on prior sessions, with real URLs, the teach-back note, and one line on what 1pm will build. |
| `genai-midday-build` | Weekdays 1:00 PM | Delivers **only today's build block** — the spec, the definition of done, what gets committed — and closes with 2 questions on the day's material. Wednesdays it enforces the designated tool. Fridays it runs the **gate**: a 5-question week-wide warm-up, then all five oral questions verbatim. |
| `genai-weekly-review` | Saturdays 9:00 AM | Broader weekly currency sweep, pace check against plan, gate and quiz-score review, triage rule application, week-ahead preview, and one cold retrieval question. |

Every one of them runs a **freshness check before it writes anything** — AWS docs, What's New, the AWS-curated `amazon-bedrock` and `aws-ai-ml` skill bundles, and the relevant specs. Sessions get adjusted before they reach you, findings get appended to `06-CURRENCY-DELTA.md`, and a "what changed" note appears only when a finding actually alters the day's work.

Three things to know about how these behave:

**1pm is inside your workday, and that's the fragile part.** A 6am block competes with sleep; a 1pm block competes with meetings, which are more persistent adversaries. Put a recurring 1–2pm hold on your calendar marked busy, before Day 1. If meetings take that hour three days running, say so and we move it — a block that quietly decays is worse than one that's honestly rescheduled.

**They only run while the Claude app is open.** If it's closed at 6am, the brief fires on next launch. That's a real gap — if you habitually quit the app overnight, the morning brief will arrive late and you should treat the tracker, not the notification, as your source of truth.

**They deliberately don't send you the whole week.** One block at a time. The failure mode of the old plan was a wall of content at 7am that was easier to close than to read. If a brief ever runs long, tell me and I'll tighten the prompt — the prompts live at `~/Claude/Scheduled/<task-id>/SKILL.md` and are editable.

### The live tracker

The dashboard artifact **GenAI & Agentic AI — 16-Week Intensive** is in your Cowork sidebar. Click each AM/PM slot as you complete it and cycle each Friday gate through `pending → passed → partial → failed`.

It computes pace by pro-rating planned sessions against today's date, so the "vs. plan" number is honest rather than flattering. The banner maps directly onto the triage rules below — it will tell you to stop and re-plan if you're more than two weeks down, because grinding against a dead calendar is how programs die quietly.

State is stored locally in that view. It survives restarts. It does not sync anywhere, so it's a private instrument, not a report to anyone.

---

## 2. What's on you

Four commitments. Everything else is scaffolding around these.

**Click the slots.** Not for my benefit — for the visibility that the old plan lacked. An unclicked slot on Wednesday is information you need on Thursday.

**Commit something every session.** Ten commits a week, minimum. `LEARNING-LOG.md` gets appended every single session, even the bad ones, even one line. In Week 16 this file becomes your interview prep, and it will be the highest-value artifact in the repo.

**Answer the Friday oral questions out loud, from memory, with the laptop closed.** This feels absurd alone in a room. Do it anyway. Reading the answer silently and nodding is exactly the self-deception the gate exists to prevent. Hedging on two or more is a fail — and you'll know when you're hedging.

**Answer the daily quizzes before scrolling to the answers, and log the score.** Three questions at 6am on prior material, two at the end of the build block on today's. Two minutes total. Their value is entirely in the fact that you commit to an answer first; a quiz you read the answers to is just more reading. Sub-80% on a topic means it goes back into Friday's frontier hour.

**Tell me when you're behind, early.** Not as confession — as input. The triage rules only work if they're applied while there's still slack to spend.

---

## 3. How debt is handled

Restated from `00-PROGRAM.md` because this is the section you'll actually need.

| Situation | Response |
|---|---|
| Missed 1 block | Nothing. The week has slack by design. Keep going. |
| Missed 2–3 blocks | Skip Wednesday PM extension work. Protect Thursday and Friday. **Never skip the gate.** |
| Missed a full week | Do not double up — it fails every time. Next Monday AM: compressed catch-up of the missed readings only. Skip that week's build. Mark the week **partial**. Carry forward. |
| Missed two weeks | Stop. We re-plan the remaining weeks around where you actually are. |
| Gate failed | Repeat that week's Thursday and Friday blocks before advancing. |
| Two gates failed in a row | Stop. The program is wrong, not you. We redesign. |

**Amnesty:** two `partial` weeks across the sixteen, no penalty, no explanation owed. Spend them deliberately rather than sliding into them.

**The one rule above the others:** when you're behind, **cut build scope, never the gate.** A shipped-but-smaller artifact that you can defend out loud beats an ambitious half-build you can't. The gate is what converts activity into retained capability; the build is just the vehicle.

---

## 4. The escalation ladder

If you've missed three consecutive blocks, work down this list in order rather than negotiating with yourself:

1. **Cut scope, not the gate.** Ship the smallest defensible version.
2. **Move the block, don't drop it.** A Saturday morning is a legitimate substitute for a lost Tuesday 1pm. Two build blocks stacked into one day is not — that's the doubling-up failure wearing a different hat.
3. **Take a partial week** and spend an amnesty. Explicitly. In the tracker.
4. **Ask me to re-plan.** Fewer weeks with real gates beats sixteen weeks of fiction.

Note what's *not* on the ladder: doubling up, skipping a gate to stay "on schedule," and marking something complete that isn't. Those three are how the last attempt ended, and each of them trades a visible problem for an invisible one.

---

## 5. The honest limits of all this

I can generate a prompt at 6am and tell you plainly when you're eleven sessions behind. That's roughly the program-manager function, and it's real value. But three things this system cannot do, and pretending otherwise would set you up to be surprised:

**I can't create social stakes.** A notification has no expectations of you. This is the main thing the $10K buys at JHU — a cohort and a mentor who notice. Which is why the two substitutions in `01-JHU-GAP-ANALYSIS.md` matter more than anything on this page:

> **Send your Friday gate write-up to one or two peers.** Every week. It doesn't need to be reciprocal, formal, or even acknowledged. Someone *expecting an artifact from you on a known day* is most of what a cohort provides, and it's the single highest-leverage thing you can add to this program.
>
> **Book the Week 13 internal presentation now** — multi-region agentic resilience, to the AWS Resilience Specialty community you helped found. Put a date on the calendar in Week 1, before you know whether you'll be ready. A real audience on a real date is a stronger forcing function than every gate in this document combined, and unlike a cohort, it's your actual professional network and it compounds into your career.

**I don't persist between sessions the way a person does.** My memory of this program is written to files, so a future session reads the plan rather than remembering the conversation. That works, but it means the files *are* the program — keep `LEARNING-LOG.md` current and the tracker clicked, because that's the state I can actually see.

**Motivation isn't the binding constraint, and shouldn't be.** You're a Principal SA with 25 years in; you don't need to be inspired, you need the path to be unambiguous and the slippage to be visible. That's what this is built for. On the weeks it feels like grinding, the design assumption is that you show up to a known block and do the known work — not that you feel like it.

---

## Quick reference

- **Program:** `00-PROGRAM.md` — rhythm, gates, triage, setup
- **Gap analysis:** `01-JHU-GAP-ANALYSIS.md` — what's covered, dropped, added
- **Sessions W1–8:** `02-WEEKS-01-08.md`
- **Sessions W9–16:** `03-WEEKS-09-16.md`
- **Resources:** `04-RESOURCES.md` — papers, docs, the eight currency sources
- **Currency delta:** `06-CURRENCY-DELTA.md` — what's changed since authoring; **read the first entry before Day 1**
- **Tracker:** Cowork sidebar → *GenAI & Agentic AI — 16-Week Intensive*
- **Scheduled prompts:** `~/Claude/Scheduled/genai-{morning-brief,midday-build,weekly-review}/SKILL.md`

**Day 1 is Wednesday, 2026-08-26.** Sandbox setup happens Wednesday morning before the 1pm block, about 90 minutes. Put the recurring 1–2pm calendar hold in place at the same time. First morning brief arrives 6am Tuesday.
