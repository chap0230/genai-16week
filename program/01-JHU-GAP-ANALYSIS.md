# JHU Certificate Program in Agentic AI — Coverage Mapping & Honest Gap Analysis

This document exists so you can satisfy yourself that you're not giving anything up that matters. It maps every element of JHU's 18-week program to this one, states plainly what I dropped and why, states what I added, and — importantly — is honest about what you genuinely lose by not paying.

---

## Coverage map

Every JHU curriculum element, and where it lives here.

| JHU element | Covered here | Notes |
|---|---|---|
| **Pre-work:** Landscape of AI, GenAI, Agentic AI | W1 Fri + every Friday | Reframed as active verification you perform yourself, weekly, rather than a lecture consumed once. |
| **Pre-work:** Python fundamentals | **Dropped** | CS degree, 25 years, comfortable with code. This is remediation for career-changers. |
| **W1:** AI-Assisted Python Coding for Agentic AI | W15 (entire week) | Moved late and expanded ~10×. JHU teaches using an AI assistant; W15 has you authoring skills, hooks, and your own agent harness. |
| **W2:** LLMs and Prompt Engineering | W1 + W2 (two weeks) | Split into mechanics (W1) and inference control (W2). Substantially deeper than one week allows. |
| **W3:** Retrieval Augmented Generation | W4 + W5 (two weeks) | Split into fundamentals and advanced/evaluated retrieval. |
| **W4:** Prompt Optimization and Evaluation | W2 (regression harness) + W6 (full week) | Includes automated prompt optimization — DSPy and successor approaches like GEPA — which JHU also teaches. |
| **W5:** Hands-on Project | W5 — **Project 1** | |
| **W6:** Learning Break | Absorbed | Replaced by real holidays (Labor Day W2, Thanksgiving W13) plus a two-week amnesty allowance. |
| **W7:** Core Concepts of Agentic AI Systems (ReAct, MCP) | W7 | Plus you author an MCP server, which JHU does not require. |
| **W8:** Planning and Reasoning Mechanisms | W9 | |
| **W9:** Ethics, Safety, Alignment, Responsible AI | W12 (Thu AM) + threaded throughout | Constitutional AI, RLHF and refusal behavior, jailbreak taxonomy, PII. |
| **W10:** Hands-on Project | W10 — **Project 2** | |
| **W11:** Learning Break | Absorbed | |
| **W12:** Multi-Agent Systems | W10 | Plus A2A, and a required finding on where multi-agent *hurt*. |
| **W13:** Interaction and Embodiment | Partially — see "dropped" below | Human-agent interaction covered (HITL, approval gates, AG-UI). Physical embodiment dropped. |
| **W14:** Evaluation of Agentic AI Systems | W6 + W11 | Moved eight weeks earlier. See "changes" below — this is the most consequential restructuring. |
| **W15:** Monitoring and Observability | W11 | OTel GenAI conventions, AgentCore Observability, CloudWatch. |
| **W16:** Securing Agentic AI Systems | W12 (entire week) | |
| **W17:** Pre-Deployment and Operationalization | W14 + W16 | Expanded well beyond JHU's containerization focus. |
| **W18:** Hands-on Project | W16 — **Project 3 capstone** | |
| **Claude-Based AI Workflows** (~5 hrs) | W15 + every Wednesday PM | JHU allots 5 hours. You get a full week plus 16 weeks of rotating real work in Claude Code, Codex, Kiro, and Cowork. |
| **Self-paced RL module** (RL foundations, Deep RL, Verbal RL) | W13 + W9 | Verbal RL sits naturally in W9 with Reflexion. Foundations and modern post-training in W13. |
| **Anthropic Masterclass** | W2, W12, W15 | Claude models, Constitutional AI, prompting, API integration, structured outputs, model comparison. |
| GraphRAG | W5 Wed AM | |
| Agentic RAG | W5 Thu AM | |
| Advanced RAG | W5 | |
| Neuro-Symbolic AI | W2, W6, W12 — reframed | See "dropped/reframed" below. |
| Small Language Models | W13 Tue PM | |
| PPO | W13 Tue AM — **concept only** | See below. |
| DSPy / RAGAS / DeepEval | W6 Thu AM | |
| LangGraph | W8 (full implementation) | |
| smolagents | W8 Mon AM survey | |
| ChromaDB / vector stores | W4 | Plus the AWS-native menu, which JHU omits. |
| Docker / containerized deployment | W8 (AgentCore Runtime), W14 | |

**Every JHU curriculum item is accounted for.** Two are deliberately reduced, and I want to be explicit about both.

---

## What I dropped, and why

**1. PPO implementation and the reinforcement-learning coding track.**
JHU has you implement PPO for warehouse navigation. I cover RL conceptually in W13 — the RLHF pipeline via InstructGPT, why the field moved to DPO, and RLVR as the basis for reasoning models — but you will not implement a policy-gradient algorithm.

*Reasoning:* implementing PPO teaches you RL engineering. You are not going to be an RL engineer, and no GenAI Specialist SA interview will ask you to implement one. What you *will* be asked is "should we fine-tune, and what's involved," which is the conceptual framework. The 8–10 hours PPO would consume buys a full week of agent reliability engineering instead, which is worth far more to your specific career.

*Honest counterpoint:* if you ever want to go deep on RL, this is a real gap, and you'd want a dedicated month. I don't think you should, but you should know it's a choice I made on your behalf.

**2. Physical embodiment and robotics.**
JHU's Week 13 covers "interaction and embodiment." I keep the interaction half — human-in-the-loop design, approval gates for irreversible actions, and AG-UI for agent-to-UI protocols — and drop physical embodiment.

*Reasoning:* it's not relevant to enterprise cloud architecture, which is your entire market.

*Where I'm light and you should know it:* **computer-use and browser agents** are the practically relevant descendant of embodiment, and I've only given them incidental coverage (AgentCore Browser appears in W8). This is a genuine soft spot. My recommendation: make it your first Continuous Mode deep-dive in December, or swap it into W10's Wednesday if multi-agent goes faster than expected.

**3. Neuro-symbolic AI — reframed rather than dropped.**
JHU emphasizes this twice, including "neuro-symbolic methods for deterministic validation." I cover the production-relevant core — constrained decoding and structured output (W2), deterministic verification and symbolic checks (W6), and tool-verified reasoning with deterministic guards (W12) — without the academic neuro-symbolic framing.

*This one is a judgment call, not a clear win.* My view is that the enterprise-relevant substance is "use deterministic code to validate probabilistic output," which is thoroughly covered, and the broader neuro-symbolic research program is more academically interesting than practically load-bearing today. A reasonable person could disagree, and if the term comes up in an interview you should be able to say roughly what I just said.

---

## What I added that JHU doesn't have

**1. Context engineering — a full week (W3).**
The single biggest omission in JHU's curriculum. Prompt engineering largely dissolved into context engineering during 2025; the discipline is now about allocating a finite, degrading, expensive context window. JHU still teaches "Prompt Engineering" as a Week 2 topic and never addresses context as a managed resource. This is also the week where your systems-thinking background gives you a real edge.

**2. Reliability, resilience & multi-region agentic architecture — a full week (W14).**
JHU has nothing comparable. This is your differentiator, and the reason to weight it heavily: you are a re:Invent speaker on multi-region architecture and a founding member of the AWS Resilience Specialty community. Almost nobody in GenAI reasons rigorously about SLOs for non-deterministic systems, agent idempotency, or failover for stateful agents. W14's output is publishable and conference-submittable.

**3. GenAI economics and cost modeling (W15 Thu, threaded from W2 onward).**
Every call in your harness reports its cost starting Week 2. JHU never addresses unit economics. This is the conversation you'll have with every executive you advise.

**4. Toolchain mastery as a first-class skill (W15 + 16 Wednesdays).**
JHU gives Claude ~5 hours as a bolt-on module. You get a full week plus 16 weeks of rotating real work across Claude Code, Codex, Kiro, and Cowork — ending with skills, hooks, and a custom harness you author. This directly serves your "expert operator" goal, which JHU's format cannot.

**5. A permanent currency system (every Friday AM + W16 Fri).**
JHU ends and you're on your own. You explicitly said staying current matters, so frontier watch is a weekly habit from Week 1, and standing up Continuous Mode is a graded Week 16 deliverable — built while you still have momentum.

**6. AWS-native depth throughout.**
JHU hands out OpenAI API keys and teaches LangGraph. You'll learn LangGraph too (W8), but weighted toward Bedrock, AgentCore's full component set, and Strands — because that's your job, your credibility, and your interview panel.

**7. MCP authorship, not just consumption (W7).**
JHU covers MCP as an integration technique. You'll build a server and understand the protocol from both sides.

---

## The one structural change I'd defend hardest

**JHU teaches evaluation in Week 14 of 18. I teach it in Week 6 of 16.**

Everything after evaluation is either measured or guessed. JHU's students spend Weeks 7–13 building agents with no instrument to tell them whether changes help — then learn to measure in Week 14, by which point the projects are done. You'll build Projects 2 and 3 with a calibrated eval harness already in hand, which means every architectural decision in Weeks 7–16 comes with evidence attached.

There's a cost: Week 6's error analysis requires Project 1 to already exist, so the sequencing is tight. That's why Project 1 lands in Week 5 rather than later.

---

## Hours

| | JHU | This program |
|---|---|---|
| Duration | 18 weeks | 16 weeks |
| Weekly commitment | 8–10 hrs | 10 hrs |
| Learning breaks | 2 weeks | 0 (holidays absorbed instead) |
| **Total instructional hours** | **130** (13 CEUs) | **~152** |
| Hands-on projects | 3 | 3 + 16 weekly deliverables |
| Graded assessments | Projects + quizzes | 16 hard gates with oral exams |
| Cost | ~$10K | $0 + ~$40–75/mo AWS |

---

## What you genuinely lose by not paying

I'd be doing you a disservice if I pretended this were strictly better. Four real losses:

**A cohort.** Learning alongside peers creates social accountability and exposes you to questions you wouldn't ask. This is the biggest loss and it's not fully substitutable.

**Live mentors and JHU faculty masterclasses.** Four masterclasses with genuinely distinguished faculty, plus 16 live sessions with industry mentors — including, per the brochure, a GenAI/ML Engineer at AWS. Real value, and unavailable here.

**A credential from a top-10 university.** You said you don't care. I'd gently note that credentials do sometimes function as a filter at the résumé stage — but your Amazon Principal SA title and re:Invent speaking history already outrank a continuing-education certificate, so I think your read is correct.

**A program manager whose job is chasing you.** Real accountability value, given your history with the last plan.

### How we substitute

For the cohort and accountability gaps specifically, three things — and I'd push you to do at least the first two:

1. **Present W14 internally at Amazon.** Multi-region agentic resilience, to the Resilience Specialty community you helped found. A real audience on a real date is the strongest forcing function available to you, and it's better than a cohort because it's your actual professional network.

2. **Find one or two peers** — inside Amazon or not — doing something similar, and send them your Friday gate write-up every week. It doesn't need to be reciprocal or formal. Someone expecting a weekly artifact from you is most of what a cohort provides.

3. **I'll do the program-manager job.** Scheduled prompts, gate tracking, and telling you plainly when you're behind. That's the `05-ACCOUNTABILITY.md` setup and the tracker dashboard. It's the part I can actually replace well.

The masterclasses and the credential I can't replace. Everything else, I think this does better for your specific situation — because it's built for one person with 25 years of systems expertise and a specific role in mind, rather than for a mixed-ability cohort that has to include Python remediation.
