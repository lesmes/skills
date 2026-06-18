# Known Cases, Reference Benchmarks (v4)

> Companion to the Software Survival Analyzer skill. The survival framework is
> Steve Yegge's ("Software Survival 3.0", Medium, January 2026). The scoring,
> calibration, and case library here are by Lesmes López Peña
> (https://lesmes.com, https://github.com/lesmes/skills). See SKILL.md for full
> attribution.

Tools already analyzed, to use as comparisons.
All ratios computed with the v2 formula: `(Savings × Usage) / ((Kc + Fc) × 10)`

**New fields in v4** (relative to v3):
- **Savings type**: algorithmic / regulatory / integrations / UX (see SKILL.md)
- **Geographic scope**: Global / Multi-region / Single country (affects Usage)
- **Language bias in Kc**: if the product is in a non-English-speaking market, it is flagged

These fields help calibrate correctly and avoid the biases documented in v4.

---

## 🟢 INDESTRUCTIBLE (Base ratio >50)

### PostgreSQL / MySQL
- **Type**: Tool for agents (library/driver)
- **Absurdity test**: YES. Decades of ACID optimization, concurrency, query planning. ~40 years of trial-and-error compressed.
- **Intermediation test**: NO. Does not intermediate; it IS the infrastructure.
- **Savings type**: Algorithmic (maximum insight density)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 95 · **Usage**: 95 · **Kc**: 5 · **Fc**: 10 · **H**: 10
- **Base ratio**: (95×95) / (15×10) = **60.2**
- **H boost**: None (H=10)
- **Trajectory**: → Stable. Indestructible, no foreseen changes.
- **Desire Paths**: The API (SQL) is the original desire path. Agents use it as they expect.
- **Levers**: Knowledge compression ★, Substrate efficiency ★, Broad utility ★, Awareness ★
- **Horizon**: Indefinite.
- **Forecast**: 🟢 Indestructible

### grep / Unix CLI tools
- **Type**: Tool for agents (CLI)
- **Absurdity test**: YES. Unbeatable substrate efficiency for pattern matching. ~50 years of refinement.
- **Intermediation test**: NO. Does not intermediate; it does computation on CPU cheaper than on GPU.
- **Savings type**: Algorithmic + Substrate efficiency (CPU vs GPU)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 70 · **Usage**: 85 · **Kc**: 5 · **Fc**: 5 · **H**: 10
- **Base ratio**: (70×85) / (10×10) = **59.5**
- **H boost**: None (H=10)
- **Trajectory**: → Stable. "Nobody is coming for grep" (Claude via Yegge).
- **Desire Paths**: Intuitive flags and options. Agents get it right on the first try.
- **Levers**: Substrate efficiency ★, Broad utility ★, Awareness ★, Low friction ★
- **Horizon**: Indefinite.
- **Forecast**: 🟢 Indestructible

## 🟢 VERY SAFE (Base ratio 25-50)

### Git / GitHub
- **Type**: Tool for agents (CLI/API)
- **Absurdity test**: YES. Commit DAG, branching, merging, reflog = decades of wisdom. ~30 years of trial-and-error.
- **Intermediation test**: NO. Does not intermediate; it is fundamental version-control infrastructure.
- **Savings type**: Algorithmic (high insight density)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 95 · **Usage**: 90 · **Kc**: 5 · **Fc**: 15 · **H**: 30
- **Base ratio**: (95×90) / (20×10) = **42.8**
- **H boost**: +0.5 (H=30, human code review valued)
- **Trajectory**: ↑ Improving. Agents produce 10x-100x more code -> more need for version control.
- **Desire Paths**: Good but complex (Fc=15). Git is "already losing you" as Yegge says.
- **Levers**: Knowledge compression ★, Broad utility ★, Awareness ★
- **Horizon**: Indefinite. Grows with the agentic era.
- **Forecast**: 🟢 Very safe

### Stripe
- **Type**: Tool for agents (API) + Infrastructure
- **Absurdity test**: YES. PCI-DSS, banking integrations, fraud, international taxes. ~15 years.
- **Intermediation test**: NO. Does not intermediate; it handles real payment complexity the AI cannot take on.
- **Savings type**: Algorithmic + Regulatory + Integrations (strong combination)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 90 · **Usage**: 80 · **Kc**: 10 · **Fc**: 10 · **H**: 25
- **Base ratio**: (90×80) / (20×10) = **36.0**
- **H boost**: +0.5 (H=25, trust in payments)
- **Trajectory**: → Stable. Strong regulatory/financial moat.
- **Desire Paths**: Exemplary API. The gold standard of desire paths for agents.
- **Levers**: Knowledge compression ★, Low friction ★, Awareness ★
- **v4 note**: Stripe has regulatory savings (PCI, compliance) BUT also algorithmic savings (fraud detection, payment routing). The combination puts it at 90, not just the compliance.
- **Horizon**: Indefinite.
- **Forecast**: 🟢 Very safe

## 🟢 SAFE (Base ratio 10-25)

### Docker
- **Type**: Tool for agents (CLI)
- **Absurdity test**: YES. Containerization, reproducibility, image ecosystem. ~12 years.
- **Intermediation test**: NO. Execution infrastructure, not a cognitive layer.
- **Savings type**: Algorithmic (isolation, reproducibility)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 70 · **Usage**: 80 · **Kc**: 15 · **Fc**: 20 · **H**: 10
- **Base ratio**: (70×80) / (35×10) = **16.0**
- **H boost**: None (H=10)
- **Trajectory**: → Stable. Fundamental for agents that need isolated environments.
- **Desire Paths**: Intuitive CLI, the Dockerfile is declarative and predictable.
- **Levers**: Knowledge compression, Substrate efficiency, Broad utility
- **Horizon**: Indefinite.
- **Forecast**: 🟢 Safe

### Vercel / Netlify
- **Type**: Infrastructure/substrate (with API)
- **Absurdity test**: NO. They simplify deploys but agents can use alternatives.
- **Intermediation test**: NO. Infrastructure, not a cognitive intermediary.
- **Savings type**: Integrations (git push -> deploy) + some algorithmic (edge functions)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 50 · **Usage**: 65 · **Kc**: 15 · **Fc**: 10 · **H**: 10
- **Base ratio**: (50×65) / (25×10) = **13.0**
- **H boost**: None (H=10)
- **Trajectory**: ↑ Improving. More and more agents deploy code -> more deploy automation.
- **Desire Paths**: Excellent. Git push to deploy is the perfect desire path.
- **Levers**: Low friction ★ (very clean API, git push to deploy)
- **Horizon**: Long term. Commodity infrastructure but with great DX for agents.
- **Forecast**: 🟢 Safe, survives because of the excellent DX for agents

### Kubernetes
- **Type**: Tool for agents (CLI/API)
- **Absurdity test**: YES. Container orchestration is genuinely complex. ~10 years.
- **Intermediation test**: NO. Real infrastructure, not an intermediary.
- **Savings type**: Algorithmic (distributed orchestration)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 85 · **Usage**: 75 · **Kc**: 20 · **Fc**: 35 · **H**: 10
- **Base ratio**: (85×75) / (55×10) = **11.6**
- **H boost**: None (H=10)
- **Trajectory**: → Stable. Real complexity does not go away.
- **Desire Paths**: Mediocre. High friction (Fc=35), verbose YAML, many retries.
- **Levers**: Knowledge compression ★, Substrate efficiency
- **Note**: Lower ratio than PostgreSQL due to high friction (Fc=35), not lower value
- **Horizon**: Long term, but vulnerable if simpler orchestration emerges.
- **Forecast**: 🟢 Safe

### Terraform
- **Type**: Tool for agents (CLI/declarative)
- **Absurdity test**: YES. IaC with state management and drift detection. ~10 years.
- **Intermediation test**: NO. Real infrastructure.
- **Savings type**: Algorithmic (state management, drift detection, dependency graph)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 75 · **Usage**: 70 · **Kc**: 20 · **Fc**: 25 · **H**: 10
- **Base ratio**: (75×70) / (45×10) = **11.7**
- **H boost**: None (H=10)
- **Trajectory**: → Stable. Minor threat from Pulumi/CDK but a consolidated niche.
- **Desire Paths**: Good. HCL is declarative and predictable for agents.
- **Levers**: Knowledge compression ★, Broad utility
- **Horizon**: Long term.
- **Forecast**: 🟢 Safe

## 🟡 VIABLE (Base ratio 5-10)

### Temporal
- **Type**: Tool for agents (SDK/API)
- **Absurdity test**: YES. Durable execution, sagas, exactly-once are hard problems. ~8 years.
- **Intermediation test**: NO. Solves real distributed-execution problems.
- **Savings type**: Algorithmic (durable execution, sagas, exactly-once, high insight density)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 80 · **Usage**: 75 · **Kc**: 35 · **Fc**: 30 · **H**: 10
- **Base ratio**: (80×75) / (65×10) = **9.2**
- **H boost**: None (H=10)
- **Trajectory**: ↑↑ Improving rapidly. Agentic workflows NEED durable execution. Kc will drop with adoption.
- **Desire Paths**: In progress. Good SDK but awareness is the bottleneck, not friction.
- **Levers**: Knowledge compression ★, Substrate efficiency ★, Broad utility ★
- **Note**: Ratio penalized by awareness (Kc=35) and friction (Fc=30), NOT by lack of value.
- **Horizon**: Long term. Position actively improving with the agentic era.
- **Forecast**: 🟡 Viable -> trending to 🟢 Safe

### Notion
- **Type**: SaaS for humans
- **Absurdity test**: NO. Agents can organize information without Notion.
- **Intermediation test**: NO directly. It is a human workspace, not a cognitive intermediary.
- **Savings type**: UX/Integrations (human interface, not insight density)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 40 · **Usage**: 70 · **Kc**: 15 · **Fc**: 15 · **H**: 60
- **Base ratio**: (40×70) / (30×10) = **9.3**
- **H boost**: +1.5 categories (H=60, personal/team workspace)
- **Trajectory**: → Stable. H protects but agents do not need it.
- **Desire Paths**: API available but the value is in the human interface, not the API.
- **Levers**: Human coefficient ★
- **Horizon**: Long term (protected by H).
- **Forecast**: 🟡 Viable -> 🟢 Protected by H (human thinking space)

### Slack
- **Type**: Social infrastructure
- **Absurdity test**: NO technically. BUT the network of humans is irreplaceable.
- **Intermediation test**: NO. Does not intermediate between humans and AI; it IS human communication.
- **Savings type**: UX/Integrations (the value is not algorithmic, it is social)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 30 · **Usage**: 75 · **Kc**: 10 · **Fc**: 15 · **H**: 85
- **Base ratio**: (30×75) / (25×10) = **9.0**
- **H boost**: +2 categories (H=85, human communication)
- **Trajectory**: → Stable. Extreme H protects indefinitely.
- **Desire Paths**: Good bot API. Agents can participate in Slack, they do not need to replace it.
- **Levers**: Human coefficient ★★★ (extreme)
- **Horizon**: Indefinite (social infrastructure).
- **Forecast**: 🟡 Viable -> 🟢 Safe/Protected by H (social infrastructure)

### Figma
- **Type**: SaaS for humans + Creation tool
- **Absurdity test**: DEPENDS. Real-time collaboration, yes. Individual UI design, less clear.
- **Intermediation test**: PARTIAL (~40%). UI design generation is increasingly automatable, but collaboration and human judgment are not.
- **Savings type**: Partly algorithmic (real-time collaboration engine) + UX (design tools)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 50 · **Usage**: 60 · **Kc**: 25 · **Fc**: 30 · **H**: 75
- **Base ratio**: (50×60) / (55×10) = **5.5**
- **H boost**: +1.5 categories (H=75, human design valued)
- **Trajectory**: ↓ Worsening. AI generates ever-better UI. Creativity-based H protects but automatic generation erodes it.
- **Desire Paths**: Minimal. Visual interface = high friction for agents (Fc=30).
- **Levers**: Human coefficient ★★
- **Horizon**: 3-5 years for the individual design component. Collaboration protected by H.
- **Forecast**: 🟠 At risk -> 🟡 Viable/Protected by H

## 🟠 AT RISK (Base ratio 2-5)

### Zapier / Make
- **Type**: SaaS for humans (automation intermediary)
- **Absurdity test**: NO. Agents write integrations directly with code.
- **Intermediation test**: **YES**. Intermediates between humans and automation that agents do directly. A textbook Yegge case.
- **Savings type**: Integrations (catalog of pre-made connectors)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 45 · **Usage**: 60 · **Kc**: 25 · **Fc**: 45 · **H**: 10
- **Base ratio**: (45×60) / (70×10) = **3.9**
- **H boost**: None (H=10)
- **Trajectory**: ↓↓ Worsening rapidly. Agents prefer writing code directly over using drag-and-drop UIs.
- **Desire Paths**: Minimal. The visual interface is the anti-desire-path for agents.
- **Levers**: None strong. High friction (Fc=45) because visual interfaces != agents.
- **Horizon**: 1-2 years until significant erosion.
- **Forecast**: 🟠 At risk, agents prefer direct code over drag-and-drop UIs

### Postman
- **Type**: Development tool (with visual interface)
- **Absurdity test**: NO. An agent can test APIs with curl or code.
- **Intermediation test**: **YES**. Intermediates between developers and APIs that agents call directly.
- **Savings type**: UX (visual interface for testing, no insight density)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 40 · **Usage**: 55 · **Kc**: 20 · **Fc**: 35 · **H**: 15
- **Base ratio**: (40×55) / (55×10) = **4.0**
- **H boost**: None (H=15)
- **Trajectory**: ↓ Worsening. Agents do not need a GUI to test APIs.
- **Desire Paths**: Minimal. The GUI is the value for humans but the problem for agents.
- **Levers**: Weak. The visual interface is a drag for agents.
- **Horizon**: 2-3 years.
- **Forecast**: 🟠 At risk, agents test APIs directly

### Jira
- **Type**: SaaS for humans (coordination)
- **Absurdity test**: NO technically. But organizational data and processes do matter.
- **Intermediation test**: PARTIAL (~50%). Part of project management will be done by agents, but human coordination will not.
- **Savings type**: Integrations (accumulated organizational workflows) + UX
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 35 · **Usage**: 65 · **Kc**: 20 · **Fc**: 40 · **H**: 50
- **Base ratio**: (35×65) / (60×10) = **3.8**
- **H boost**: +1 category (H=50, human coordination)
- **Trajectory**: ↓ Worsening. Agents could manage tasks without Jira. But organizational lock-in slows it down.
- **Desire Paths**: API exists but is infamous for its complexity. Anti-desire-paths.
- **Levers**: Human coefficient (partial). The bureaucracy is a drag.
- **Horizon**: 3-5 years (H and lock-in buy time).
- **Forecast**: 🟠 At risk -> 🟡 Viable (partly protected by H)

### Holded (NEW in v4)
- **Type**: SaaS for humans (business-management intermediary)
- **Absurdity test**: **NO**. An agent with knowledge of Spanish tax law and access to banking APIs (PSD2/Open Banking) could replicate most of it. There is no "insight density" comparable to Git or PostgreSQL. ~5-8 years of product refinement over standard processes.
- **Intermediation test**: **PARTIAL (~55%)**. It intermediates in: invoice OCR, automatic bank reconciliation, expense categorization, auto-filling of tax forms, all "smart things" the AI does natively. It does NOT intermediate in: Verifactu compliance (AEAT certification), SII connection, tax filing with electronic signature.
- **Savings type**: **Regulatory/institutional** (Verifactu certification, 300+ banks, AEAT forms), NOT algorithmic. There is no insight density; it is encodable compliance.
- **Geographic scope**: **Single country (Spain)**. Adjustment to Usage: -20 relative to a global equivalent.
- **Language bias in Kc**: **YES**. Spanish product, invisible in the training data of global LLMs. An English-language LLM would never mention Holded. Kc adjusted upward.
- **Savings**: 45 · **Usage**: 35 · **Kc**: 40 · **Fc**: 40 · **H**: 50
- **Base ratio**: (45×35) / ((40+40)×10) = 1575/800 = **1.97**
- **H boost**: +1 category (H=50, regulatory trust/accounting oversight)
- **Trajectory**: ↓ Worsening. LLM capabilities in accounting and invoicing improve constantly. Holded does not invest in agent UX. The regulatory moat (Verifactu) buys time but erodes.
- **Desire Paths**: Minimal. GUI-first, limited API, no MCP server, no evals, no aliases for agents. An agent would not know Holded exists or how to use it.
- **Levers**:
  - Knowledge compression 🟡 (regulatory, not algorithmic)
  - Substrate efficiency 🔴 (no advantage; cognitive tasks agents do directly)
  - Broad utility 🔴 (niche: Spain + SMBs)
  - Awareness 🔴 (invisible in global training data)
  - Low friction 🔴 (GUI-first, limited API, no desire paths)
  - Human coefficient 🟡 (regulatory trust, erodable)
- **Horizon**: No changes: 2-3 years (regulatory moat buys time). With an agent-first strategy: 5-8 years.
- **v4 note**: Holded is the case that motivated the v4 changes. The errors in its first analysis (Usage=55 instead of 35, Kc=25 instead of 40) revealed the need for the geographic penalty, the language bias, and the anti-bias checklist.
- **Forecast**: 🔴 Threatened -> 🟠 **At risk** (rescued by H=50)

### Low-code tools (Bubble, Retool)
- **Type**: Platform (intermediary)
- **Absurdity test**: NO. Their value was "you don't need a programmer", but now agents program.
- **Intermediation test**: **YES**. Textbook case: they intermediate between humans and programming the AI already does.
- **Savings type**: UX (drag-and-drop visual interface, value only for humans)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 30 · **Usage**: 50 · **Kc**: 30 · **Fc**: 50 · **H**: 25
- **Base ratio**: (30×50) / (80×10) = **1.9**
- **H boost**: +0.5 (H=25, empowering non-technical users)
- **Trajectory**: ↓↓ Worsening rapidly. Vibe coding directly replaces the value they offered.
- **Desire Paths**: Minimal. Proprietary visual interfaces = maximum friction for agents.
- **Levers**: None strong. They intermediate between humans and AI = high risk (Yegge).
- **v4 note**: Compare with Holded (1.97): almost identical ratio, same intermediation vulnerability, but Holded has more H (50 vs 25) due to the regulatory moat.
- **Horizon**: 1-2 years.
- **Forecast**: 🔴 Threatened -> 🟠 borderline (slight H helps)

## 🔴 THREATENED (Base ratio 0.5-2)

### Grammarly
- **Type**: Content tool
- **Absurdity test**: NO. LLMs already write well out of the box.
- **Intermediation test**: **YES**. Does "smart things" (grammar correction) that LLMs do natively.
- **Savings type**: None (LLMs do this natively, net negative savings)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 5 · **Usage**: 60 · **Kc**: 15 · **Fc**: 15 · **H**: 10
- **Base ratio**: (5×60) / (30×10) = **1.0**
- **H boost**: None (H=10)
- **Trajectory**: ↓↓ Worsening rapidly. Each LLM improvement reduces its value further.
- **Desire Paths**: Irrelevant. The problem is not the interface but that the product is redundant.
- **Levers**: None. Does "smart things that LLMs already do" (Yegge).
- **Horizon**: 1 year.
- **Forecast**: 🔴 Threatened

### Stack Overflow
- **Type**: Social infrastructure + Content tool
- **Absurdity test**: NO for the answers. PARTIAL for the community curation.
- **Intermediation test**: **YES**. Intermediates between programmers and answers that LLMs give directly.
- **Savings type**: Integrations (accumulated community curation, but already internalized in LLMs)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 10 · **Usage**: 50 · **Kc**: 15 · **Fc**: 25 · **H**: 20
- **Base ratio**: (10×50) / (40×10) = **1.25**
- **H boost**: +0.5 (H=20, weak community)
- **Trajectory**: ↓↓ Worsening rapidly. Traffic already collapsed ~50%.
- **Desire Paths**: Irrelevant. Agents do not search Stack Overflow; they have the answers internalized.
- **Levers**: Weak human coefficient. Traffic already collapsed ~50%.
- **Horizon**: 1-2 years as a relevant resource.
- **Forecast**: 🔴 Threatened

### Simple compilers/transpilers
- **Type**: Tool for agents (in theory)
- **Absurdity test**: NO. LLMs convert code between languages directly.
- **Intermediation test**: **YES**. They do code transformation that LLMs do natively.
- **Savings type**: Partly algorithmic (but LLMs replicate the functionality natively)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 5 · **Usage**: 40 · **Kc**: 20 · **Fc**: 20 · **H**: 10
- **Base ratio**: (5×40) / (40×10) = **0.5**
- **H boost**: None (H=10)
- **Trajectory**: ↓↓ Worsening rapidly.
- **Desire Paths**: Irrelevant.
- **Levers**: None.
- **Horizon**: <1 year.
- **Forecast**: 🔴 Threatened

## 🔴 CRITICAL (Base ratio <0.5)

### Jasper / Copy.ai (content generators)
- **Type**: Content tool (LLM wrapper)
- **Absurdity test**: NO. They are literally wrappers over LLMs that add overhead.
- **Intermediation test**: **YES**. Extreme case: they intermediate between humans and LLMs that the user could use directly.
- **Savings type**: Negative (they add overhead over direct LLMs)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: -10 · **Usage**: 50 · **Kc**: 25 · **Fc**: 30 · **H**: 10
- **Base ratio**: Negative -> **<0**
- **H boost**: None (H=10)
- **Trajectory**: ↓↓ Already collapsing.
- **Desire Paths**: Irrelevant. The product should not exist in the agentic era.
- **Levers**: None. "Unnecessary intermediaries" (Yegge).
- **Horizon**: Already in crisis.
- **Forecast**: 🔴 Critical

### Chegg
- **Type**: Content tool
- **Absurdity test**: NO. LLMs have the answers internalized.
- **Intermediation test**: **YES**. Intermediates between students and answers that LLMs give for free.
- **Savings type**: None (content already internalized in LLMs)
- **Geographic scope**: Global. No adjustment to Usage.
- **Savings**: 0 · **Usage**: 40 · **Kc**: 20 · **Fc**: 25 · **H**: 10
- **Base ratio**: **0**
- **H boost**: None (H=10)
- **Trajectory**: ↓↓ Already collapsing. Traffic in free fall.
- **Desire Paths**: Irrelevant.
- **Levers**: None. Already suffering traffic collapse.
- **Horizon**: Already in crisis.
- **Forecast**: 🔴 Critical

---

## Key Patterns

### Signals of HIGH survival (base ratio >10):
- Decades of crystallized knowledge that would be absurd to rediscover (crystallized cognition)
- **Algorithmic savings type**, genuine insight density, not compliance or UX
- Computation more efficient on CPU than on GPU
- Omnipresent in training data (low Kc)
- Clean API with "desire paths" for agents (low Fc)
- The agent would ACTIVELY choose it over doing it itself
- Does NOT intermediate, it IS the infrastructure
- Fails the intermediation test (does not intermediate)
- Passes the absurdity test (it would be absurd to re-synthesize it)
- **Global scope**, amortizes awareness cost with volume (v4)

### Signals of LOW survival (base ratio <3):
- Does "smart things" that LLMs already do natively (fails the intermediation test)
- Intermediates between humans and AI without adding unique value
- Visual interface hard to automate (high Fc)
- Wrapper over LLMs with no added value (negative Savings)
- The agent would pass it by and do the same on its own
- Few decades of trial-and-error compressed
- Does NOT pass the absurdity test
- **UX or integrations savings type**, not algorithmic (v4)
- **Limited geographic scope**, high penalty in Usage (v4)
- **Non-English-speaking product**, Kc underestimated if not adjusted for language bias (v4)

### When H saves and when it does not:
- **H saves long term** (H>=70) when the product IS the human connection/creativity (Slack, Figma, games)
- **H protects temporarily** (H 40-60) when trust/regulation is involved (payments, medicine, accounting), this protection erodes over time as trust in AI grows
- **H does NOT save** (H<40) when the human component is replaceable (customer support, content curation the AI will soon do equally well)

### "Hosting and similar" pattern (commodity infrastructure):
- Hosting, CDN, DNS, etc. are necessary but commodity substrate
- Survivors are those with a clean API (Cloudflare, Vercel): base ratio 10-15
- Those die that only have a web panel (no API for agents): base ratio 1-3
- The differentiation comes not from the service but from the programmatic interface

### "Cognitive intermediary" pattern:
- Software that interposes a layer between the user and a task the AI does directly
- Includes: low-code tools, LLM wrappers, visual automation, writing assistants
- Quick test: "could the user ask an agent to do this directly?"
- If YES -> the software intermediates -> high risk
- Trend: ↓↓ worsening for all intermediaries as agents improve

### "Desire paths as defense" pattern:
- Software with high Savings but high Fc can improve dramatically by implementing desire paths
- Example: Temporal (ratio 9.2) could rise to ~15+ if it lowers Fc from 30 to 15 with better agent UX
- Reverse example: Jira (ratio 3.8) suffers because its API is anti-desire-paths (Fc=40)
- Investment in desire paths has the best ROI of all the levers for established software

### "Regional SaaS" pattern (NEW in v4):
- SaaS software successful in a single country/language but invisible globally
- Suffers a DOUBLE penalty: low Usage (geographic scope) + high Kc (language bias)
- Example: Holded (ratio 1.97) vs. global QuickBooks (estimated ratio ~5+)
- **Common trap**: confusing "leader in my market" with "tool an agent would choose"
- **Possible defense**: become regulatory infrastructure for agents (the "Stripe of
  Spanish taxation"), not a pretty ERP for humans
- The regional tools that survive will be those that become agent-first regulatory APIs,
  not those with a better GUI

### "Regulatory vs algorithmic savings" pattern (NEW in v4):
- Not all savings are equal. Algorithmic savings (Git, PostgreSQL, Temporal) is the most
  defensible because it requires decades of insight density to replicate.
- Regulatory savings (certifications, compliance, institutional agreements) is REAL but
  more vulnerable: regulation can be encoded and agents can learn law.
- **Stripe is the exception** that proves the rule: it has BOTH types (fraud = algorithmic,
  PCI = regulatory), which is why its Savings=90 is justified.
- A product with ONLY regulatory savings typically deserves Savings 30-50, not 60+.
