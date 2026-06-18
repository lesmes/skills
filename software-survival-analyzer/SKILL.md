---
name: software-survival-analyzer
description: >
  Analyzes the survival probability of software tools, SaaS platforms,
  and technologies in the AI era using Steve Yegge's formula (Software Survival 3.0).
  Use when the user asks whether a tool or SaaS will survive AI, about the future
  viability of software, competitive analysis against AI agents, or comparisons
  of technological survival. Triggers (English and Spanish): "will X survive",
  "future of X", "will AI replace X", "analyze X with the formula", "survival
  ratio", "sobrevivirá X", "futuro de X", "la IA reemplazará X", "analiza X con
  la fórmula", "ratio de supervivencia".
---

# Software Survival Analyzer v5

Analyzes tools and platforms using Steve Yegge's survival formula.

## Credits & attribution

This skill is an **implementation** of the survival framework introduced by
**Steve Yegge** in "Software Survival 3.0" (Medium, January 2026):
https://steve-yegge.medium.com/software-survival-3-0-97a2a6255f7b

- **The framework, the core concepts, and the base formula are Steve Yegge's.**
  This includes the survival question, the Savings / Usage / H / Awareness model,
  the "desire paths" idea, the survival levers, and the notion of "crystallized
  cognition" (which Yegge credits to Brendan Hopper). Short quotations from the
  article are attributed inline.
- **This skill is a derivative operational layer** authored by **Lesmes López Peña**
  (https://lesmes.com, https://github.com/lesmes/skills). The author's contribution
  is the numerical calibration of the formula, the scoring guides, the
  case/benchmark library, the anti-bias checklist, the geographic and language-bias
  adjustments (v4), the prior research phase and maturity filter (v5), and the
  output format. None of these layers are Yegge's.

If you find this useful, read Yegge's original article first. This skill only
operationalizes his thinking; it does not replace it.

## License

The author's contribution is released under the **MIT License** (see `LICENSE`).
This covers the original layer of this skill only. The underlying framework and
short quotations are Steve Yegge's and are used with attribution.

## Model context

Yegge's central question is: **in a world where AI agents write all the software
and choose which tools to use, will your tool survive?** Survival depends on whether
the tool saves the agent cognition (tokens) versus synthesizing the functionality
from scratch.

Yegge frames it as an evolutionary selective pressure: tokens cost energy and money,
so agents will prefer tools that save cognition. Those that do not save it will be
"routed around" and eventually abandoned.

**Disruption timeline** (Yegge's progression):
- 2023: Completions
- 2024: Chat
- 2025: Agents (early)
- 2026: Orchestration (multi-agent)

This timeline helps estimate horizons: software threatened by individual agents has
roughly 1-2 years; software threatened by multi-agent orchestration has roughly 3-4 years.

## Prior Phase · Adapted research (proposed, before Step 0)

> **Why this phase exists**: the model's premise is that the rate of change in the AI
> era is annual (the 2023→2026 timeline itself assumes it). Scoring from frozen
> knowledge contradicts the model's thesis. In addition, research improves the analysis
> **asymmetrically**: it hits the volatile variables (Fc/desire paths, competition,
> trajectory) and barely touches the structural ones (Savings, Usage). It doesn't
> improve everything equally; it improves what moves the most.

**Activation rule (decide BEFORE proposing anything):**

1. **Is there already fresh information in context?** If the user just provided
   research, pasted recent sources, or the conversation already contains the current
   state of the software, **do not propose research**: use what's there and move to
   Step 0. The real gate is "do I have fresh info?", not "is it research time?".
   Proposing it anyway is redundant.
2. **Does the software justify it?** This phase adds little for:
   - Stable infrastructure with high absurdity (PostgreSQL, grep, Git): scores are
     stable by definition; research returns little new signal.
   - Obscure, internal, or private tools with no public information: research returns noise.
   In those cases, acknowledge it and don't insist.
3. **In all other cases** (SaaS, platforms, tools in active evolution, anything with
   live competition), **propose adapted research to the user** before starting, and
   execute it if they accept.

**Research brief adapted to the formula** (not a generic "research the company" brief
— targeted searches tied to the model's concrete inputs):

| Search for | Feeds into | Guiding question |
|------------|------------|------------------|
| Does it have an MCP server / API / SDK / CLI? Docs for agents? Programmatic-surface launches. | **Fc, desire paths (lever 5), Kc** | Does the agent reach it with low friction and know it exists? |
| Recent entrants and competitors; who attacks which layer; how they position. | **Relative competition (Step 7b), anchors** | Has the survival threshold risen? Is there a new competitor to use as an anchor? |
| Launches, pivots, financials, direction signals, leadership statements. | **Trajectory (↑↑/↑/→/↓/↓↓)** | Is the tool improving or worsening its position against agents? |
| Do LLMs natively do what the tool does? Features that generate what a model already generates? | **Intermediation test (0b), Savings** | What percentage of the value intermediates a task the AI already does? |

**Mandatory research filter (announced ≠ shipped ≠ adopted):**

Research introduces **recency and marketing bias** if not filtered. Before incorporating
any finding into the scoring, classify by maturity:

- **Announced**: the press release exists, not the product. Near-zero weight in scoring.
- **Shipped but beta/early**: it exists but it's immature. Don't move a variable to the
  extreme because of this. Example: a beta MCP server justifies lowering Fc, but not to
  the level of a mature API (Stripe, Vercel).
- **Shipped and adopted**: evidence of real usage (metrics, cases). Full weight.

Beware of the inverse mirage: new features can **worsen** the profile even when they
look like momentum. Example: product expansion that adds intermediation-exposed surface
raises test 0b instead of strengthening the moat. More features ≠ better survival.

**Output of this phase:**

- Filtered findings feed Step 0 (a new competitor becomes an anchor) and the scoring of
  Fc, Kc, competition and trajectory.
- **Baseline vs. updated pattern**: if the software already has an entry in
  `references/known-cases.md`, do NOT mentally overwrite the baseline. Present **two
  scenarios side by side** (frozen entry vs. fresh evidence) and explain which variables
  change and why. The entries in the reference file are baselines from the last
  calibration, not permanent truth.
- When the research justifies a stable change, **propose to the user that the entry be
  updated** in `references/known-cases.md` (with a calibration date), so that the
  reference file doesn't fall stale exactly in a domain where freshness is the point.

## Step 0: Binary Tests (mandatory)

Before scoring anything, answer TWO binary questions:

### 0a. Absurdity Test

> **"Would it be absurd for an AI agent to try to re-synthesize this from scratch?"**

- **YES, it would be absurd** → Strong survival signal. Example: re-synthesizing
  PostgreSQL, Git, or Kubernetes from scratch would be "nuts" (Yegge). Proceed with
  the numerical analysis expecting a high ratio.
- **NO, it would not be absurd** → Warning sign. The agent can produce something
  equivalent with little effort. The ratio will be low unless H (the human coefficient)
  protects it.
- **DEPENDS** → The tool has components that would indeed be absurd to re-synthesize
  and others that would not. Analyze them separately if possible.

The complementary calibration question (Yegge): **how many decades of human
trial-and-error does this tool have compressed inside it?** Software with high
knowledge compression is "crystallized cognition", a real financial asset, just as
money is crystallized human labor (Brendan Hopper via Yegge). If the answer is "none"
or "little", the absurdity test is probably a NO.

### 0b. Intermediation Test

> **"Does this software intermediate between humans and cognitive tasks that the AI will do on its own?"**

Yegge is explicit: *"any software that's intermediating between humans and AIs, or is trying
to do any sort of 'smart thing' that AIs will soon be able to do themselves, is in real trouble."*

- **YES, it intermediates** → A warning sign as strong as failing the absurdity test.
  Includes: LLM wrappers, tools that do OCR/classification/generation that LLMs do natively,
  visual automation that agents can code directly.
- **NO, it does not intermediate** → Good. The software offers its own value; it is not an
  unnecessary layer.
- **PARTIALLY** → Identify which parts intermediate (vulnerable) and which do not (resistant).
  **Estimate what percentage of the product's value lies in the part that intermediates.**
  If >60% intermediates → treat as YES for the forecast.
  If <40% intermediates → moderate warning sign, not blocking.
  If 40-60% → gray zone, document it and reflect it in the Savings score.

**Both tests must be documented** in the analysis. If a piece of software fails BOTH tests
(it is not absurd to re-synthesize it AND it intermediates), the forecast rarely rises above
🟠 At risk, even with high H.

## Taxonomy: Types of software/service

Yegge's model talks about tools that AGENTS use. But not all software is a tool for agents.
It is crucial to classify first:

| Type | Description | How the model applies |
|------|-------------|----------------------|
| **Tool for agents** | CLI, API, library, SDK that agents use directly | Core case of the model. Applies directly. |
| **Infrastructure/substrate** | Hosting, cloud, CDN, DNS, servers | The agent does not "use" the hosting; it deploys ON it. Evaluate the provider's programmatic interface (API), not the underlying service. |
| **SaaS for humans** | CRM, PM tools, analytics, email marketing | The agent can replicate the functionality but not the user base. H is crucial. |
| **Platform/Marketplace** | Intermediaries, app stores, aggregators | Network effect protects it. But if it intermediates between humans and AI, high risk (test 0b). |
| **Content tool** | Text/image generators, writing assistants | HIGH RISK. If it does "smart things that LLMs already do", it is threatened (test 0b). |
| **Social infrastructure** | Social networks, communication, communities | Protected almost exclusively by H. The base ratio may be low but H saves it. |

**Important**: Many products are hybrids. A hosting provider with a clean API (Cloudflare) is
evaluated differently from one without an API (legacy web panel). Identify the type BEFORE scoring.

## The Formula (v2 — corrected and calibrated)

### Base Ratio (pure cognitive efficiency)

```
Base_ratio = (Savings × Usage) / ((Knowledge_cost + Friction_cost) × 10)
```

### Human Coefficient (separate modifier)

H does NOT multiply the base ratio. It is an **independent protective force** that can
raise the forecast category. Yegge describes it as "a different selection pressure
entirely — human preference instead of efficiency."

```
Final_forecast = Category(Base_ratio) + H_boost
```

Where H_boost is computed according to the H table further below.

### Why H is not multiplicative

In v1, H multiplied the ratio, which caused serious distortions:
- Slack (Savings=30, H=85) gave a ratio of ~77 (higher than Docker=80), which is absurd:
  an agent does not "need" Slack as a tool.
- Notion (H=60) gave more than Kubernetes, when in reality K8s is more critical for agents.

Separating H reflects reality better: Slack survives not because it is efficient for agents,
but because humans want it. They are distinct survival forces.

## Variables

| Variable | Meaning | Scale | Key question |
|----------|---------|-------|--------------|
| **Savings** | Tokens saved vs. synthesizing from scratch | 0-100 | How much cognition does the agent save by using this instead of doing it itself? |
| **Usage** | Breadth of application across different contexts | 0-100 | In how many different situations would an agent choose this tool? |
| **Knowledge_cost** | Energy for agents to know the tool | 1-100 | Is it in the training data? Does it need a lot of prompting? |
| **Friction_cost** | Errors, retries, difficulty of use by agents | 1-100 | Does it have "desire paths"? Or does the agent get frustrated and abandon it? |
| **H** | Human coefficient (independent protective force) | 0-100 | Does the value depend on humans being involved? |

### Savings scoring guide

The calibration question: **how many decades of human trial-and-error does it have compressed?**
Yegge (via Brendan Hopper): software with high compression is "crystallized cognition",
equivalent to a financial asset. The more decades compressed, the more absurd it would be to
rediscover it.

| Score | Description | Example | Decades compressed |
|-------|-------------|---------|-------------------|
| 80-100 | Re-synthesizing would be absurd. Decades of crystallized knowledge. | PostgreSQL, Git, Stripe | 20-40+ years |
| 60-80 | Significant savings. Complex problem well solved. | Docker, Kubernetes, Temporal | 10-20 years |
| 40-60 | Moderate savings. Simplifies tasks but agents could manage. | Vercel, Zapier | 5-10 years |
| 20-40 | Little savings. The agent can do something equivalent quickly. | Low-code tools, basic hosting | 1-5 years |
| 0-20 | No savings or negative. The LLM already does this natively. | Grammarly, Chegg, LLM wrappers | 0 (or negative) |

**Note on regulatory/institutional savings** (v4): There is a type of savings that is not
algorithmic but regulatory or institutional: legal certifications, agreements with banks,
country-specific regulatory compliance. This savings is REAL (an agent cannot obtain a
certification from the tax authority nor sign banking contracts) but it is qualitatively
different from Yegge's "insight density" (Git, PostgreSQL). Calibration guide:

| Type of savings | Typical range | Example | Vulnerability |
|-----------------|---------------|---------|---------------|
| **Algorithmic/engineering** (insight density) | 60-100 | Git, PostgreSQL, Temporal | Low: decades of knowledge hard to rediscover |
| **Regulatory/institutional** | 30-50 | Certified tax ERP, regulated payments platform | Medium: regulation can be encoded by agents trained on it |
| **Integrations/agreements** | 20-40 | Banking APIs, partnerships, catalogs | Medium-high: APIs open up, agreements get replicated |
| **Interface/UX** | 10-30 | Pretty dashboards, intuitive forms | High: value only for humans, invisible to agents |

Do not confuse "the product has many features" with "the product saves cognition for agents".
An ERP with 50 modules still has low Savings if an agent can replicate each module individually
with little effort.

### Usage scoring guide

| Score | Description | Example |
|-------|-------------|---------|
| 80-100 | Universal. Almost every project needs it. | SQL, Git, grep |
| 60-80 | Very broad. Most serious projects use it. | Docker, Stripe, Slack |
| 40-60 | Broad niche. Many projects but not most. | Figma, Jira, Postman |
| 20-40 | Specific niche. Only certain types of projects. | Local hosting, vertical tools |
| 0-20 | Ultra-niche. Very limited use cases. | Industry-specific software |

**Geographic scope penalty** (v4): Agents operate globally. A tool that is only relevant
in a specific country or region has restricted utility from an agent's perspective, even if
it dominates its local market.

| Scope | Adjustment to Usage | Example |
|-------|---------------------|---------|
| Global | No adjustment | Stripe, Docker, Slack |
| Multi-region (3+ countries) | -5 to -10 | SAP (Europe), Xero (ANZ+UK+US) |
| One large country | -15 to -25 | Holded (Spain), Conta Azul (Brazil) |
| One small country | -20 to -30 | Norwegian ERP, Uruguayan invoicing |

Practical example: An ERP that every Spanish SMB uses might look like Usage=60 ("broad niche")
but from the perspective of global agents it is Usage=35-40 (specific niche in one country).
**Calibration question**: would an agent operating for a company in Japan choose this tool?
If the answer is "no, because it only applies in Spain", lower Usage.

### Cost scoring guide

| Score | Description (Knowledge_cost) | Description (Friction_cost) |
|-------|------------------------------|------------------------------|
| 1-10 | Omnipresent in training data | Perfect "desire paths". Zero friction. |
| 10-25 | Well documented, present in many tutorials | Clean API, clear errors, good DX |
| 25-50 | Known but not ubiquitous. Needs some prompting. | Learning curve but manageable |
| 50-75 | Little known. Requires in-context documentation. | Confusing interface, frequent errors |
| 75-100 | Unknown to agents. Requires teaching from scratch. | Visual interface without API, impossible for agents |

**Note on language bias in Knowledge_cost** (v4): LLMs are trained predominantly in English.
Software popular in non-English-speaking markets (Spain, France, Germany, Japan, Brazil...)
can have a Knowledge_cost **15-25 points higher** than its local market share suggests.

Calibration question: **If you ask an English-language LLM to solve a problem in this domain,
would it mention this tool spontaneously?** If the answer is no, Knowledge_cost >= 35.

Examples:
- Stripe → any LLM mentions it for payments → Knowledge_cost=10
- Holded → no global LLM mentions it for invoicing → Knowledge_cost=35-45
- SAP → mentions it but with friction ("too complex") → Knowledge_cost=25-30

Do not confuse "popular among humans in my country" with "present in the training data of LLMs".
They are very different things.

### H scoring guide (Human Coefficient)

H does NOT measure whether the software is "for humans". Almost all software is for humans in
some way. H measures: **does the value of this software depend SPECIFICALLY on humans being
involved in its creation, curation, or interaction?**

| Score | Type of human value | Example |
|-------|---------------------|---------|
| 80-100 | **Social interaction**: the product IS the connection between humans | Social networks, multiplayer games, dating apps |
| 60-80 | **Creativity/judgment**: it is specifically valued that a human made it | Figma (design), Notion (personal curation), craft marketplaces |
| 40-60 | **Trust/oversight**: a human is needed to validate/approve | Jira (coordination), payments (trust), medical platforms |
| 20-40 | **Customer support**: the human component adds value but is replaceable | Tech support with humans, consulting with a web panel |
| 0-20 | **No relevant human component**: the value is purely technical/functional | Databases, CLIs, compilers, pure hosting |

**Note on H erosion** (Yegge): H protection is not permanent. In the 40-60 band
(trust/oversight), protection erodes as social trust in AI grows. Trust-based H protects
temporarily but not indefinitely. Only H >= 70 (creativity, social interaction) has long-term
protection because it depends on people SPECIFICALLY valuing that humans are involved.

### H boost by category

| H | Boost | Meaning |
|---|-------|---------|
| 80-100 | +2 categories | Strong protection. Survives even if the base ratio is low. |
| 60-79 | +1.5 categories | Significant protection. |
| 40-59 | +1 category | Moderate protection. Helps but does not save on its own. |
| 20-39 | +0.5 categories | Slight protection. Minor factor. |
| 0-19 | No boost | The software lives or dies by its efficiency. |

(+0.5 categories = on the edge, mention that H helps but does not change the forecast)

## Interpreting the Base Ratio

| Base Ratio | Forecast | Description |
|------------|----------|-------------|
| >50 | 🟢 Indestructible | Absurd to re-synthesize. Fundamental tool. |
| 25-50 | 🟢 Very safe | High insight density. Agents clearly prefer it. |
| 10-25 | 🟢 Safe | Good position. Saves real cognition. |
| 5-10 | 🟡 Viable | Survives but must adapt or faces competition. |
| 2-5 | 🟠 At risk | Significant pressure. Agents can manage without it. |
| 0.5-2 | 🔴 Threatened | High probability of disruption. Little cognitive savings. |
| <0.5 | 🔴 Critical | Agents already do this better/cheaper. |

**Note**: Apply the H boost afterwards to obtain the final forecast. Example: Figma has a
base ratio of ~5.5 (🟠 At risk) but H=75 gives it +1.5 categories → 🟡 Viable/Protected.

## Relative Competition (Step 7b)

Yegge explains that the survival threshold is NOT fixed: **it rises when there is competition.**
A ratio of 1.2 can die if a competitor has 2.5. In crowded domains, the awareness cost rises
because agents have many options and the mediocre ones get lost in the noise.

After computing the ratio, identify:

1. **Direct competitors** that solve the same problem for agents
2. **The estimated ratio of the strongest competitor** (no full analysis needed, a reasoned
   estimate suffices)
3. **The relationship**: if your ratio is <50% of the strongest competitor, high risk of being ignored

Example: In accounting for Spanish SMBs, if a QuickBooks with Spanish compliance had a ratio
of ~8 and Holded has ~2, the competitive window closes.

In domains with little competition (DNA sequencing, as Yegge mentions), even a modest ratio
can be enough. In crowded domains, you need to stand out.

## The 6 Survival Levers (Yegge)

The levers are the concrete strategies to improve each variable:

| # | Lever | Variable it improves | Example | Key question |
|---|-------|----------------------|---------|--------------|
| 1 | **Knowledge compression** | → Savings | Git, PostgreSQL, Temporal | Does it crystallize insights that would be expensive to rediscover? How many decades of trial-and-error does it compress? |
| 2 | **Substrate efficiency** | → Savings | grep, ImageMagick, calculators | Does it do on CPU what would be expensive to do on GPU/inference? |
| 3 | **Broad utility** | → Usage | SQL, Temporal, Docker | Does it apply to many different contexts? |
| 4 | **Publicity/Awareness** | lowers Knowledge_cost | Everything in the training data | Do agents know it exists? |
| 5 | **Low friction / Desire paths** | lowers Friction_cost | Beads CLI, Stripe API | Does the tool work the way the agent expects it to work? |
| 6 | **Human coefficient** | → H | Slack, Figma, multiplayer games | Does the value depend on involving humans? |

### Desire Paths: expanded section (Lever 5)

"Desire paths" are Yegge's most original and actionable contribution. The idea:

> Observe what agents try to do with your tool, even (especially) when they fail. Each failed
> attempt is a "hallucination" telling you what the agent EXPECTS your tool to do. Implement
> that functionality.

Yegge describes how he did this with Beads: he observed the agents' attempts, implemented each
"hallucination" as real functionality, until almost every attempt was correct. Result: 100+
subcommands, aliases, and alternative syntaxes that HUMANS would never ask for but that agents
use naturally.

**Questions to evaluate desire paths**:
- Are you monitoring failed agent attempts against your API?
- Does your CLI/API have aliases and alternative syntaxes for the patterns agents try?
- Are your error messages informative for agents (not just for humans)?
- Can an agent that has never seen your documentation guess how to use you?

**Impact**: Desire paths can lower Friction_cost from 40-50 to 10-15, which typically
doubles or triples the base ratio.

## Trajectory Indicator

Every analysis must include a direction indicator that captures whether the tool is
improving or worsening over time:

| Indicator | Meaning | Typical signals |
|-----------|---------|-----------------|
| ↑↑ | Improving rapidly | Gaining awareness, agents discover and adopt it, virtuous training-data cycle |
| ↑ | Improving | Investing in API/agents, awareness growing gradually |
| → | Stable | No significant change in competitive position |
| ↓ | Worsening | Emerging competitors, functionality replicable by ever-better LLMs |
| ↓↓ | Worsening rapidly | Already losing users/traffic, AI alternatives clearly superior |

Trajectories are justified by:
- **Awareness cost**: is it dropping (more presence in training data) or rising (more competitors)?
- **LLM capabilities**: are models getting better at what your tool does?
- **Investment in agent UX**: is the tool building desire paths, MCP servers, evals?
- **Regulation**: do new laws create or destroy moats?

## Analysis Process

### Prior Phase (before Step 0): Adapted research

> Apply the **Activation rule** from the Prior Phase · Adapted research section: if there is
> no fresh information in context and the software justifies it, propose research adapted to
> the formula, execute it if the user accepts, and filter it by maturity
> (announced/shipped/adopted). The findings feed steps 4 (comparables), 7b (competition), the
> scoring of Fc/Kc, and the trajectory.

### Step 0 (BEFORE scoring): Calibration with comparables

> **MANDATORY**: Before assigning numerical scores, identify the 2-3 closest comparables in
> `references/known-cases.md` and use them as calibration anchors. Score RELATIVE to them,
> not in absolute terms.
>
> Example: If you are going to analyze a Spanish ERP, first look at Jira (Usage=65,
> Knowledge_cost=20), Zapier (Savings=45, Knowledge_cost=25) and the low-code tools
> (Savings=30, Usage=50). Your scores should be consistent with those anchors. If you give
> Usage=55 to a Spain-only product when Jira (global) has 65, something is wrong.

1. **Classify** the software according to the type taxonomy
2. **Absurdity Test** (Step 0a): Would it be absurd to re-synthesize it? + how many decades of trial-and-error does it compress?
3. **Intermediation Test** (Step 0b): Does it intermediate between humans and tasks the AI will do? If PARTIAL, estimate the % of value that intermediates.
4. **Identify comparables** in `references/known-cases.md`, use them as anchors BEFORE scoring
5. **Score** each variable using the scoring guides AND the calibration anchors
6. **Compute** the base ratio: `(Savings × Usage) / ((Kc + Fc) × 10)`
7. **Evaluate H** separately and determine the boost
7b. **Relative competition**: identify direct competitors and compare ratios
8. **Anti-bias checklist** (mandatory, see section below)
9. **Apply** the base forecast + H boost → final forecast
10. **Determine trajectory**: ↑↑ / ↑ / → / ↓ / ↓↓ with justification
11. **Compare** the final ratio with the comparables identified in step 4. If it differs >3x, review.
12. **Map** the 6 levers: which are active? which could be activated?
13. **Evaluate desire paths** specifically: does the tool have agent UX? does it monitor failed attempts?
14. **Estimate the time horizon** using Yegge's disruption timeline
15. **Recommend** concrete actions aligned with the levers

### Anti-Bias Checklist (Step 8, mandatory)

After scoring and BEFORE computing the final forecast, answer these questions to detect
common biases. If any answer is "yes", review the affected score.

| # | Question | If the answer is YES... | Affected variable |
|---|----------|-------------------------|-------------------|
| 1 | Am I scoring **Usage** based on the LOCAL market instead of the GLOBAL universe of agents? | Lower Usage by 15-25 points | Usage |
| 2 | Am I scoring **Knowledge_cost** based on popularity among HUMANS instead of presence in the TRAINING DATA of LLMs? | Raise Knowledge_cost by 15-25 points | Knowledge_cost |
| 3 | Is the absurdity test consistent with the ratio? (If I said "NOT absurd" but ratio >5, or "YES absurd" but ratio <10) | Review Savings or Usage | Savings, Usage |
| 4 | Am I confusing "product successful among humans" with "product an agent would CHOOSE"? | Review Savings | Savings |
| 5 | Is the product from a non-English-speaking market and I gave it Knowledge_cost < 30? | Raise Knowledge_cost | Knowledge_cost |
| 6 | Was I generous with Savings because the product "has many features"? (Many features != high cognitive savings) | Review Savings | Savings |
| 7 | Did I move a variable to an extreme because of something **just announced or in beta** (recency/marketing bias)? Or did I read as momentum an expansion that actually **raises intermediation**? | Reclassify the finding by maturity (announced/shipped/adopted) and reweight | Fc, Kc, Savings, trajectory |

**Yegge's golden rule for bias**: The question is NOT "is it a good product?" but
"would an agent stop to use it instead of doing it itself?" (Yegge: "Build something that
would be crazy to re-synthesize. Make it easy to find. Make it easy to use.")

## Output Format

```markdown
## Survival Analysis: [Tool]

**What it does**: [brief description]
**Type**: [per taxonomy]

### Research / Sources
- **Research performed**: YES/NO (if NO: reason — info already in context / stable infra / no public info)
- **Information date**: [date of the research or sources used]
- **Key findings by maturity**: [announced / shipped-beta / shipped-adopted] that affect the scoring
- **Variables moved by the research**: [e.g. Fc, competition, trajectory]

### Binary Tests

| Test | Result | Justification |
|------|--------|---------------|
| Absurdity | YES/NO/DEPENDS | [1-2 sentences + decades of compressed trial-and-error] |
| Intermediation | YES/NO/PARTIAL (X%) | [1-2 sentences: which "smart things" does it do that the AI will do? If PARTIAL, % of value that intermediates] |

### Calibration Anchors
- Comparable 1: [tool] (Savings=X, Usage=X, Kc=X, Fc=X, ratio=X)
- Comparable 2: [tool] (Savings=X, Usage=X, Kc=X, Fc=X, ratio=X)

### Scoring

> If the software already has an entry in `known-cases.md`, use **two columns**: "Baseline (entry)"
> and "Updated (research)", indicating what changes and why. Otherwise, a single column.

| Variable | Value | Justification (with reference to anchors) |
|----------|-------|-------------------------------------------|
| Savings | X/100 | [type: algorithmic/regulatory/integrations/UX] ... |
| Usage | X/100 | [geographic scope considered] ... |
| Knowledge_cost | X/100 | [presence in training data, not human popularity] ... |
| Friction_cost | X/100 | ... |
| H | X/100 | ... |

### Anti-Bias Checklist
- [ ] Usage based on the global perspective of agents, not the local market
- [ ] Knowledge_cost based on presence in training data, not human popularity
- [ ] Absurdity test consistent with the ratio
- [ ] I am not confusing "good product" with "product an agent would choose"
- [ ] If a non-English-speaking market, Knowledge_cost adjusted upward
- [ ] Savings measures cognition saved, not number of features
- [ ] No variable moved to an extreme by recency/marketing bias (findings filtered by maturity)

**Base ratio**: X.X
**Base category**: 🟢/🟡/🟠/🔴 [Category]
**H boost**: +X categories (justification)
**Final forecast**: 🟢/🟡/🟠/🔴 [Category]
**Trajectory**: ↑↑/↑/→/↓/↓↓ [justification]

### Relative Competition

| Competitor | Estimated ratio | Advantage/disadvantage |
|-----------|-----------------|------------------------|
| ... | ~X.X | ... |

### Yegge's Levers

| # | Lever | Status | Comment |
|---|-------|--------|---------|
| 1 | Knowledge compression | 🟢/🟡/🔴 | ... |
| 2 | Substrate efficiency | 🟢/🟡/🔴 | ... |
| 3 | Broad utility | 🟢/🟡/🔴 | ... |
| 4 | Publicity/Awareness | 🟢/🟡/🔴 | ... |
| 5 | Low friction / Desire paths | 🟢/🟡/🔴 | ... |
| 6 | Human coefficient | 🟢/🟡/🔴 | ... |

### Desire Paths (specific evaluation)

- Does it have a complete API? [YES/NO/PARTIAL]
- Does it monitor failed agent attempts? [YES/NO/UNKNOWN]
- Does it have aliases/alternative syntaxes for agents? [YES/NO]
- Are error messages informative for agents? [YES/NO]
- Could an agent without docs guess how to use it? [YES/NO]

### Comparables
- Similar to [known tool] (base ratio ~X, H=Y)
- [Check: ratio differs <3x from comparable → OK / ratio differs >3x → REVIEW]

### Time Horizon
- **No changes**: X-Y years (based on Yegge's timeline: completions → chat → agents → orchestration)
- **With an agent-first strategy**: X-Y years

### Conclusion
[Paragraph with qualitative analysis in Yegge's spirit: would the agent pass it by?
would it stop to use it? would it actively seek it out? Include concrete recommendations
aligned with the 6 levers.]
```

## Calibration Notes

### How the formula was calibrated

The v1 formula `(S × U × H_adj) / (Kc + Fc)` produced ratios 10x to 100x off relative to the
published benchmarks, with no consistent scale factor. This was due to:

1. Multiplicative H massively inflated tools with high H (Slack gave more than Docker)
2. The numerator's range (0 to 1,000,000) was disproportionate to the denominator (2 to 200)
3. The original benchmarks were assigned intuitively, not computed with the formula

The v2 formula corrects this:
- Separates H as an independent force (faithful to Yegge: "different selection pressure entirely")
- Normalizes with ×10 in the denominator to produce manageable ratios (0-100+)
- All benchmarks in `references/known-cases.md` were RECOMPUTED with the formula
  and are mathematically verifiable

### Changes in v3 (relative to v2)

1. **Intermediation Test** (Step 0b): New mandatory binary test based on the direct
   Yegge quote about software that intermediates.
2. **Relative Competition** (Step 7b): The survival threshold rises with competition.
3. **Trajectory Indicator**: ↑↑/↑/→/↓/↓↓ to capture whether the tool is improving or worsening.
4. **Expanded Desire Paths**: Specific section with evaluation questions for agent UX.
5. **Decades of trial-and-error**: Savings calibration based on crystallized cognition
   (Yegge concept via Brendan Hopper).
6. **Time horizon**: Explicit estimate using Yegge's disruption timeline.
7. **H erosion**: Note on how trust/oversight H (40-60) erodes over time, unlike social
   interaction H (80+).

### Changes in v4 (relative to v3)

Changes derived from real errors made in analyses (the Holded case) and validated against
Yegge's original article (Software Survival 3.0, January 2026).

1. **Geographic scope penalty in Usage**: Agents operate globally; regional software has
   restricted utility. Adjustment table added to the Usage guide.
   *Yegge validation*: "Aim to build software that lots of agents prefer to use in lots of
   situations" (p.11) — "lots of situations" implies global, not local, scope.

2. **Note on language bias in Knowledge_cost**: LLM training data is predominantly English.
   Software popular in non-English-speaking markets has Knowledge_cost 15-25 points higher
   than expected.
   *Yegge validation*: "the energy to get it into their training sets" (p.5) — training sets
   have inherent language bias.

3. **Table of savings types** (algorithmic vs. regulatory vs. integrations vs. UX): Distinguishes
   between genuine "insight density" and other types of less defensible accumulated value.
   *Yegge validation*: "sheer insight density" (p.8) and "crystallized cognition" (p.8) always
   refer to deep engineering knowledge, not regulatory compliance.

4. **Quantification of PARTIAL intermediation**: When test 0b is PARTIAL, estimate the % of
   value that intermediates and use thresholds (>60% → treat as YES, <40% → moderate).
   *Yegge validation*: "any software that's intermediating..." (p.15) is a strong formulation
   that justifies treating PARTIAL >60% as YES.

5. **Mandatory anti-bias checklist** (Step 8): 6 questions to detect common biases before
   issuing the final forecast. Prevents the most frequent errors.
   *Yegge validation*: The distinction of H as "different selection pressure entirely" (p.14)
   is key — confusing "popular" with "efficient for agents" is bias #1.

6. **Comparables BEFORE scoring** (Step 0, before step 5): Identify calibration anchors before
   assigning numerical scores to avoid scoring in absolute terms.
   *Yegge validation*: "Your software's survivability threshold floats above 1 when there's
   competition" (p.6) — without a comparative reference, the scores float.

### Changes in v5 (relative to v4)

Changes derived from a real analysis (the Figma case, June 2026) in which the baseline's
frozen knowledge had fallen out of date relative to the product's actual state.

1. **Prior Phase of adapted research** (before Step 0): a proposed and skippable step, not a
   mandatory gate. Includes an activation rule (do not propose if there is fresh info in
   context, or if it's stable infrastructure / a tool with no public info), a brief tied to
   the formula's variables (not generic), and a maturity filter. It sits before calibration
   because research can reveal a new competitor that then becomes an anchor.
   *Yegge validation*: the 2023→2026 timeline assumes annual change; scoring from frozen
   knowledge contradicts the model's own premise.

2. **Announced ≠ shipped ≠ adopted filter**: research improves the analysis asymmetrically
   (it hits Fc/desire paths, competition and trajectory; barely touches Savings/Usage) and
   introduces recency/marketing bias if not filtered by maturity. A beta feature does not
   move a variable to the extreme; a product expansion can worsen the profile by raising
   intermediation.

3. **Anti-bias question 7** (Step 8): detects recency/marketing bias and the "momentum" mirage
   that actually raises test 0b.

4. **Baseline vs. updated pattern**: when the software already has an entry in
   `known-cases.md`, the baseline is not overwritten; two scenarios are presented side by
   side and the research can **propose updating the entry** (with a calibration date). The
   output format adds a "Research / Sources" section and dual-column support in Scoring.

### Verification: how to know if your score is reasonable

1. Compute the ratio with the formula
2. Find the closest comparable in `references/known-cases.md`
3. If your ratio differs >3x from the most similar comparable, review your scores
4. The absurdity test must be consistent with the ratio: if you said "YES absurd" but the
   ratio comes out <10, something is wrong in the scoring
5. The intermediation test must be consistent: if you said "YES it intermediates" but the
   ratio comes out >10, check whether it is really intermediating or has other value
6. **New (v4)**: Run the anti-bias checklist BEFORE giving the final forecast

## Reference Cases

See `references/known-cases.md` for benchmarks and comparisons.
All ratios have been recomputed with the v2 formula and are verifiable.
