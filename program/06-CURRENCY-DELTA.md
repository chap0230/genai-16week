# Currency Delta Log

**A living record of what changed since the program was authored, and what each change does to the plan.**

You asked that nothing reach you without a freshness check first. This file is where those checks land. Each entry is dated, states what was verified against a live source, and says which week it affects. Append — never overwrite. By December this is also a genuine artifact: sixteen weeks of tracked platform movement, which is a better answer to "how do you stay current?" than any list of newsletters.

The scheduled tasks now run this check before every session. Anything they find gets appended here.

---

## 2026-08-20 — Initial verification pass

Checked against live AWS documentation and What's New on the day the program was authored. **Findings were significant.** My training knowledge runs to roughly mid-2025; the AWS agentic platform moved substantially in the fourteen months since, and several things in the original program were written against a platform that no longer exists in that shape.

A useful illustration of the problem: I'm running as **Claude Opus 5**, a model that postdates my own training data. I cannot see the current model landscape from the inside. That's the whole argument for this file.

### Confirmed correct — no change needed

- `npm install -g @aws/agentcore` is the current AgentCore CLI install. Verify with `agentcore --version`; update with `agentcore update`.
- AgentCore components as listed, including Payments and the Harness.
- Python 3.12+ with `uv` is fine (docs say 3.10+ minimum).

### Corrections to the program as written

**Node version.** The program said Node 20+. That's correct for the Python CLI path, but the **TypeScript** path requires **Node 22+**. Weeks 8 and 15 do TypeScript work. → Install Node 22+. *(Already corrected in `00-PROGRAM.md`.)*

**The Bedrock API surface is no longer just Converse/InvokeModel.** There is now a **`bedrock-mantle` endpoint** exposing the **OpenAI Responses API, OpenAI Chat Completions API, and Anthropic Messages API** natively, with Bedrock API keys and a redesigned console built around them (June 2026). Week 2 was written as "Converse API as the engineering surface." That's now one of *several* surfaces, and choosing between them is a real architecture question a customer will ask you.
→ **W2 change:** keep Converse as the primary teaching vehicle, but Tue AM now includes the mantle endpoint, and the W2 deliverable should call the same model through **both** Converse and an OpenAI-compatible client, with a written note on when each is the right choice. Portability from OpenAI-based code to Bedrock is a migration conversation you will have repeatedly.

### Major additions the program must absorb

**AgentCore Policy — GA, Cedar-based (Dec 2025).** Real-time, deterministic authorization on every agent tool call, intercepted at AgentCore Gateway. Write policies in natural language, auto-convert to **Cedar**, then review the generated Cedar. Supports `permit`/`forbid`, conditions on tool inputs, time-based/temporal policies, and guardrails-in-policies. CLI: `agentcore add policy --generate` or `--source`.

```
permit(principal,
  action == AgentCore::Action::"RefundTarget___process_refund",
  resource == AgentCore::Gateway::"<gateway-arn>")
when {
  context.input.amount < 1000
};
```

This is the single most important thing I missed, for two reasons. First, deterministic policy enforcement on non-deterministic callers is *exactly* the problem your background makes you good at. Second — note what it does to the gap analysis: I reframed JHU's neuro-symbolic module as "use deterministic code to validate probabilistic output" and argued the academic framing wasn't load-bearing. Cedar is a formal, verifiable authorization language sitting in the agent's tool path. That reframing turns out to be more literally correct than I knew when I wrote it.
→ **W12 change:** Mon PM and Tue PM now build Cedar policies over the Project 2 gateway. This partly displaces hand-rolled guard code. **W8** gets Policy in the Gateway session. Add to the W12 gate: your threat model must state which controls are probabilistic (guardrails, prompts) and which are deterministic (Cedar, IAM), because conflating those is the most common enterprise mistake.

**AgentCore Evaluations — preview (Dec 2025), plus optimization (May 2026).** Far more built out than the program assumes:

- **13 built-in evaluators** at three scopes. Session: `GOAL_SUCCESS_RATE`. Trace: `HELPFULNESS`, `CORRECTNESS`, `FAITHFULNESS`, `HARMFULNESS`, `STEREOTYPING`, `REFUSAL`, `COHERENCE`, `RESPONSE_RELEVANCE`, `CONCISENESS`, `INSTRUCTION_FOLLOWING`. Tool-call: `TOOL_SELECTION_ACCURACY`, `TOOL_PARAMETER_ACCURACY`. Referenced as `Builtin.EvaluatorName`.
- **Trajectory evaluators** — `Builtin.TrajectoryExactOrderMatch`, `TrajectoryInOrderMatch`, `TrajectoryAnyOrderMatch`. Programmatic, **zero token cost**. Week 11 has you hand-building precisely this.
- On-demand, batch, and **online** evaluation; third-party evaluators from OSS libraries; custom evaluators; **skill evaluators** for skill-loading tool calls.
- CDK support via `aws_bedrockagentcore` (`OnlineEvaluationConfig`, `DataSourceConfig.fromCloudWatchLogs`); SDK `from bedrock_agentcore.evaluation import EvaluationClient, ReferenceInputs`; CLI `agentcore run eval --evaluator-arn ...`.
- **Optimization (preview, May 2026):** generates system-prompt and tool-description recommendations from your production traces, validates them with batch evals, then A/B tests against test sets or live traffic with statistical significance reported. Every recommendation requires human approval.

→ **W6 and W11 change, but do not shrink.** Build the harness by hand first — you cannot judge a managed evaluator you've never had to implement, and the calibration work in W6 is the transferable skill. Then, on Wednesday of each week, port to the managed service and write the comparison. That comparison memo is more valuable than either half alone, and "I built it, then I replaced it with the managed service and here's the tradeoff" is a Specialist SA answer. The optimization loop belongs in **W15** next to cost modeling, since prompt/tool optimization is a cost lever as much as a quality one.

**AgentCore Harness — preview (April 2026).** Declare model, system prompt, and tools; it runs the full agent loop with no orchestration code, plus filesystem and shell access. Model-agnostic, and **exportable to Strands code** when you need control. **Filesystem persistence (preview)** externalizes session state so agents can suspend and resume.
→ **W7 change:** the from-scratch build stays, and stays first — writing the loop yourself is the point of that week. Add Friday: run the same task on the Harness and write what the managed loop takes away and what it gives back. Suspend/resume is directly relevant to **W13** — externalized session state is what makes an agent recoverable across a regional failure, and it's a much stronger answer than anything I'd have had you build by hand.

**AgentCore skills for coding assistants — via Kiro Power, with Claude Code, Codex, and Cursor support.** Pre-built skills that give coding assistants AgentCore guidance directly, and a CLI optimized for coding-assistant control.
→ **W15 change:** this is now the centerpiece of toolchain week rather than a footnote. It is the exact intersection of your two goals — expert operator and AWS specialist — and it is what "agentic AI in your own workflow" now concretely means on AWS.

**Smaller items, folded into their weeks.** AgentCore **Memory** gained **episodic memory** (W9 — this is the "learn and adapt across sessions" primitive that week is about). **Runtime** gained **bidirectional streaming** (W8). **Identity** gained custom claims (W12). **Browser** gained Chrome policies — 100+ configurable, including URL allow/blocklists and kiosk mode — and **custom root CA** support (W12, and it partly closes the computer-use soft spot the gap analysis flagged). Policy, memory, and harness are also now in **GovCloud (US-West)**, which matters for your public-sector conversations.

**Strands has moved.** Python SDK reached **1.0** (GA, out of the May 2025 preview) with four multi-agent primitives, **A2A protocol support**, a session manager for remote state, and improved async throughout. **TypeScript 1.0 shipped April 2026.** The repo is now `strands-agents/harness-sdk`.
→ **W8 and W10:** use the 1.0 multi-agent primitives rather than composing agents by hand, and use the session manager for Project 2's state. Don't pin SDK versions in your notes — check current on the day.

**Model landscape (verify in-console, do not trust this list past today).** Claude **Sonnet 4.6** landed on Bedrock Feb 2026 as a direct Sonnet 4.5 upgrade; **Opus 4.6** is referenced alongside it, and AWS's own migration guidance spans "4.5 → 4.6 → 4.7," so the Claude line has moved at least twice more than I knew. I am myself running as **Opus 5**. **Amazon Nova 2** (Dec 2025): Nova 2 Lite GA with a **1M-token context window**, extended thinking with **three thinking-intensity levels**, and built-in code interpreter and web grounding; Nova 2 Pro in preview via Nova Forge. **Intelligent Prompt Routing** is GA.
→ **W1 Friday baseline:** build your landscape table from the console and from Artificial Analysis, not from `04-RESOURCES.md`. Configurable thinking intensity is a cost/latency lever that didn't exist when W2's cost accounting was designed — add it as a dimension in the W2 harness.

### One resource I didn't know I had

The AWS MCP server in this session exposes retrievable **AWS skills** — curated, current guidance bundles. Two are directly relevant: **`amazon-bedrock`** (Converse vs InvokeModel, Knowledge Bases, Guardrails, AgentCore and the Harness, prompt caching, throttling diagnosis, cost tracking, Claude-generation migration, Payments/x402) and **`aws-ai-ml`** (SFT, DPO, **RLVR**, RLAIF, dataset prep, evaluation, SageMaker deployment — squarely W14). These are maintained by AWS and are more current than anything I can write from memory. Use them as the first stop in W2, W8, and W14 rather than starting from docs search.

---

## 2026-08-25 — W1 Tue AM (tokenization) freshness check

Checked: `amazon-bedrock` AWS skill, Bedrock API reference and user guide, and liveness of every Week 1 resource link. No live AWS credentials in the session today, so nothing was verified against your own account — the console checks stay yours.

### Alters today's work

**`CountTokens` exists on `bedrock-runtime`, and it's free.** Returns the exact input-token count that *would* be billed if the same payload were sent to `InvokeModel` or `Converse`. Accepts either shape via a union: `input={"invokeModel": {"body": "<json str>"}}` or `input={"converse": {...}}`. Requires the `bedrock:CountTokens` IAM action in addition to `bedrock:InvokeModel`. Docs: [count-tokens](https://docs.aws.amazon.com/bedrock/latest/userguide/count-tokens.html), [API_runtime_CountTokens](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_CountTokens.html).

**With a sharp edge worth knowing before you hit it:** Claude models offered on `bedrock-runtime` only through cross-Region inference (CRIS) — which is how the current frontier Claudes ship — **do not support `CountTokens` there**, because there's no Region-specific endpoint for it to target. For those you call Anthropic's own count-tokens API on the **`bedrock-mantle`** endpoint: `POST https://bedrock-mantle.{region}.api.aws/anthropic/v1/messages/count_tokens`, Anthropic request shape (`model`, `messages`, optional `system` and `tools`), SigV4 with service name `bedrock-mantle` or a Bedrock API key. That path is Claude-specific; other models return `does not support the '/anthropic/v1/messages' API`.

→ **W1 Tue change:** the tokenization exercise no longer stops at a GPT-family tokenizer. You can measure the *billed* tokenization of the actual model you'll be calling, which turns "tokenization is model-specific" from an assertion into a number. Added to today's hour.
→ **W1 Tue PM / W2:** the harness gets *pre-flight* token accounting, not just post-hoc `usage`. That's the difference between reporting cost and controlling it.
→ **W3:** the context budget analyzer can be exact rather than estimated. Free, too — so no reason not to.

### Folded in silently

- **`maxTokens` must be set explicitly on every call.** Unset defaults to the model's maximum (e.g. 64K on Sonnet) and *reserves that much quota*, which is the leading cause of surprise `ThrottlingException` at low request rates. Applies to tonight's harness and to W2's quota arithmetic.
- **The endpoint count is five, not the four I implied on 08-20:** `bedrock`, `bedrock-runtime`, `bedrock-mantle`, `bedrock-agent`, `bedrock-agent-runtime`. Refinement to the mantle note above: `bedrock-runtime` *also* serves OpenAI Chat Completions at `/openai/v1`, but **client-side tool use only** — `bedrock-mantle` is the recommended surface for new Chat Completions work and the only one with server-side built-in tools. That distinction is the W2 "when is each the right choice" answer, so don't flatten the two into "there's an OpenAI-compatible endpoint."
- **Bedrock Agents classic is in maintenance mode and closed to new customers.** The 08-20 entry had the migration story but not the lifecycle status. → **W8** oral question 4 gets sharper: the advice isn't "consider migrating," it's that the platform they're on takes no new customers and the target is an AgentCore Harness.
- Cross-region inference profile prefixes are a **data-residency decision**, not just a throughput one: geographic (`us.`, `eu.`, `apac.`) keeps data in-boundary, `global.` routes to any commercial region. → **W13**.

### Link liveness — all Week 1 resources confirmed 200

`github.com/karpathy/minbpe` (README on `master`), Karpathy *Let's build the GPT Tokenizer* (`youtube.com/watch?v=zduSFxRajkE`, title confirmed), `tiktokenizer.vercel.app`. No dead links in Week 1.

---

## How the check runs from here

Each scheduled session, before delivering anything, checks the day's material against live sources — targeted, not vague:

| Week topic | What gets checked |
|---|---|
| W1–2 models, inference, API surface | Bedrock What's New; model catalog in console; `amazon-bedrock` skill; mantle endpoint status |
| W3 context engineering | Anthropic engineering blog; current context-window and caching limits |
| W4–5 retrieval | Knowledge Bases features; chunking options; embedding model catalog |
| W6, W11 evaluation & observability | AgentCore Evaluations status (preview→GA?); evaluator list; OTel GenAI convention status |
| W7–8 agent loop, MCP, frameworks | MCP spec revision; Strands releases; AgentCore Harness and CLI |
| W9 memory | AgentCore Memory (episodic, filesystem persistence) |
| W10 multi-agent | A2A spec; Strands multi-agent primitives |
| W12 security | AgentCore Policy and Cedar; Guardrails; Browser policies; new injection research |
| W13 reliability | AgentCore Runtime regions; cross-region inference; session persistence and failover |
| W14 customization | `aws-ai-ml` skill; Bedrock/SageMaker customization paths; distillation |
| W15 toolchain & cost | AgentCore skills for coding assistants; CLI changes; Bedrock pricing; optimization preview |

**The delivery rule:** adjust the session silently for anything minor, and surface a short "**what changed**" note only when a finding actually alters the day's work. If nothing moved, say nothing — a freshness check that produces daily noise gets ignored, which defeats it.
