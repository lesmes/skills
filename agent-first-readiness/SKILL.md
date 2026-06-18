---
name: agent-first-readiness
description: >
  Evaluates whether a product, service, or API is well designed to be consumed by AI agents.
  Produces an assessment with a score, gaps, and concrete actions. Use whenever the user
  mentions: validate for agents, agent-first, agent-ready, design for agents, "is my product
  ready for agents?", "can agents use this?", agent consumption, agent interface, agentic
  distribution, awareness for agents, desire paths, scaffold-LM, or any variant of "is my
  proposal well framed for agents to use it?". Also trigger when the user has a PRD, proposal,
  spec, or product idea and wants to know whether an agent would discover it, use it, and prefer
  it over doing the job itself. Triggers (English and Spanish): "is this agent-ready?",
  "validate for agents", "will agents use this?", "agent-first assessment", "would an agent
  find it?", "is this good for agents?", "evaluate my product for agents", "agent readiness check".
---

# Agent-First Readiness Assessment v1

Evaluates whether a product, service, or API is well designed to be discovered, used, and
preferred by AI agents over the alternative of the agent doing the job itself.

## Credits, sources & license

This skill is an **original synthesis framework** authored by **Lesmes López Peña**
(https://lesmes.com, https://github.com/lesmes/skills). The six-dimension model, the scoring
rubrics, the assessment process, the calibration anchors, and the output format are the
author's own work, released under the **MIT License** (see `LICENSE`).

It builds on concepts from several thinkers, credited where used (these authors contributed
ideas, not this assessment; the borrowed concepts remain attributed to them):
- **Steve Yegge**, "Software Survival 3.0" (survival formula, desire paths, levers)
- **Andrej Karpathy** (CLIs for agents, Skills, "Build for Agents" checklist)
- **Alex Zhang**, "Language Models will be Scaffolds" (scaffold-LMs, the time window)
- **Andrew Ng** (Context Hub / chub, documentation registries for agents, feedback loops)
- **Danila Poyarkov** (figma-use / OpenPencil: single operation, token efficiency, dual output)

## How to use

The user provides a proposal (PRD, spec, idea, existing product). The skill evaluates
six dimensions (the sixth, operational reliability, applies only to products with their own
infrastructure), produces a score, identifies gaps, and proposes concrete actions.

If the user does not provide enough information, ask questions to understand:
1. What the product does
2. Who the end user is (human, agent, or both)
3. What interfaces it has or plans to have (API, CLI, MCP, web, etc.)
4. Where it is documented or how it is discovered
5. What alternative an agent has (doing it itself, going to a competitor)

## The six dimensions

### D1. Discoverability: Does an agent find you?

Evaluates whether an agent (a scaffold-LM operating in a REPL, a coding agent, an
infrastructure agent) can discover that the product exists when it needs it.

**Evaluation questions:**
- Is there a public GitHub repo with readable code? (the code IS the documentation for scaffold-LMs)
- Is there a SKILL.md or structured documentation for LLMs?
- Is it in registries where agents look? (chub/Context Hub, awesome-agent-skills, MCP registries, npm, pip)
- Do usage examples appear in contexts where agents operate? (Vercel, Cloudflare, GitHub Actions)
- Is the naming self-explanatory for an agent that finds it for the first time?
- Does it appear, or would it appear, in LLM training data?

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | Invisible. Exists only as a website for humans or as private documentation. |
| 3-4 | Partially visible. Has API docs but they are not where agents look. |
| 5-6 | Visible. Public repo with docs, but no presence in agent registries. |
| 7-8 | Well positioned. Present on multiple discovery surfaces (GitHub + npm/pip + at least one agent registry). |
| 9-10 | Excellent. Full multi-surface: open source repo + CLI on npm/pip + SKILL.md + chub + MCP registry + examples in real contexts. |

### D2. Consumability: Can an agent use you without friction?

Evaluates whether an agent can invoke the product and obtain useful results without complex
configuration, extensive learning, or manual steps.

**Evaluation questions:**
- How many consumption surfaces does it have? (REST API, CLI, MCP, SDK, programmatic tool calling)
- Does the CLI have dual output? (human-readable by default, `--json` for parsing by agents)
- Can it be used without an API key for exploration? (zero friction to try)
- Are error messages informative for agents? (not "Error 400" but "Try .legal instead")
- How many tokens does a typical operation cost? (<50 tokens CLI = good, >200 tokens MCP/JSON = expensive)
- Does it have desire paths? (aliases, alternative syntaxes, telemetry of failed attempts)
- Do all surfaces expose the same operations? (the single-operation principle)

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | Unusable by agents. Web interface only, or API without docs. |
| 3-4 | Usable with effort. Documented API but no CLI, no --json, no desire paths. |
| 5-6 | Functional. API + CLI or MCP. But inconsistent surfaces or auth friction. |
| 7-8 | Good experience. Consistent multi-surface, dual output, informative errors, low friction. |
| 9-10 | Excellent. Single operation across all surfaces, ~50 tokens/op, active desire paths, automated feedback, zero friction to explore. |

### D3. Value vs. Alternative: Why would an agent use you instead of doing it itself?

This is the most critical dimension. A scaffold-LM with access to a REPL can research at
runtime, call APIs directly, and build ad hoc solutions. The question is not whether the agent
CAN do your job. It is whether it PREFERS to use your product because it is faster, cheaper,
or more reliable than the alternative.

**Evaluation questions:**
- How many distinct API calls would an agent have to make to replicate your result? (1-3 = weak, 10+ = strong)
- Does your product pre-compute something the agent would otherwise compute at runtime? (index, aggregation, comparison)
- How long would it take the agent to do it itself? (<30s = weak, >5min = strong)
- Does your product have data that is not in training data? (proprietary data, real-time data, human curation/taste)
- Is the value one of impossibility (the agent CANNOT do it) or convenience (it CAN but it is faster with you)?
- Is the value window permanent or temporary? (will scaffold-LMs close the gap over time?)

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | No value. The agent can do exactly the same in seconds. |
| 3-4 | Weak value. Saves some time but the agent can replicate it easily. |
| 5-6 | Moderate value. Saves significant effort but the window is temporary. |
| 7-8 | Strong value. Pre-computes something costly to replicate at runtime. Alternative-cost moat. |
| 9-10 | Critical value. Impossible or absurdly expensive to replicate. Regulatory, contractual, or permanent proprietary-data moat. |

**Note on the time window (Zhang):** If the value is one of convenience (not impossibility),
document the estimated window and which additional moats are being built (switching cost,
regulatory, network effect) before the window closes.

### D4. Open Source Strategy: What do you open and what do you close?

A scaffold-LM navigates GitHub the way a developer navigates Stack Overflow. What it finds in
public repos, it uses. What it does not find, does not exist for it. Open source strategy is not
"being generous". It is designing the acquisition funnel for agents.

**Principle:** Open everything that teaches the agent to use you. Close everything that makes
you necessary.

**Evaluation questions:**
- Is there public code a scaffold-LM can read to understand what the product does? (CLI, SDK, examples)
- Is there a public schema of the data/responses? (the value teaser, not the full data)
- Is there a free subset or sample that lets it try before buying? (data freemium)
- Are the core data/logic protected behind the API? (do not give away the main asset)
- Are credentials and third-party integrations closed? (what cannot be replicated in 3 minutes)

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | Everything closed. No public code. Agents do not know you exist. |
| 3-4 | Public docs but no readable code. Agents read the README but cannot inspect the implementation. |
| 5-6 | Open source CLI or SDK. Agents read the code and understand the API. But no schema or data sample. |
| 7-8 | Good strategy. Open code (CLI + SDK + examples) + schema + data sample. Core protected behind the API. |
| 9-10 | Excellent. Full funnel: readable code -> schema -> sample -> free trial -> full paid API. The repo is the acquisition product; the API is the monetization product. |

### D5. Defensibility: Do you survive when agents improve?

Scaffold-LMs will be increasingly able to do things by themselves. Does your product have moats
that survive that improvement?

**Evaluation questions:**
- Is there a regulatory moat? (certifications, licenses, accreditations that cannot be replicated with code)
- Is there a cumulative switching cost? (the more users/data, the more painful to migrate)
- Does the index/data moat strengthen with scale? (more integrations = more expensive to replicate at runtime)
- Is there a network effect? (more users -> more value for everyone)
- Do you have a chained-moats strategy? (temporary moat -> cumulative -> permanent)
- Do you monitor the erosion of your advantage? (do you know when agents start being able to do your job?)

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | No defenses. Any agent can replicate your product in minutes. |
| 3-4 | Temporary moat. Data or index that erodes with better scaffold-LMs. No evolution plan. |
| 5-6 | Temporary moat + plan. Value window identified, with a strategy to build more durable moats before it closes. |
| 7-8 | Chained moats. Temporary (data/index) -> cumulative (switching cost/portfolio) -> on the way to permanent (regulatory/contractual). |
| 9-10 | Permanent moat active. Regulatory, contractual, or network effect that no agent can replicate. |

### D6. Operational Reliability: Can you serve agents consistently?

Evaluates whether the infrastructure behind the product can sustain real agentic consumption:
bursty traffic, high concurrency, and an expectation of continuous availability. An agent does
not tolerate downtime or degradation. It simply finds an alternative and does not come back.

**Applicability**: this dimension applies only to products with their own infrastructure that
serve requests (SaaS, APIs, platforms). It does NOT apply to libraries, local CLIs, SDKs, or
products at the idea/concept stage. When it does not apply, mark it as N/A and exclude it from
the composite score.

**Three possible states per question:**
- **Evaluable**: the user has data or can answer -> score normally
- **Not applicable**: the product has no infrastructure of its own -> dimension excluded (N/A)
- **Unknown**: it is a SaaS but the user lacks the data -> score as risk (conservative 3-4)
  with a "pending validation" note

**Evaluation questions:**
- Is response latency predictable and low? (P95 < 500ms is the threshold below which an agent
  does not consider doing it itself)
- Does the service scale under bursts without degradation? (an agent can generate 50 requests
  in 10 seconds; 200 concurrent agents is a realistic medium-term scenario)
- Are there mechanisms to detect and correct quality degradation? (model drift, stale data,
  obsolete indexes. The agent does not warn you; it just stops using you)
- Can you deploy without downtime? (every minute of API downtime is an agentic consumer that
  finds an alternative and may not return)
- Do you have intelligent rate limiting that distinguishes legitimate agents from abuse?
  (rate limiting that is too aggressive blocks your best consumers; too permissive exposes you)

**Scoring:**
| Score | Description |
|-------|-------------|
| 0-2 | Fragile. Frequent downtime, unpredictable latency, no scaling. Agents abandon you fast. |
| 3-4 | Basic. Works under normal conditions but degrades under agentic load. No drift detection. |
| 5-6 | Functional. Acceptable latency, scales reasonably, but no intelligent rate limiting or zero-downtime deploys. |
| 7-8 | Robust. P95 < 500ms, scales under bursts, zero-downtime deploys, active degradation detection. |
| 9-10 | Excellent. All of the above + intelligent rate limiting by consumer type + explicit SLAs for agents + proactive monitoring of response quality. |

**Note:** If the user cannot answer these questions, that itself is a signal. A product that
does not know its P95 or has not tested agentic load has unquantified operational risk.

## Assessment process

### Step 1: Classify the product

Before evaluating, classify:
- **Type**: Tool for agents / SaaS for humans / Infrastructure / Platform / Hybrid
- **Primary channel**: Agent-first / Human-first / Dual
- **Stage**: Idea / MVP / Existing product

### Step 2: Evaluate the dimensions

For each dimension, assign a score of 0-10 with a brief justification.
D6 (Operational reliability) is evaluated only if the product has its own infrastructure.

### Step 3: Compute the composite score

```
If D6 applies:    Score = (D1 + D2 + D3 + D4 + D5 + D6) / 6
If D6 = N/A:      Score = (D1 + D2 + D3 + D4 + D5) / 5
If D6 = Unknown:  score D6 as 3-4 (risk) and divide by 6
```

| Score | Category | Meaning |
|-------|----------|---------|
| 8-10 | 🟢 Agent-Ready | The product is well designed for agents. Minor adjustments. |
| 6-7.9 | 🟡 Almost ready | Solid base but with important gaps in 1-2 dimensions. |
| 4-5.9 | 🟠 Needs work | Significant gaps across multiple dimensions. Requires partial redesign. |
| 0-3.9 | 🔴 Not ready | The product is not designed for agents. Requires fundamental rethinking. |

### Step 4: Identify critical gaps

List the dimensions with a score <5 as critical gaps. For each gap, propose 2-3 concrete
actions with estimated effort (low/medium/high) and estimated impact (low/medium/high).

### Step 5: Generate an action roadmap

Order actions by impact/effort ratio. Prioritize "quick wins" (high impact, low effort).

## Output format

```markdown
# Agent-First Readiness Assessment

**Product**: [name]
**Type**: [classification]
**Date**: [date]

## Score: X.X/10 — 🟢/🟡/🟠/🔴 [Category]

### Dimensions

| # | Dimension | Score | Summary |
|---|-----------|-------|---------|
| D1 | Discoverability | X/10 | [1 sentence] |
| D2 | Consumability | X/10 | [1 sentence] |
| D3 | Value vs. Alternative | X/10 | [1 sentence] |
| D4 | Open Source Strategy | X/10 | [1 sentence] |
| D5 | Defensibility | X/10 | [1 sentence] |
| D6 | Operational Reliability | X/10 or N/A | [1 sentence] |

### Critical gaps

[For each dimension <5, explain the gap and propose actions]

### Quick wins (high impact, low effort)

1. [Action] — Effort: X, Impact: X
2. ...

### Medium-term actions

1. [Action] — Effort: X, Impact: X
2. ...

### Key question

> [The most important question the product must answer to improve its readiness]
```

## Quick checklist (for an express evaluation)

If the user wants a quick check without a full assessment, use this checklist:

- [ ] Does it have a documented REST API?
- [ ] Does it have a CLI published on npm or pip?
- [ ] Does the CLI have dual output (readable + --json)?
- [ ] Does it have a SKILL.md?
- [ ] Is it on Context Hub (chub)?
- [ ] Is it in any skills/MCP registry?
- [ ] Does it have a public repo with readable code?
- [ ] Are errors informative for agents?
- [ ] Can it be used without an API key to explore?
- [ ] Do all surfaces expose the same operations?
- [ ] Does it pre-compute something the agent would otherwise do at runtime?
- [ ] Does it have a moat that survives better scaffold-LMs?
- [ ] Is latency P95 < 500ms? (if applicable, N/A if it has no infrastructure of its own)
- [ ] Does it scale under bursts without degradation? (if applicable)
- [ ] Does it deploy without downtime? (if applicable)

Each ✅ = 1 point. N/A items are excluded from the total.
Quick score: X / [applicable items].
- >80%: 🟢 Agent-Ready
- 60-80%: 🟡 Almost ready
- 40-60%: 🟠 Needs work
- <40%: 🔴 Not ready

## Calibration anchors

To calibrate scores, use these reference examples:

| Product | D1 | D2 | D3 | D4 | D5 | D6 | Total | Notes |
|---------|----|----|----|----|----|----|-------|-------|
| Stripe | 9 | 9 | 9 | 7 | 9 | 9 | 8.7 | Gold standard. CLI + SDK + docs + chub + regulatory moat + world-class infrastructure. |
| Cloudflare Workers | 8 | 8 | 7 | 8 | 8 | 9 | 8.0 | Very good. Multi-surface, published Skills, ultra-reliable own infrastructure. |
| Vercel | 7 | 8 | 6 | 7 | 6 | 8 | 7.0 | Good but replicable. Solid infrastructure, but the agent can deploy without Vercel. |
| Generic domain registrar (e.g., Namecheap) | 4 | 4 | 4 | 3 | 5 | 5 | 4.2 | API exists but not optimized for agents. No CLI, no Skills. Functional infrastructure. |
| Web-only SaaS without API | 1 | 1 | 3 | 1 | 3 | 3 | 2.0 | Invisible and unusable for agents. |
| Open source CLI (e.g., jq, ripgrep) | 8 | 9 | 7 | 9 | 7 | N/A | 8.0 | No infrastructure of its own. D6 N/A. Score over 5 dimensions. |
