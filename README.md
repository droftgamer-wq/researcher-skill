# Research Skills

Purpose-based research skills for Codex / Claude Code.

This repository started as a single `researcher` skill. It is now a small
research skill system:

- one shared core and router skill
- multiple purpose-specific skills
- shared reference packs for evidence classes and search strategy

English | [中文](README.zh-CN.md)

## What This Repository Is

These skills are designed for research tasks that are:

- open-ended
- multi-source
- judgment-heavy
- vulnerable to hype, shallow summaries, or one-sided narratives

The system keeps the original breadth-first then depth-first idea, but upgrades
it from topic search to evidence-driven investigation:

```text
FRAME -> MAP -> FRONTIER -> DEEPEN -> CHALLENGE -> SYNTHESIZE
```

That means:

- the first pass maps evidence classes, not just webpages
- later search becomes lead-driven, not generic query reformulation
- strong conclusions require support, challenge paths, and visible reasoning

## Included Skills

| Skill | Use when you need to... |
|---|---|
| `researcher` | Route an ambiguous research request and run the shared research operating system |
| `field-mapping-research` | Map a space, identify branches, actors, debates, and next leads |
| `claim-validation-research` | Test whether a claim, report, metric, or narrative holds up |
| `decision-support-research` | Compare options and recommend a path under real constraints |
| `opportunity-research` | Find credible opportunities, wedges, or emerging directions |
| `due-diligence-research` | Stress-test a company, product, or thesis against reality |
| `operator-reality-research` | Understand day-to-day work, hidden friction, and lived experience |

## Core Design

### 1. Purpose-first routing

Top-level skills are split by search purpose, not by topic.

This matters because a single question may span:

- papers
- job markets
- community signals
- company evidence
- adversarial material

Example:

`"Is AI agent engineer a real entry-level path?"`

This is not only a job-market question. It may require:

- exact-title job postings
- adjacent-title job postings
- company hiring pages
- LinkedIn trajectories
- Reddit or forum experience
- skeptical or adversarial takes

### 2. Evidence classes instead of single-source hierarchy

The shared references treat the internet as a mixed evidence environment:

- official
- behavioral
- operator
- lived experience
- adversarial
- market proxy
- artifact

This avoids the common mistake of treating "official" as automatically true or
treating social/community sources as automatically useless.

### 3. Visible reasoning

Each skill is written to keep a visible `research-{topic}.md` log while working.
The goal is to avoid the familiar failure mode of "searched a lot, but I cannot
see the actual reasoning path."

## Repository Structure

```text
researcher-skill/
├── README.md
├── README.zh-CN.md
├── researcher/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── core-method.md
│       ├── frontier-management.md
│       ├── query-shaping.md
│       ├── saturation-and-counterevidence.md
│       ├── scientific-literature.md
│       ├── source-hierarchy.md
│       ├── source-packs-company-intel.md
│       ├── source-packs-field-signals.md
│       └── source-packs-jobs.md
├── field-mapping-research/
├── claim-validation-research/
├── decision-support-research/
├── opportunity-research/
├── due-diligence-research/
└── operator-reality-research/
```

## How The Skills Fit Together

`researcher/` is the shared core:

- router skill
- common workflow
- source hierarchy
- query shaping
- challenge-path logic
- source packs

The purpose-specific sibling skills are intentionally thin:

- strong trigger descriptions
- focused workflow
- shared references to `../researcher/references/...`

This keeps the shared method centralized while letting each skill stay tuned to
its research purpose.

## Installation

### Local install

Clone the repository:

```bash
git clone https://github.com/recomby-ai/researcher-skill.git
```

Copy all skill folders into your Codex/Claude skill directory:

```bash
cp -R researcher-skill/researcher ~/.codex/skills/
cp -R researcher-skill/field-mapping-research ~/.codex/skills/
cp -R researcher-skill/claim-validation-research ~/.codex/skills/
cp -R researcher-skill/decision-support-research ~/.codex/skills/
cp -R researcher-skill/opportunity-research ~/.codex/skills/
cp -R researcher-skill/due-diligence-research ~/.codex/skills/
cp -R researcher-skill/operator-reality-research ~/.codex/skills/
```

If you are using Claude Code instead of Codex, copy the same folders into
`~/.claude/skills/`.

Important:

- install `researcher/` together with the purpose-specific skills
- the sibling skills rely on the shared references inside `researcher/`

### Web upload

When uploading to a web UI, zip the skill directories together.

Include:

- `researcher/`
- `field-mapping-research/`
- `claim-validation-research/`
- `decision-support-research/`
- `opportunity-research/`
- `due-diligence-research/`
- `operator-reality-research/`

Do not upload only one purpose-specific skill unless you also include
`researcher/`, because the shared references live there.

## Example Prompts

```text
Use $field-mapping-research to map the AI agent engineering job market.
Use $claim-validation-research to verify whether this industry claim holds up.
Use $decision-support-research to compare quant, AI infrastructure, and applied ML for a math undergraduate.
Use $opportunity-research to identify the most promising wedges in vertical AI for SMBs.
Use $due-diligence-research to stress-test this startup narrative.
Use $operator-reality-research to find what practitioners actually complain about in production agent systems.
Use $researcher to investigate what is really happening here and choose the right research mode.
```

## Notes On Current Behavior

This repository was refactored to address a few recurring failure modes:

- too much generic search, not enough lead chasing
- not enough challenge-path work
- role or market research getting trapped by exact job titles
- invisible reasoning during long searches

The current skills explicitly push for:

- breadth-first evidence mapping
- visible research logs
- exact-title and adjacent-title checks for market claims
- use of community, adversarial, and operator sources as signal paths

## Limitations

- public-web access still depends on available search and fetch tools
- some sources remain inaccessible behind paywalls or platform login
- social and community sources are useful, but still require triangulation
- these skills improve research behavior; they do not replace domain expertise

## License

MIT
