# GenAI & Agentic AI — 16-Week Intensive

**A JHU-comparable program, rebuilt for a Principal AWS Solutions Architect**

| | |
|---|---|
| **Starts** | Wednesday, 2026-08-26 |
| **Ends** | Friday, 2026-12-11 |
| **Continuous Mode begins** | Monday, 2026-12-14 |
| **Commitment** | 10 hrs/week — 1 hr at 6am + 1 hr at 1pm, weekdays |
| **Total instructional time** | ~150 hours (JHU's program is 130) |
| **Cost** | $0 plus AWS sandbox spend (budget ~$40–75/mo) |

---

## Why this document exists

You sent me an 18-week, ~$10K Johns Hopkins certificate program in Agentic AI and said you want the learning, not the credential. I read all 22 pages. This program covers everything JHU covers with two exceptions I'll defend in the gap analysis, adds five areas JHU omits that matter specifically for you, and is weighted toward AWS because that's where you work and where your credibility compounds.

Full module-by-module mapping is in `01-JHU-GAP-ANALYSIS.md`. The short version: JHU spends its first six weeks and a prework module getting a mixed-ability cohort to a baseline you're already past — Python fundamentals, "AI-assisted coding," environment setup. It also has two learning breaks and a lot of finance-industry case studies. Stripping that recovers roughly five weeks, which I've spent on context engineering, agent reliability and multi-region architecture, GenAI cost economics, toolchain mastery, and a permanent currency system. JHU has no equivalent to any of those.

---

## Why your last attempt didn't stick — and what's different

You've had a daily 1-hour program running since 2026-06-17 with a 7am scheduled push. You told me it mostly didn't happen. That's diagnostic information, not a character flaw, and the design was working against you in five specific ways:

**The content was generated fresh each morning.** Nothing existed in advance, so there was no path to be behind *on*. Slippage was invisible and therefore costless. *Fix: this entire program is authored up front. All 16 weeks, all 152 sessions, all deliverables exist before you start. Falling behind is now a measurable, visible fact.*

**7am, before a Principal SA workday.** The single most interruptible hour you own, competing directly with your inbox. *Fix: a split — 6am reading and 1pm building. The morning hour is reading and thinking, which survives a distracted brain. The 1pm hour is building, which needs you cognitively warm and at a machine you're already working on.*

*One caveat on 1pm, stated plainly:* a midday block sits inside your workday, so it will be attacked by meetings in a way an evening block wouldn't. This design only works if you put a recurring 1–2pm hold on your calendar, marked busy, starting now — and defend it the way you'd defend a customer call. If you find yourself losing that hour to meetings three days in a row, tell me and we move it rather than letting it quietly decay. That decay is precisely how the last attempt died.

**One hour is too short to build anything.** By the time you reload context on a coding problem, the hour's gone. This is why the daily-hour format produces reading and not artifacts. *Fix: the morning session's explicit job is to load context for the 1pm session. Same topic, twice a day, seven hours apart — which is close to an ideal spacing interval. You arrive at the build block already warm, and you get spaced repetition for free.*

**Nothing was produced.** Consumption without artifacts feels like progress and isn't. You cannot demo a module you read. *Fix: every single session ends with something committed to a git repo. Every week produces a named deliverable. Nothing is complete until it's committed.*

**No consequence.** *Fix: hard gates. Friday's 1pm block is a graded assessment and you don't advance until you pass. See "The gate system" below.*

---

## The calendar

Sixteen weeks, with US holidays already absorbed so they don't derail you.

| Wk | Dates | Theme | Gate deliverable |
|----|-------|-------|------------------|
| 1 | Aug 26–28 *(3 days)* | LLM mechanics from first principles | Inference harness + landscape baseline |
| 2 | Aug 31–Sep 4 | Inference control & the API as engineering surface | Prompt regression harness |
| 3 | Sep 7–11 *(Labor Day Mon)* | Context engineering | Context budget analyzer |
| 4 | Sep 14–18 | Retrieval I — embeddings, chunking, vector search | Working RAG on AWS |
| 5 | Sep 21–25 | Retrieval II — advanced/graph/agentic RAG + retrieval eval | **PROJECT 1** |
| 6 | Sep 28–Oct 2 | Evaluation as an engineering discipline | Eval suite + LLM-judge calibration |
| 7 | Oct 5–9 | The agent loop from scratch + MCP | Hand-built agent + your own MCP server |
| 8 | Oct 12–16 | Frameworks & the AWS agentic platform | Same agent, three frameworks, compared |
| 9 | Oct 19–23 | Planning, reasoning, reflection, memory | Agent with persistent memory + replanning |
| 10 | Oct 26–30 | Multi-agent systems | **PROJECT 2** |
| 11 | Nov 2–6 | Agent evaluation & observability | Trajectory eval + OTel tracing |
| 12 | Nov 9–13 | Security & safety for agentic systems | Threat model + red-team report |
| 13 | Nov 16–20 | Reliability, resilience & multi-region agents | Multi-region agent + chaos results |
| 14 | Nov 23–27 *(Thanksgiving — light)* | Model customization & the training-side model | Customization decision framework |
| 15 | Nov 30–Dec 4 | Toolchain mastery + GenAI economics | Custom agent harness + cost model |
| 16 | Dec 7–11 | Capstone + interview conversion | **PROJECT 3** + Continuous Mode live |

Week 1 is three days. The scheduled-delivery pipeline was still being repaired on Tue Aug 25 and no session was delivered, so Day 1 is Wednesday Aug 26 and Week 1 runs Wed-Fri as six blocks with a compressed plan. **Week 2 starts Monday Aug 31 and every week after it is exactly as authored** — Labor Day still falls in Week 3, Thanksgiving still in Week 14, and the program still ends Dec 11. Week 3 loses Labor Day and Week 14 loses Thanksgiving Thursday and Friday — both are deliberately lighter weeks, not weeks where you fall behind. Week 14's gate moves to Wednesday.

---

## The weekly rhythm

Ten one-hour blocks. The pattern is identical every week, which is the point — you should never wonder what today is for.

| Block | Purpose |
|-------|---------|
| **Mon AM** | Primary source. Read the paper or spec. Write a teach-back note in your own words. |
| **Mon PM** | Scaffold the week's artifact. Get something running end to end, however badly. |
| **Tue AM** | Second source, deeper. Mechanism, not narrative. |
| **Tue PM** | Core implementation. The main build. |
| **Wed AM** | Failure modes. How does this break? What are the known pathologies? |
| **Wed PM** | Extend the artifact — using the week's **designated tool** (rotates: Claude Code → Codex → Kiro → Cowork). |
| **Thu AM** | Write evals for what you built. Measurement before opinion. |
| **Thu PM** | Harden: security, cost, observability, one injected failure. |
| **Fri AM** | Frontier watch (30 min) + write it up (30 min). |
| **Fri PM** | **GATE.** Graded deliverable + oral-exam self-test. Commit everything. |

Three structural notes on why this shape:

*Morning loads, midday builds.* The 6am block is deliberately the low-energy, interruption-tolerant work — reading, note-writing, thinking. It also front-loads the context you need at 1pm, so the build block starts warm instead of spending 20 minutes remembering where you were.

*Thursday is your unfair advantage.* Every week, one full block on evals and one on hardening. Most people learning agentic AI never do this and it's precisely where 25 years of reliability engineering converts into GenAI credibility. By Week 16 you'll have done it 16 times.

*The Wednesday tool rotation is not busywork.* You listed Claude Code, Cowork, ChatGPT, Codex, Quick, and Kiro as tools you care about. You get expert with a tool by doing real work in it under deadline, not by reading its docs. Rotating the same class of task across four harnesses also teaches you what's intrinsic to agentic coding versus what's one vendor's opinion — which is exactly the comparative judgment a Specialist SA is paid for.

---

## The gate system

You asked for maximum structure, so gates are hard, not advisory.

**Every Friday PM** you produce a gate artifact and grade yourself against three criteria:

1. **The artifact runs.** Committed, reproducible, and someone else could clone it and get the same result.
2. **The written defense holds.** One page: what you built, what you chose, what you rejected and why, what it costs, and how it fails. Written as if a bar-raiser will read it.
3. **The oral test passes.** Five questions per week are pre-written in the weekly detail. You answer out loud, from memory, without notes. If you hedge or hand-wave on two or more, the gate fails.

**A failed gate means you repeat the week's Thursday and Friday blocks before moving on.** You don't get to accumulate silent debt. Two consecutive failed gates and we stop and redesign — that's a signal the program is wrong, not that you are.

**Triage rules for when life happens.** This is the part most study plans omit and the reason most study plans die.

- *Missed one block:* Do nothing. The week is designed with slack. Keep going.
- *Missed 2–3 blocks:* Skip that week's Wednesday PM extension work. Protect Thursday and Friday. Never skip the gate.
- *Missed a full week:* Do not try to double up — that fails every time. Instead take the following week's Mon AM to do a compressed catch-up of the missed week's Mon/Tue AM readings, skip its build, and carry forward. Mark the week **partial** in the tracker and note the specific debt.
- *Missed two weeks:* Stop. We re-plan the remaining weeks together rather than pretending the calendar still holds.
- *Amnesty:* You get two "partial" weeks across the program with no penalty. Spend them deliberately.

The single rule that matters more than the rest: **when you're behind, cut build scope, never the gate.** The gate is what converts activity into retained capability.

---

## Daily quizzes

The Friday oral exam is the gate, but it's a lagging indicator — by Friday, a week you skimmed is already spent. So every day carries a low-friction retrieval check:

- **6am block opens with 3 multiple-choice questions** on the *previous* one to three sessions. Spaced retrieval, roughly two minutes, and it doubles as context reload for the day.
- **1pm block closes with 2 multiple-choice questions** on that day's material — one from the morning's reading, one on something the build should have made concrete.
- **Friday's gate opens with a 5-question set covering the whole week.** This is a diagnostic, not a formality: miss two or more and you're not ready for the orals, so reread before attempting them.

Answers always sit below a divider so you can't see them while answering. Log the score in `LEARNING-LOG.md`.

The questions are written to catch a shallow read — telling apart two things that sound similar, or predicting a failure mode — rather than to test vocabulary. **Accuracy below 80% on a topic sends it back into Friday's frontier hour for a reread.** The point of tracking this is that quiz scores and gate results fail differently: you can pass a gate on a well-built artifact while having absorbed very little of the reading behind it. Two signals catch that; one doesn't.

---

## Currency: nothing reaches you unverified

This field moves faster than any authored curriculum can hold, and a study plan that teaches last year's platform is worse than no plan — it produces confident wrong answers. So the program is authored up front, but **every session is verified against live sources immediately before it's delivered.**

Each scheduled session checks the day's material against AWS documentation, What's New, the AWS-curated `amazon-bedrock` and `aws-ai-ml` skill bundles, and the relevant specs — then adjusts the session before sending. Deprecated APIs get fixed, renamed components get renamed, and where a managed service has appeared that does what you were about to hand-roll, you still build it by hand first and then compare, because you can't judge a managed abstraction you've never had to implement.

Findings accumulate in **`06-CURRENCY-DELTA.md`**. Read that file's first entry before Day 1 — the initial verification pass found substantial drift, including a Cedar-based policy engine for agent tool calls, a managed evaluation service with trajectory evaluators, and an entirely new Bedrock API surface. Several weeks change as a result.

One rule keeps this from becoming noise: a "what changed" note appears **only when a finding actually alters the day's work.** A currency alert that fires every morning gets ignored, which defeats the purpose.

---

## Your AWS sandbox setup

Do this before your first 1pm build block on Wed 2026-08-26. The Wednesday morning block needs none of it; the afternoon needs all of it. It is not part of the 16 weeks and should take about 90 minutes.

- **Budget guardrails first.** AWS Budgets at $50/mo with alerts at 50/80/100%. A runaway agent loop is a real financial risk and you should experience thinking about that on day zero.
- **Bedrock model access** enabled in `us-east-1` and `us-west-2` — both regions, deliberately, because Week 13 needs them.
- **Repo:** `genai-16week` with a directory per week. Private is fine. Everything you build lives here; the repo *is* the portfolio.
- **Toolchain installed and authenticated:** Claude Code, Codex, Kiro, and the AgentCore CLI (`npm install -g @aws/agentcore`).
- **Python 3.12+** with `uv`, and the AWS SDK. **Node 22+** for the TypeScript work in Weeks 8 and 15 — the AgentCore CLI's TypeScript path requires 22, not 20. Also install the AWS CDK; the CLI uses it to deploy.
- **A running note file** at the repo root, `LEARNING-LOG.md`. Append to it every session. This becomes your interview prep material in Week 16 and it is genuinely the highest-value artifact in the whole program.

---

## The three projects

You chose customer-facing AWS scenarios — projects modeled on real asks you'd field as a GenAI Specialist SA. Each is reusable in your day job and each is directly demoable in an interview.

**Project 1 (Week 5) — Architecture Standards Advisor.**
*The customer ask:* "We have 400 pages of internal architecture standards plus AWS's guidance, and our teams don't read either. Can we ask questions against it?"
You'll build a retrieval system over AWS Well-Architected content and a synthetic internal-standards corpus, with a real retrieval evaluation harness — not a demo notebook. Deliverable includes measured retrieval quality, a documented chunking decision, cost per query, and an honest statement of what it gets wrong. The evaluation rigor is the point; anyone can wire up a vector store.

**Project 2 (Week 10) — Migration Assessment Crew.**
*The customer ask:* "Here's a description of our estate. Give us a modernization assessment."
A multi-agent system: a planner, specialist assessors for compute, data, and network, a cost analyst, and a critic that challenges the others' findings. You'll deploy it on AgentCore Runtime with Memory and Gateway. Critically, you will also produce a written finding on **where multi-agent made it worse** — because it will, in at least one place, and knowing that is a senior signal.

**Project 3 (Week 16) — Capstone: production agentic platform.**
*The customer ask:* "We want to run agents in production and our risk team has questions."
A complete, defensible system: multi-region, evaluated with a real trajectory eval suite, traced through OTel into CloudWatch, guardrailed, least-privilege IAM'd, cost-modeled, with a documented failure and recovery story. This is the artifact you walk into an interview with, and it is your resilience expertise expressed in a GenAI system — a combination very few candidates can offer.

---

## What happens after Week 16

Continuous Mode starts Monday 2026-12-14 and runs indefinitely at a sustainable 3–4 hrs/week. Rotating focus: frontier-watch, AWS-watch, one deep-dive, one build, one paper. The Week 16 gate includes standing this up so it exists before motivation fades.

The premise is that expertise in this field is a maintained state, not an achieved one. The program's real deliverable isn't the 16 weeks — it's that on 2026-12-14 you have a working system for staying current, a portfolio of three demoable systems, and a 152-hour learning log you can mine for any interview question you'll be asked.

---

## The rest of the program

| File | What's in it |
|---|---|
| `01-JHU-GAP-ANALYSIS.md` | Every JHU element mapped; what I dropped and why; what I added; what you genuinely lose by not paying |
| `02-WEEKS-01-08.md` | Session-by-session for Weeks 1–8, with build specs and the five oral questions per gate |
| `03-WEEKS-09-16.md` | Session-by-session for Weeks 9–16 |
| `04-RESOURCES.md` | Papers by theme with arXiv IDs, courses, docs worth close reading, and exactly eight currency sources |
| `05-ACCOUNTABILITY.md` | The scheduled tasks, the tracker, the escalation ladder, and the honest limits of all of it |
| `06-CURRENCY-DELTA.md` | **Read this before Day 1.** Dated log of what's changed since authoring, mapped to the weeks it affects |
