# Curated Resources

Everything here is free unless marked. Aggressively pruned — a 40-item list you actually work through beats a 200-item list you bookmark.

> **An honesty note you should read before trusting this file.**
> My reliable knowledge runs through roughly mid-2025. Papers and resources from before then I've listed with confidence, including arXiv IDs. For **anything from late 2025 and 2026 I have deliberately not fabricated citations** — instead, building that portion of the reading list is your Week 1 Friday assignment. That's not me passing off work: a specialist who can't identify what's important in the last twelve months isn't current, and the skill of finding it is more durable than any list I could hand you. Items marked **[VERIFY]** existed as of my knowledge but should be confirmed as still current.

---

## 1. LLM mechanical foundations

Work through these in Week 1. The goal is mechanical intuition, not familiarity.

| Resource | Time | Why, for you |
|---|---|---|
| **Karpathy — "Deep Dive into LLMs like ChatGPT"** (YouTube, ~3.5 hrs) | 3.5 hrs | The single best explanation of the full pipeline — pretraining through post-training — for someone with engineering background but no ML background. If you watch one thing, this. **[VERIFY]** |
| **Karpathy — "Let's build the GPT Tokenizer"** + the `minbpe` repo | 2 hrs | Tokenization is the source of a surprising share of LLM failures. Week 1 Tuesday. |
| **3Blue1Brown — Neural Networks, chapters on transformers and attention** | 1.5 hrs | Best visual intuition for attention that exists. Watch before Alammar. |
| **Jay Alammar — The Illustrated Transformer** | 45 min | The canonical written explanation. Still holds up. |
| **Karpathy — "Let's build GPT from scratch"** | 2 hrs | Optional but high value if you want to have actually written attention once. |
| **Stanford CS336 — Language Modeling from Scratch** | ~30 hrs if pursued | Far deeper than this program needs. Listed as the on-ramp if you later want genuine ML depth. **[VERIFY]** materials are public. |

Skip: anything titled "LLMs explained simply." You're past it.

---

## 2. Papers, by theme

Read primary sources. The gap between you and the median candidate is that they read a summary.

### Core architecture and scaling
- **Attention Is All You Need** — [1706.03762](https://arxiv.org/abs/1706.03762) — read it once, properly.
- **Scaling Laws for Neural Language Models** (Kaplan) — [2001.08361](https://arxiv.org/abs/2001.08361)
- **Training Compute-Optimal LLMs** (Chinchilla) — [2203.15556](https://arxiv.org/abs/2203.15556) — why model size alone stopped being the story.
- **LoRA** — [2106.09685](https://arxiv.org/abs/2106.09685) — W13.

### Prompting and reasoning
- **Chain-of-Thought Prompting** — [2201.11903](https://arxiv.org/abs/2201.11903)
- **Self-Consistency** — [2203.11171](https://arxiv.org/abs/2203.11171)
- **Tree of Thoughts** — [2305.10601](https://arxiv.org/abs/2305.10601) — W9.
- **STaR: Self-Taught Reasoner** — [2203.14465](https://arxiv.org/abs/2203.14465) — the conceptual seed of reasoning-model training.
- **DeepSeek-R1** — [2501.12948](https://arxiv.org/abs/2501.12948) — the open account of RL-trained reasoning. W13.
- **DeepSeekMath / GRPO** — [2402.03300](https://arxiv.org/abs/2402.03300) — the algorithm behind much of modern reasoning training.

### Retrieval
- **RAG** (Lewis et al.) — [2005.11401](https://arxiv.org/abs/2005.11401) — W4, the original.
- **ColBERT** — [2004.12832](https://arxiv.org/abs/2004.12832) — late interaction; useful for reasoning about rerankers.
- **HyDE** — [2212.10496](https://arxiv.org/abs/2212.10496) — W5.
- **Self-RAG** — [2310.11511](https://arxiv.org/abs/2310.11511) — W5.
- **Corrective RAG** — [2401.15884](https://arxiv.org/abs/2401.15884) — W5.
- **GraphRAG** (Microsoft) — [2404.16130](https://arxiv.org/abs/2404.16130) — W5.
- **Lost in the Middle** — [2307.03172](https://arxiv.org/abs/2307.03172) — W3, essential.
- **Late Chunking** — [2409.04701](https://arxiv.org/abs/2409.04701) — W4.
- **Matryoshka Representation Learning** — [2205.13147](https://arxiv.org/abs/2205.13147) — why you can truncate embeddings.

### Agents
- **ReAct** — [2210.03629](https://arxiv.org/abs/2210.03629) — W7, the foundational one.
- **Toolformer** — [2302.04761](https://arxiv.org/abs/2302.04761)
- **Reflexion** — [2303.11366](https://arxiv.org/abs/2303.11366) — W9; this is JHU's "verbal RL."
- **Self-Refine** — [2303.17651](https://arxiv.org/abs/2303.17651) — W9.
- **Generative Agents** (Park et al.) — [2304.03442](https://arxiv.org/abs/2304.03442) — W9, memory architecture.
- **MemGPT** — [2310.08560](https://arxiv.org/abs/2310.08560) — W9.
- **Voyager** — [2305.16291](https://arxiv.org/abs/2305.16291) — skill acquisition; W9.
- **AutoGen** — [2308.08155](https://arxiv.org/abs/2308.08155) — W10.

### Alignment, safety, security
- **InstructGPT** — [2203.02155](https://arxiv.org/abs/2203.02155) — the RLHF pipeline. W13.
- **Constitutional AI** — [2212.08073](https://arxiv.org/abs/2212.08073) — W12; JHU's Anthropic masterclass covers this.
- **DPO** — [2305.18290](https://arxiv.org/abs/2305.18290) — W13.
- **Not what you've signed up for** (indirect prompt injection) — [2302.12173](https://arxiv.org/abs/2302.12173) — W12, foundational.
- **Universal and Transferable Adversarial Attacks** (GCG) — [2307.15043](https://arxiv.org/abs/2307.15043) — W12.
- **Sleeper Agents** — [2401.05566](https://arxiv.org/abs/2401.05566) — W12; why safety training can fail to remove behavior.

### Evaluation and benchmarks
- **Judging LLM-as-a-Judge / MT-Bench** — [2306.05685](https://arxiv.org/abs/2306.05685) — W6, essential.
- **Ragas** — [2309.15217](https://arxiv.org/abs/2309.15217) — W5/W6.
- **SWE-bench** — [2310.06770](https://arxiv.org/abs/2310.06770)
- **GAIA** — [2311.12983](https://arxiv.org/abs/2311.12983)
- **τ-bench** — [2406.12045](https://arxiv.org/abs/2406.12045) — tool-agent-user interaction; the most role-relevant agentic benchmark.
- **WebArena** — [2307.13854](https://arxiv.org/abs/2307.13854) and **OSWorld** — [2404.07972](https://arxiv.org/abs/2404.07972) — computer-use evaluation.
- **On the Measure of Intelligence** (Chollet, ARC) — [1911.01547](https://arxiv.org/abs/1911.01547)

### Your Week 1 assignment
Build the **2025–2026 section** yourself. Target 10–15 papers that became reference points in the last twelve months. Start from Hugging Face Daily Papers, alphaXiv trending, the citation graphs of the papers above, and what practitioners you respect are actually citing. Add them to this file with a one-line note on why each matters. Revisit every Friday.

---

## 3. Engineering writing that beats most papers

For production agentic work, the best material is practitioner writing, not academia.

- **Anthropic — "Building Effective Agents"** — the clearest statement of workflow-vs-agent and the standard patterns. Read in W7.
- **Anthropic — "Effective context engineering for AI agents"** — W3's primary source.
- **Anthropic — multi-agent research system write-up** — W10. Read against Cognition's piece.
- **Cognition — "Don't Build Multi-Agents"** — W10. Disagrees with the above productively; holding both is the actual skill.
- **Anthropic — "Writing effective tools for agents"** — W7.
- **Simon Willison — the "lethal trifecta"** and his prompt-injection archive — W12. Nobody explains agentic security more clearly.
- **Hamel Husain — evals writing, especially on error analysis** — W6. The most practically useful eval material available free.

---

## 4. Courses

Selectively. Most are below your level; these aren't.

| Course | Time | Verdict |
|---|---|---|
| **Hugging Face Agents Course** | 8–12 hrs | Good structured coverage; use as W7–W8 reinforcement, not primary. |
| **Hugging Face MCP Course** | 4 hrs | Worth it before W7's MCP server build. **[VERIFY]** |
| **Anthropic courses** (`github.com/anthropics/courses`) | 6–8 hrs | The interactive prompt-engineering tutorial is genuinely good and directly substitutes for JHU's Anthropic masterclass. |
| **Anthropic Cookbook** (`github.com/anthropics/anthropic-cookbook`) | ongoing | Reference, not linear. Highest-value pages: tool use, RAG, evals. |
| **Berkeley LLM Agents MOOC** (Dawn Song) | 15–20 hrs | Lecture series with strong guest speakers; closest free equivalent to JHU's masterclasses. **[VERIFY]** current offering. |
| **DeepLearning.AI short courses** | 1–2 hrs each | Pick 3–4 max, on evals, MCP, and agent frameworks. Skip the rest — they're introductory. **[VERIFY]** which are current. |
| **AWS Skill Builder — free tier GenAI plans** | varies | Do the Bedrock and AgentCore content in W4 and W8. Verify what's free vs subscription. |
| **AWS Workshops** (`catalog.workshops.aws`) | 2–4 hrs each | Best AWS hands-on material available. Search for Bedrock, AgentCore, Strands, Knowledge Bases, Guardrails. Use inside W4/W8. |

---

## 5. Docs worth reading properly, not skimming

**Anthropic:** tool use, extended thinking, prompt caching, context windows, Claude Code docs (skills, hooks, subagents, plugins), Agent SDK. — W2, W7, W15.

**MCP:** the specification itself at `modelcontextprotocol.io/specification` — read the whole thing in W7, not a tutorial about it.

**AWS Bedrock:** Converse API reference, Knowledge Bases, Guardrails, prompt caching, cross-region inference, quotas. — W2, W4, W12, W14.

**AWS AgentCore:** the developer guide at `docs.aws.amazon.com/bedrock-agentcore/latest/devguide/` — Runtime, Memory, Gateway, Identity, Browser, Code Interpreter, Observability, Payments, and the Harness managed agent loop. Also read the **release notes** page, which is the fastest way to see what's shipped recently. — W8, W9, W11.

**Strands Agents:** SDK docs, Python and TypeScript. — W8.

**OpenTelemetry GenAI semantic conventions:** current status and the span/attribute definitions. — W11.

---

## 6. Books

Only two are worth your money.

- **Chip Huyen — *AI Engineering*** (O'Reilly). The best single book for exactly your situation: experienced engineer, needs the systems view of building on foundation models. The evaluation chapters are the strongest part and support Week 6 directly. **Buy this one.**
- One current book on agentic patterns or LLM evaluation published 2025–2026 — **[VERIFY]**, I can't reliably recommend a specific title in that window. Check O'Reilly's recent AI catalog in Week 1 and pick one.

Skip: anything promising to make you an "AI expert in 30 days," and most self-published LLM books.

---

## 7. Currency sources — exactly eight

You said staying current matters and your time is limited. Eight sources, checked Friday mornings in 30 minutes. Resist adding more; the failure mode here is a 40-feed reader you stop opening.

| Source | Cadence | Why this one |
|---|---|---|
| **Simon Willison's blog** — simonwillison.net | daily-ish | Highest signal-to-noise in the field for practitioners. Skeptical, specific, tests things himself. If you read one source, this. |
| **Anthropic Engineering blog** | ~monthly | Where agentic best practice actually gets defined right now. |
| **AWS ML Blog + What's New (Bedrock/AgentCore filter)** | weekly | Non-negotiable for your job. What's New is the authoritative GA-date source. |
| **Sebastian Raschka — Ahead of AI** | ~monthly | Best technical explainer of new architectures and training methods. Fills your ML-depth gap. |
| **Latent Space** (newsletter + podcast) | weekly | Best coverage of the AI engineering practitioner scene. Good for hearing how builders actually talk. |
| **Hamel Husain's blog** | occasional | Evals and error analysis. Low volume, high value. |
| **Artificial Analysis** — artificialanalysis.ai | as needed | Independent model benchmarks, pricing, and latency comparisons. Your reference when a customer asks "which model." |
| **Hugging Face Daily Papers** | daily, skim | Your paper-discovery funnel. Read titles, open one or two a week, no guilt about the rest. |

**Explicitly not recommended:** AI Twitter/X as a primary source (high noise, strong hype gradient), LinkedIn AI commentary, and aggregator newsletters that summarize the above with less accuracy. If something matters, it will reach you through these eight within a week.

---

## 8. Where to put your Friday frontier-watch notes

One file, `FRONTIER-LOG.md`, at your repo root. Append weekly with the date and three sections: what shipped, what it changes for customers you advise, and what you want to try. Sixteen entries by December is both a genuine knowledge base and — when you're asked "how do you stay current?" — a far better answer than a list of newsletters.
