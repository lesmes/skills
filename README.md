# skills

Skills for the agentic era — by [Lesmes López Peña](https://lesmes.com).

> Companion to the launch post: [*Will Your Software Survive the Agents? Two Skills for the Agentic Era*](https://lesmes.com/blog/will-your-software-survive-the-agents-two-skills-for-the-agentic-era).

When agents stopped autocompleting and started writing their own code, running it, and calling tools when they needed them, two questions stopped being rhetorical:

1. **Will this thing survive?** Given a tool, SaaS, or technology that already exists, what are its odds in the agentic era?
2. **How do I build for it?** If I am designing a product now, what makes an agent discover it, use it, and prefer it over doing the work alone?

This repo packages a skill for each.

## The skills

### [software-survival-analyzer](software-survival-analyzer/) — the diagnostic lens

An implementation of Steve Yegge's framework from [Software Survival 3.0](https://steve-yegge.medium.com/software-survival-3-0-97a2a6255f7b). Two binary gut-checks (would it be absurd to re-synthesize this? does it intermediate between humans and tasks the AI will soon do on its own?), then a scored model — how much cognition the tool saves, how broadly it is used, how easily an agent can know about it and use it — plus a separate human-preference factor for things that survive because people want them, not because they are efficient.

Output: a survival forecast, a trajectory (improving or eroding), the competitive picture, and concrete levers to pull. Includes a calibrated case library (Git, Stripe, Docker, Kubernetes, Notion, Slack, Figma, Jira, Zapier, Holded, Grammarly, Chegg…) so scores are anchored against benchmarks, not assigned in a vacuum.

**Use it when**: you want to look at something that already exists — your product, a competitor, a stack you depend on — and ask honestly how exposed it is.

### [agent-first-readiness](agent-first-readiness/) — the design lens

An original framework that synthesizes ideas from [Steve Yegge](https://steve-yegge.medium.com/software-survival-3-0-97a2a6255f7b) (desire paths), [Andrej Karpathy](https://x.com/karpathy/status/2004607146781278521) (build for agents), [Alex Zhang](https://alexzhang13.github.io/blog/2026/scaffold/) (scaffold-LMs), [Andrew Ng](https://x.com/AndrewYNg/status/2031051809499054099) (Context Hub) and [Danila Poyarkov](https://github.com/dannote/figma-use) (figma-use). It scores a product across six dimensions:

1. **Discoverability** — can an agent find you at all?
2. **Consumability** — can it use you without friction?
3. **Value vs. alternative** — would it prefer you over doing the job itself?
4. **Open source strategy** — what teaches the agent, what makes you necessary?
5. **Defensibility** — do you survive when scaffold-LMs improve?
6. **Operational reliability** — can you serve bursty agentic traffic?

Each dimension scores 0–10, gaps turn into concrete actions, and the actions get sorted by impact over effort so you know what to fix first.

**Use it when**: you are designing or auditing a product, API, or service and want to know whether an agent would find it, choose it, and keep choosing it.

## How they fit together

One is diagnosis, the other is design. The survival analyzer asks *"will it last?"* and is most useful pointed at things that already exist. The readiness assessment asks *"how do I make it last, and get used?"* and is most useful pointed at what you are building next. Run the first and you understand the pressure. Run the second and you do something about it.

Neither tries to predict the future with false precision. They are structured ways to ask better questions and to replace hand-wavy intuition with something you can score, compare, and act on.

## Quickstart — try it: Figma in June 2026

A live application of the framework to a case the market is actively debating. The summary below is the output of running the `software-survival-analyzer` skill in Claude Code (Opus 4.8, max) on top of a prior research pass — public business data, product evolution, the X.com sentiment split on Figma's agentic-era fate.

| Field | Value |
|-------|-------|
| Type | SaaS for humans + content creation + tool for agents (emerging) |
| Absurdity test | DEPENDS (collaboration yes, design generation no) |
| Intermediation test | PARTIAL ~40% (design generation) |
| Base ratio (v4 baseline / 2026 evidence) | 5.5 / **6.4** |
| Composite H | 72 (collaboration ~85 durable + design taste ~55 erodable) |
| H boost | +1.5 categories |
| **Final forecast** | 🟡 Viable → 🟢 Protected by H *(conditional on the orchestration pivot)* |
| Trajectory | → Bifurcating (orchestration ↑ / design generation ↓) |
| Horizon | 3–5 years for the design component; >5 years for the platform if it executes the pivot |

**The non-obvious finding the framework surfaces**: H is not one number, it is two with very different half-lives. Figma's *multiplayer collaboration* H (~85) is durable, Slack-like. Its *design-taste* H (~55) is exactly in the band the skill flags as erodable. Figma's long-term protection does **not** rest on people wanting a human to do the design — it rests on the team wanting to collaborate on a shared artifact. That decomposition is what changes the strategic question from *"will AI design tools kill Figma?"* to *"can Figma pivot to being the system of record agents read and write to?"*.

**Read the full analysis** — binary tests, side-by-side scoring, anti-bias checklist, the 6 levers, desire-paths evaluation, competition map, and four lever-aligned recommendations — in [`examples/figma-2026-06.md`](examples/figma-2026-06.md).

**A second worked case** — Salesforce. Also bifurcated, but for a different reason: its dominant moat (data gravity + switching costs + organizational inertia) sits *outside* what Yegge's formula measures well. The framework names that gap as a methodological caveat instead of forcing the variables to hit a flattering number. See [`examples/salesforce-2026-06.md`](examples/salesforce-2026-06.md) — the case is the closest the framework gets to admitting where it doesn't fit, which is exactly the "uncomfortable case" the survival analyzer is built for.

## Installing as Claude Skills

Each folder is a self-contained [Claude Skill](https://docs.claude.com/en/docs/claude-code/skills) with a `SKILL.md`. To use them:

```bash
# Personal (all your sessions)
git clone https://github.com/lesmes/skills.git ~/skills-repo
cp -r ~/skills-repo/software-survival-analyzer ~/.claude/skills/
cp -r ~/skills-repo/agent-first-readiness     ~/.claude/skills/

# Or per-project
cp -r ~/skills-repo/software-survival-analyzer .claude/skills/
cp -r ~/skills-repo/agent-first-readiness     .claude/skills/
```

Claude picks them up automatically from the SKILL.md descriptions — no manual registration. Triggers in English and Spanish are documented in each `SKILL.md`.

## License & attribution

Both skills are released under the **MIT License** (see each folder's `LICENSE`).

The MIT covers the original layers authored here: numerical calibration, scoring rubrics, case libraries, anti-bias checklists, output formats, and the six-dimension model for agent-first readiness. The underlying ideas remain attributed to their authors:

- **Steve Yegge** — [*Software Survival 3.0*](https://steve-yegge.medium.com/software-survival-3-0-97a2a6255f7b) (the survival framework)
- **Andrej Karpathy** — [thread on X on the new agentic abstraction layer](https://x.com/karpathy/status/2004607146781278521) (building for agents, Skills as an abstraction layer)
- **Alex Zhang** — [*Language Models will be Scaffolds*](https://alexzhang13.github.io/blog/2026/scaffold/)
- **Andrew Ng** — [Context Hub (chub)](https://x.com/AndrewYNg/status/2031051809499054099)
- **Danila Poyarkov** — [figma-use](https://github.com/dannote/figma-use) (single operation, dual output, token efficiency)

Read their work first. These skills only operationalize it.

## The question

The bar is no longer whether your software is good. It is whether an agent would stop to use it instead of doing the job itself. These two skills are built to help you clear it.
