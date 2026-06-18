# Survival Analysis: Salesforce

> Application of the **Software Survival Analyzer** (Steve Yegge's formula). A new case (no prior entry in `known-cases.md`), preceded by the Prior Research Phase because it's a large SaaS with active agentic offensive (Agentforce).
>
> **Note**: this analysis was originally produced against **v5** of the skill. Its central methodological finding — that Salesforce's dominant moat is **data gravity + switching costs**, a third force the Yegge formula under-models — is exactly what motivated **v5.1's Step 7c** (a qualitative forecast adjustment, parallel to 7b, with anti-double-counting rule and an honesty caveat that it is an extension beyond strict Yegge). Where this document calls the gap "a methodological caveat", read it as **Step 7c** in the current method.

**What it does**: The world's leading CRM platform. Customer management core (Sales, Service, Marketing, Commerce) plus a development platform (Apex, Flows, AppExchange), a data layer (Data 360), messaging (Slack), and since late 2024 an agentic layer (Agentforce) that deploys autonomous AI agents for service, sales, IT and back-office.

**Type (taxonomy)**: Hybrid. (1) *SaaS for humans* (the CRM, historical per-seat model), (2) *Platform/Marketplace* (AppExchange, AgentExchange, Data 360), and (3) *Tool for agents / Infrastructure* (an emerging and heavily invested layer: MCP, Headless 360, Agentforce as system of record and orchestrator). Salesforce explicitly repositions itself as the "operating system of the Agentic Enterprise."

---

## Research / Sources

- **Research performed**: YES. Justified: large SaaS, live competition, AI offensive in progress; no prior fresh info in context.
- **Information date**: June 2026 (Q4 FY26 results from Feb 2026, TDX/Summer '26 launches Apr-Jun 2026).
- **Key findings by maturity**:
  - *Shipped and adopted*: Agentforce GA (29K deals, ARR $800M +169% YoY, 2.4B agentic work units, ~20T tokens); Hosted MCP Servers GA (Enterprise+); Slack as orchestration layer (1B msgs/day).
  - *Shipped but beta/preview*: Salesforce DX MCP (Beta), Data 360 MCP (Developer Preview), Agentforce as MCP client (Beta Jan 2026), Agentforce Operations (ecosystem features Beta May 2026), Headless 360 (rollout May-Jun 2026).
  - *Announced*: Agent Albert (agentic platform, expected before end of 2026, not yet shipped).
  - *Reality check*: Agentforce ~58% accuracy on simple tasks (per critical sources citing Salesforce data); strong dependency on data quality; complaints of inaccuracy (incl. mandatory Agentforce in the Help). Maturity filter applied: these limits prevent scoring the agentic layer as mature.
- **Variables moved by the research**: Fc (investment in MCP/Headless 360 lowers friction from a historically high level, but underlying complexity and immaturity keep it moderate), competition (Microsoft on the agent layer, Databricks on the data layer), trajectory (bifurcated).

---

## Binary Tests

| Test | Result | Justification |
|------|--------|---------------|
| **Absurdity** | **DEPENDS** | Re-synthesizing the CRM *application* (objects, workflows, a record base) would **not** be absurd: the CRM is not algorithmic insight density like PostgreSQL or Git; an agent could build a basic CRM. What IS irreplicable is the *system of record*: the customer's proprietary data accumulated over years, their specific configuration, integrations, and the ecosystem. But note: that moat is one of **data + integration + inertia**, not "crystallized engineering cognition". In Yegge's strict terms (engineering insight density), the test is NO/weak; Salesforce's real moat is of another kind and is captured via H and Savings-integrations, not via a high ratio. Decades of engineering trial-and-error compressed: few. Decades of customer data/integration accumulated: many, but that is not what the absurdity test measures. |
| **Intermediation** | **PARTIAL (~50%, gray zone)** | Much of the per-seat value is "a human doing cognitive work in an interface" (data entry, record updates, reports, forecasting, service-case responses) — exactly what agents now do natively. That is intermediation-exposed and a large fraction of what's paid per seat. They do NOT intermediate: custody and governance of the canonical data, compliance, security, transactional-backbone role. Estimated ~50% of value in the intermediating part, in the 40-60% gray zone (reflected downward in Savings). It is **higher** than Figma's (~40%) because CRM admin work is more directly automatable than design taste. Critical nuance: Agentforce itself **is** Salesforce automating that intermediated work; the bet is to recapture it as consumption revenue rather than lose it. |

**Combined read**: Salesforce does not pass the absurdity test (its moat is not algorithmic) and intermediates ~50%. Per the method's rule, software like this rarely beats 🟠 At risk **via the ratio route**. Its survival depends almost entirely on forces the formula captures poorly: data gravity, switching costs, and the human coefficient. This is expanded below and is the central finding of the analysis.

---

## Calibration Anchors (before scoring)

| Anchor | Savings | Usage | Kc | Fc | H | Ratio | Why it's relevant |
|--------|---------|-------|----|----|---|-------|-------------------|
| **Jira** | 35 | 65 | 20 | 40 | 50 | 3.8 | **The closest analogue**: enterprise SaaS, lock-in on organizational data/processes, partial intermediation (~50%), coordination H, complex API (anti-desire-paths). The calibration floor. |
| **Slack** | 30 | 75 | 10 | 15 | 85 | 9.0 | Salesforce **owns** Slack and uses it as orchestration layer for agents and human engagement. Injects a slice of durable social H into the portfolio. |
| **Stripe** | 90 | 80 | 10 | 10 | 25 | 36.0 | The aspirational ceiling: "become infrastructure for agents via a clean API". Headless 360 / MCP pursue that for CRM data, but Salesforce lacks the algorithmic density (fraud, routing) that justifies Stripe's 90. |
| **Zapier** | 45 | 60 | 25 | 45 | 10 | 3.9 | Warning case: textbook intermediation with a visual interface. The per-seat portion of Salesforce shares that risk. |
| **Notion** | 40 | 70 | 15 | 15 | 60 | 9.3 | SaaS for humans protected by H; reference for "workspace" with less intermediation exposure than the CRM. |

Calibration question: Salesforce resembles **Jira** at its core (enterprise SaaS, lock-in, intermediation ~50%), but is playing to become **Stripe** (data infrastructure for agents via Headless 360/MCP) while leaning on **Slack** (orchestration). Scores should land above Jira (more data / system-of-record role, lower Kc) but far from Stripe (no algorithmic insight density).

---

## Scoring

| Variable | Value | Justification (with reference to anchors) |
|----------|-------|--------------------------------------------|
| **Savings** | 45 | Type **integrations + institutional/governance + data custody (system of record)**, NOT algorithmic. An agent operating inside a Salesforce-running company saves real cognition by having a canonical, governed customer data with an API (MCP/Headless 360) instead of assembling it from scratch. But that is data/integration savings, not crystallized engineering. Above Jira (35) because of the system-of-record role and governance; well below Stripe (90) for lack of algorithmic density. **Q7 filter**: not inflated by Agentforce, which is Salesforce *doing* the work, not a moat that saves cognition for an external agent. |
| **Usage** | 65 | Global, ubiquitous in enterprise (150K customers, #1 CRM), broad in customer-facing functions. But it's a broad niche (CRM/customer-facing), not universal like SQL/Git: an agent only picks it if the company already runs on Salesforce. Same level as Jira (65). No geographic penalty. |
| **Knowledge_cost (Kc)** | 18 | Massive presence in training data (Trailhead, huge community, docs), English/global, now with official MCP/Headless 360 docs. Any LLM knows the Salesforce model. Slightly below Jira (20). Nuance: *general* knowledge is high (low Kc), but each org's *specific config* isn't in training data and requires runtime grounding — exactly what MCP provides. |
| **Friction_cost (Fc)** | 35 | **The change the research contributes.** Historically high (complex APIs, governor limits, metadata, per-org config: anti-desire-paths, worse than Jira). But aggressive and recent investment in agent-facing surface: Hosted MCP GA, Headless 360 ("all capability as API/MCP/CLI"), Data 360 MCP, AgentExchange, MCP/A2A founding member. Down from a historical ~40 toward 35. **Q7 filter**: does not fall to Stripe's level (10) because the underlying complexity remains (Salesforce's own Data 360 MCP blog admits its API surface "saturates the LLM context") and the MCP layer is new (partly Beta/Preview) with Agentforce at ~58% accuracy. |

### Base ratio calculation

```
Base_ratio = (Savings × Usage) / ((Kc + Fc) × 10)
           = (45 × 65) / ((18 + 35) × 10)
           = 2925 / 530
           = 5.5
```

**Base ratio ≈ 5.5 → 🟡 Viable** (5-10 band, low end). Above Jira (3.8) because of the system-of-record role and lower Kc; well below Stripe (36) for the absence of algorithmic density.

---

## Human Coefficient (H) decomposition

As with the Figma case, Salesforce's H has components with very different half-lives, and here in addition a moat appears that Yegge's formula captures poorly:

| Component | Approx. value | Type (band) | Durability |
|-----------|:---:|-------------|------------|
| **Governance / trust / oversight** (a human must answer for the customer data, approve agent actions, guarantee compliance and audit, especially in regulated sectors) | ~57 | Trust/oversight (40-60) | **Erodable.** The method warns that this band erodes as social trust in AI grows. |
| **Organizational lock-in / switching costs / "career risk"** (deeply embedded implementations, expensive to replace, "the safe choice") | ~50 (inertia) | Functions like Jira's coordination H | **Inertia, not human preference.** Here is the mapping trap: this is **data gravity**, not "humans being valued". Yegge captures it only partially. |
| **Social via Slack** (Salesforce owns Slack, 1B msgs/day, human engagement layer and orchestrator of agents) | ~85 | Social interaction (80-100) | **Durable.** A genuinely solid slice, social-infra type. |
| **Creativity / taste** | low | n/a | The CRM isn't valued because "a human made it". |

**Effective H ≈ 58** (boost +1 category, 40-59 band). The bifurcation matters: most of the CRM's H is of the **erodable** type (governance) or **inertia** (lock-in), with a *durable slice* contributed by Slack.

> **Method caveat (key for this case)** — *formalized as **Step 7c** in v5.1*: Salesforce's largest real moat (data gravity + switching costs + organizational inertia) **does not fit cleanly** into Yegge's two original forces, which measure cognitive efficiency for agents (Savings) and human preference (H). It is neither: it's data gravity and inertia. The formula therefore **underestimates** Salesforce's short-term survival. v5.1 captures this as a qualitative forecast adjustment parallel to 7b (modulates the threshold, not the ratio nor a new variable), with an explicit anti-double-counting rule and an erosion note (open standards like MCP make the data portable, eroding the very moat). It's reflected in the final forecast, not by forcing the variables.

---

## Anti-Bias Checklist (Step 8, v5)

| # | Question | Answer | Action |
|---|----------|--------|--------|
| 1 | Usage local vs. global universe? | Global, not inflated. | ✓ |
| 2 | Kc by human popularity vs. training data? | Kc is low because Salesforce is **genuinely** in training data (Trailhead, community, official docs). | ✓ |
| 3 | Absurdity consistent with the ratio? | DEPENDS (weak via engineering) ↔ ratio 5.5. Consistent: the non-absurd application layer keeps the ratio modest; the data moat is captured via H + Savings-integrations, not via a high ratio. | ✓ |
| 4 | Am I confusing "successful product" with "product an agent would choose"? | **Critical check.** Salesforce is a huge success, but the agent's choice is conditional on incumbency: an agent uses it because the company's data **already lives there** (data gravity), not because it's the most efficient tool. Scored against agent-choice-given-incumbency and flagged the data-gravity moat as under-modeled. Did NOT inflate Savings on account of Agentforce's success. | ✓ |
| 5 | Non-English with Kc<30? | No, global/English. | ✓ |
| 6 | Generous with Savings because "many features"? | Salesforce has an enormous feature surface (Sales/Service/Marketing/Commerce/Data/Slack/Tableau/MuleSoft/Agentforce), but Savings was kept at 45. Many features ≠ high cognitive savings; an agent can replicate individual modules. | ✓ |
| 7 | **(v5)** Variable moved to extreme by something announced/beta? Expansion read as momentum when it actually raises intermediation? | **Very relevant here.** Agentforce / Agent Albert / Setup-with-Agentforce / Vibes are heavily marketed; part is GA but with ~58% accuracy and data dependency, and part is Beta/Preview (DX MCP, Data 360 MCP, Agentforce Operations) or unshipped (Agent Albert). Filter applied: Hosted MCP GA with full weight, Beta/Preview discounted, Agent Albert ignored in scoring. In addition, the agentic expansion was NOT treated as an automatic moat: much of it is Salesforce automating the per-seat work that threatens its own model (intermediation), a recapture bet, not a moat. Kept Fc at 35 (not lower) because of immaturity. | ✓ |

**Checklist finding**: Salesforce's agentic offensive is, in part, intermediation of itself. Agentforce automates the per-seat work; the commercial success (ARR +169%) is real but does not strengthen the Yegge moat — it **shifts** revenue from the seat (high margin) to consumption (lower margin). The Q7 filter prevents reading that as a rise in survival.

---

## Forecast

| | Value |
|---|---|
| **Base ratio** | 5.5 |
| **Base category** | 🟡 Viable (low end) |
| **H boost** | +1 (H=58) |
| **Mechanical forecast** | 🟢 Safe |
| **Adjusted forecast** | 🟡→🟢 **bifurcated** (see below) |
| **Trajectory** | → Bifurcating |

The arithmetic gives 🟢 Safe (5.5 + boost +1). But the honest forecast **splits in two layers**, and the data-gravity caveat pushes *platform* survival further above what the ratio says:

- **System-of-record / data / platform / orchestration layer (Agentforce + Data 360 + Slack)**: 🟢 **Safe / durable**. Agents need the governed customer data; switching costs are enormous; Salesforce provides the surface (MCP/Headless 360) through which agents enter and exit. The formula underestimates this because of the data-gravity caveat.
- **Per-seat revenue from the CRM application ("a human doing CRM cognitive work in a UI")**: 🟠 **At risk**. ~50% intermediation, seat compression. Agentforce itself automates exactly this.

The entire Salesforce strategy is to **recapture** the threatened layer as consumption / orchestration revenue (Agentforce, Flex Credits, hybrid pricing, Headless 360). Bullish math: Agentforce at 10-20% the cost of a human could multiply per-seat revenue 2-4x on replaced seats **if** adoption and accuracy scale. Bearish risk: if agents route around the Salesforce UI and go straight to its data via generic MCP (which Salesforce itself enables), value migrates from high-margin seats to lower-margin consumption, and competitors erode share.

**Why trajectory → bifurcating**: bullish vector on the orchestration layer (aggressive MCP/Headless 360 investment, Agentforce ARR +169%, RPO +14%, owns Slack, MCP/A2A founding member); bearish vector on the per-seat layer (SaaSpocalypse, stock -30% in 2026, Agentforce at ~58% accuracy, mature ~10% growth). Net approximately neutral and contested.

---

## Relative Competition (Step 7b)

The survival threshold rises with competition, and Salesforce is attacked on **two distinct fronts**:

| Competitor | Layer it attacks | Read |
|-----------|------------------|------|
| **Microsoft** (Dynamics 365 + Copilot + Copilot Studio) | The **agent / orchestration layer** | The biggest threat: distribution via M365, agents integrated where work actually happens. Can disintermediate the CRM UI from the productivity layer. |
| **Databricks CustomerLake / agentic CDPs** | The **data layer** (Salesforce's emerging moat) | Attacks data orchestration: "Data Cloud is still an adjunct to the CRM, not a natively governed data lake". Threatens the moat Salesforce is trying to build. |
| **ServiceNow** | Adjacent enterprise workflow | Mutual: pushes agents; Salesforce counter-attacks its ITSM turf with Agentforce IT Service (180 orgs in 4 months). |
| **"Agent OS" layer / AI-native startups** | Bain's three-layer model | "One agent per outcome" replaces point solutions. Systemic pressure on all per-seat SaaS. |

**Competitive insight**: Salesforce is attacked on data (Databricks) and on agents (Microsoft) simultaneously. Its defense is owning the system of record + Slack + Agentforce + Data 360, while also playing offense (ITSM, life sciences). The competitive threshold is high, but incumbency and data gravity are a strong defense that no entrant replicates easily.

---

## Yegge's 6 levers

| # | Lever | Status | Comment |
|---|-------|:---:|---------|
| 1 | Knowledge compression | 🔴/🟡 | Weak. The CRM is not algorithmic insight density. The "savings" is data/integrations/governance, not crystallized engineering cognition. Not Git/PostgreSQL. |
| 2 | Substrate efficiency | 🔴 | None. Salesforce **consumes** inference (20T tokens); does no cheap compute an agent would want to avoid. |
| 3 | Broad utility | 🟢 | Strong. Ubiquitous in enterprise, global, broad in customer-facing functions. |
| 4 | Awareness | 🟢 | Strong. Massive presence in training data (Trailhead), official MCP docs. |
| 5 | Low friction / Desire paths | 🟡 | **Improving — the key story.** Historically 🔴 (complex APIs). Now aggressive push: Hosted MCP GA, Headless 360, AgentExchange. Half-mature and underlying complexity high. |
| 6 | Human coefficient | 🟡 | Moderate and bifurcating. Governance (erodable) + lock-in (inertia, under-modeled by Yegge) + Slack's durable slice. |

**Third force (now formalized as Step 7c in v5.1)**: **data gravity + switching costs**. Salesforce's largest real defense, which the formula's two original forces capture only in part (via Savings-integrations and H-oversight). The remaining pure inertia — the data is already here and migrating is expensive — is what Step 7c absorbs as a qualitative forecast adjustment, with the anti-double-counting rule applied.

---

## Desire Paths (specific evaluation)

| Question | Answer | Detail |
|----------|--------|--------|
| Full API? | **YES, and increasingly agent-first** | REST/SOAP/Bulk/Metadata (mature but complex) + Hosted MCP (GA Enterprise+) + Headless 360 (all capability as API/MCP/CLI) + Data 360 MCP (Preview) + AgentExchange. Extensive surface, declared priority. |
| Monitors failed agent attempts? | **Emerging** | Agentforce has eval tooling, "Answer Quality" metrics, and Plan Canvas testing. Instruments *its* Agentforce behavior more than that of external agents. |
| Aliases / alternative syntaxes? | **Via MCP + AgentExchange** | Structured tool exposure, but limited by the complexity of the underlying object model. |
| Error messages informative? | **Mixed** | Salesforce errors (governor limits) are historically cryptic; the MCP layer abstracts part. |
| Could an agent without docs guess? | **Raw Salesforce: no. MCP/Headless layer: increasingly yes** | Per-org complexity prevents it raw; the MCP layer uses a standard protocol and discoverable tools. |

**Verdict**: historically high friction, today aggressive investment in agent UX. The surface is real (Hosted MCP GA), but the underlying complexity and the layer's novelty (partly Beta/Preview, Agentforce at ~58%) keep friction moderate. It is the area of highest potential ROI for Salesforce per Yegge.

---

## Comparable verification

- vs **Jira** (3.8, closest analogue): 5.5/3.8 = **1.45×** → OK. Salesforce above, consistent (more data / system of record, lower Kc, Fc somewhat lower because of the MCP investment).
- vs **Slack** (9.0): 0.61× → OK (Slack with lower Fc and more H).
- vs **Stripe** (36): 0.15× → OK and deliberate (Salesforce lacks Stripe's algorithmic density).
- Differs <3× from the closest comparable. **Scoring consistent.** ✓

---

## Time horizon

Yegge's timeline: 2026 = orchestration / multi-agent (~3-4 years). Salesforce is trying to **be** that layer (Agentforce + Slack + MCP/A2A), not be bypassed by it.

- **No changes** (if Salesforce stood still): per-seat CRM revenue at risk in ~3-5 years (seat compression as agents take over the work); the data / system-of-record layer durable for much longer.
- **With an agent-first strategy** (which it is aggressively executing): the pivot to orchestration / system of record + consumption pricing can extend durability well beyond 5 years, and potentially **grow** (the "OS of the Agentic Enterprise" thesis, AI-upsell offsetting seat losses). Conditional on Agentforce accuracy improving from the current ~58%.

---

## Conclusion

Would the agent pass it by, stop to use it, or actively seek it out? Depends on the layer — and that is the profile of a **bifurcated** case where Yegge's formula **underestimates** real survival because it doesn't model data gravity well:

- An agent building any arbitrary app **passes by**: the CRM is not insight density it would be absurd to re-synthesize.
- An agent operating **inside a company already running on Salesforce** stops to use it, not because it's the most efficient choice but because **the customer data lives there** (data gravity) and is governed, with an MCP surface for entering and exiting.
- And Salesforce works aggressively to make agents **actively seek it out** as the orchestration layer (Agentforce + Slack + Headless 360).

Salesforce is **more resilient than its ratio suggests** (5.5) and than its stock price suggests (-30% in 2026), because its dominant moat (data gravity + switching costs + incumbency) falls outside what the formula measures well. But its **per-seat revenue model genuinely is threatened**: the ~50% intermediation and seat compression are real, and Agentforce itself automates that work. Survival *as a relevant platform* is highly likely; preservation of the *high-margin per-seat model* is not guaranteed and is being converted to consumption in real time.

**Lever-aligned recommendations:**

1. **Lever 5 (desire paths) is the right bet: mature, don't just announce.** Move Hosted MCP and Headless 360 from "broad but complex" to a reliable de facto standard; instrument the failed attempts of external agents (not just Agentforce) and implement them. It's where Yegge sees the most ROI and where Salesforce can actually move Fc. The bottleneck is not announcing surface, it is complexity and accuracy.
2. **Raise Agentforce accuracy from ~58%.** While the agentic layer is not reliable, the recapture thesis (consumption offsetting seats) is fragile and feeds skepticism. Customer-data quality is the declared limiting factor: turn "data readiness" into product.
3. **Defend the data layer against Databricks.** The emerging moat (Data 360 as the system of record for customer data for agents) is exactly what the agentic CDP attacks. Embed Data 360 as a natively governed lake, not a CRM adjunct.
4. **Leverage Slack as the durable H slice.** It is the piece with long-term protection (social, ~85) and the natural orchestration layer between humans and agents. The H asset that doesn't erode.

**Leading indicators to monitor** (thresholds that would change the forecast):
- *Seat vs. consumption mix*: revenue migration from per-seat to Agentforce/Flex Credits is the master metric. If consumption grows and net seats fall, recapture works (or doesn't).
- *Agentforce accuracy / adoption*: moving past ~58% toward production reliability validates the thesis; stalling invalidates it.
- *cRPO and high-value deals* (>$1M +26%, >$10M +33% in Q4 FY26): if they hold, incumbency endures; if they degrade, real erosion is showing.
- *Headless 360 / MCP adoption by external agents*: confirms or denies the pivot to agent-data infrastructure.
- *Market share vs. Microsoft (agent layer) and Databricks (data layer)*: the two fronts where the case is decided.

---

## Caveats

- **Salesforce's dominant moat (data gravity + switching costs) is under-modeled by Yegge's two original forces** (cognitive efficiency in the ratio and human preference in H). v5.1 of the skill formalizes this as **Step 7c**: a qualitative forecast adjustment, parallel to 7b, with an anti-double-counting rule (the cognitive savings from canonical data go in Savings, the human governance goes in H, the *pure inertia* goes in 7c without being duplicated) and an erosion note (the moat erodes as open standards make the data portable to agents). The literal 5.5 ratio underestimates platform survival in the short term, which Step 7c absorbs in the adjusted forecast.
- **Point-in-time and volatile numbers**: stock -30% in 2026, Q4 FY26 results (Feb 2026). Agent Albert is announced aspiration, not product.
- **Source bias in the maturity check**: the ~58% accuracy figure and metrics like "77% of B2B implementations fail" come from critical sources or competitors (oliv.ai); treat as directional, not definitive. Financial metrics are corroborated (official release, transcript, multiple outlets).
- **Double-edged agentic bet**: Agentforce working commercially (ARR +169%) does not equal a strengthened survival moat; it may accelerate the migration from high-margin seats to lower-margin consumption. The Q7 filter prevents confusing the two.
- Analysis based on information available as of June 2026.

---

### Summary card (for `known-cases.md`)

```
### Salesforce
- Type: SaaS for humans + Platform/Marketplace + Tool for agents (emerging)
- Absurdity: DEPENDS (weak via engineering). Non-absurd CRM app; real moat is data/integration, not algorithmic.
- Intermediation: PARTIAL (~50%, gray zone). Per-seat work intermediates; system of record / governance does not. Agentforce automates the intermediated part (recapture bet).
- Savings type: Integrations + institutional/governance + data custody. NOT algorithmic.
- Geographic scope: Global · No adjustment to Usage
- Savings: 45 · Usage: 65 · Kc: 18 · Fc: 35 · H: 58
- Base ratio: (45×65) / (53×10) = 5.5
- H decomposed: governance ~57 (erodable) + lock-in ~50 (inertia) + Slack social ~85 (durable). Effective ~58.
- H boost: +1 category (H=58)
- Trajectory: → Bifurcating (orchestration/data ↑ via MCP/Headless 360/Agentforce ARR +169%; per-seat ↓ via SaaSpocalypse, stock -30% 2026, Agentforce ~58% accuracy)
- Desire Paths: Historically high (complex APIs, Fc~40). Improving with Hosted MCP GA, Headless 360, AgentExchange. Half-mature (partly Beta/Preview).
- Levers: Broad utility ★, Awareness ★, Desire paths (under construction) ★
- Key caveat: data gravity + switching costs UNDER-MODELED by the formula; underestimates platform survival in the short term.
- Horizon: 3-5 years per-seat revenue; >5 years (or growing) for the platform/data layer if the pivot executes.
- Competition: Microsoft (agent layer), Databricks (data layer), ServiceNow (workflow).
- Forecast: 🟡 Viable → 🟢 Protected (platform/data), with per-seat revenue 🟠 At risk. Calibration: June 2026.
```

*Analysis applying the v5 method. Generated by running the `software-survival-analyzer` skill in Claude Code on top of a prior research pass. The summary card above corresponds to the entry incorporated into `known-cases.md` with calibration date June 2026.*
