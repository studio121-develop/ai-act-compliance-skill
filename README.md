# AI Act Compliance Skill for Claude Code

> The first skill for Claude Code (and compatible AI agents) that actually makes EU AI Act compliance... not terrible.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Agent Skills Standard](https://img.shields.io/badge/Agent_Skills-SKILL.md-purple.svg)](https://agentskills.io)
[![AI Act](https://img.shields.io/badge/EU_AI_Act-2024%2F1689-yellow.svg)](https://artificialintelligenceact.eu/)

---

## Why This Exists

So you're building a SaaS with Claude API, OpenAI, or whatever model-of-the-month via API. Congrats — the EU AI Act now considers you a **Provider**. Not a deployer. A *provider*. Yes, the one with actual obligations.

This means transparency requirements, documentation duties, and governance rules that kick in **August 2, 2026**. And if your AI does anything in the high-risk ballpark (hiring, credit scoring, education decisions), you've got a whole extra layer of fun waiting for you.

This skill embeds compliance directly into your development workflow: risk classification, operational checklists, documentation templates, ready-to-use code patterns, and regulatory context — so you can focus on building instead of reading 144 pages of EU regulation.

## What's Inside

| File | What it does |
|------|-------------|
| `SKILL.md` | The brain — risk classification workflow, pre-deploy checklist, doc templates, code patterns |
| `references/checklist.md` | **219 verification points**, article by article, organized by lifecycle phase. Yes, 219. We counted. |
| `references/high-risk-requirements.md` | Everything about Arts. 9-17 obligations (the scary ones) |
| `references/transparency-implementation.md` | Art. 50 technical guide with actual code you can copy-paste |
| `references/value-chain-obligations.md` | Who's responsible for what: model provider → you → your customers |
| `references/deployer-obligations.md` | What your B2B customers need to do (and what you need to tell them) |
| `references/gpai-obligations.md` | For those of you fine-tuning models — yes, that changes things |
| `references/regulatory-sandbox.md` | How to get into an EU sandbox (the legal kind) |
| `references/conformity-assessment.md` | Self-assessment walkthrough — less painful than it sounds |
| `references/annex-iv-template.md` | Technical documentation template that actually follows Annex IV |
| `references/incident-response.md` | When things go wrong — playbook with Art. 73 reporting templates |
| `references/provider-comparison.md` | Anthropic vs OpenAI vs Google vs Mistral from a compliance lens |
| `references/standards-tracker.md` | CEN/CENELEC harmonized standards — what's coming and when |
| `references/auto-update.md` | How to keep this skill current with regulatory changes |

### National Contexts

Because "the EU" is actually 27 countries, each doing their own thing:

| File | Country |
|------|---------|
| `references/national/italy.md` | Italy — Garante, AgID, ACN, templates in italiano |
| `references/national/germany.md` | Germany — BfDI, BSI, BNetzA |
| `references/national/france.md` | France — CNIL, ANSSI, home of Mistral |
| `references/national/spain.md` | Spain — AEPD, first EU sandbox |
| `references/national/netherlands.md` | Netherlands — AP, Algorithm Register pioneer |
| `references/national/TEMPLATE.md` | Want to add your country? Start here |

### Code Patterns

Real code for real frameworks, not pseudocode from a law firm's PDF:

| File | Framework |
|------|-----------|
| `references/patterns/nextjs.md` | Next.js — middleware, App Router, Server Actions |
| `references/patterns/fastapi.md` | FastAPI — middleware, Pydantic models, dependency injection |
| `references/patterns/django.md` | Django — middleware, model mixins, template tags |
| `references/patterns/go.md` | Go — HTTP middleware, struct patterns |
| `references/patterns/spring-boot.md` | Spring Boot — interceptors, JPA entities, AOP |
| `references/patterns/dotnet.md` | .NET — ASP.NET Core middleware, EF patterns |
| `references/patterns/cicd.md` | CI/CD — GitHub Actions, pre-commit hooks |
| `references/patterns/testing.md` | Testing — Jest, Pytest, Playwright compliance tests |
| `references/patterns/c2pa.md` | C2PA — content provenance implementation |

### Sector Guides

Because a chatbot for pizza orders and an AI that scores credit applications are... not the same thing:

| File | Sector |
|------|--------|
| `references/sectors/fintech.md` | Fintech — credit scoring, insurance, fraud detection |
| `references/sectors/healthtech.md` | Healthtech — clinical AI, MDR intersection |
| `references/sectors/edtech.md` | Edtech — admissions, scoring, minors |
| `references/sectors/hrtech.md` | HR-tech — recruitment, CV screening, performance eval |
| `references/sectors/legaltech.md` | Legaltech — legal research, case prediction |

## Installation

### Claude Code (terminal)

```bash
# Option 1: Project-level (recommended)
git clone https://github.com/studio121-develop/ai-act-compliance-skill.git .claude/skills/ai-act-compliance

# Option 2: Global (available in all projects)
git clone https://github.com/studio121-develop/ai-act-compliance-skill.git ~/.claude/skills/ai-act-compliance
```

### Claude.ai (web/app)

1. [Download the ZIP](https://github.com/studio121-develop/ai-act-compliance-skill/archive/refs/heads/main.zip)
2. Go to **Customize > Skills**
3. Upload the ZIP
4. Feel slightly more responsible

### Other Compatible Agents (Codex, Cursor, Gemini CLI)

```bash
# OpenAI Codex CLI
cp -r ai-act-compliance ~/.codex/skills/

# Cursor / other SKILL.md-compatible agents
cp -r ai-act-compliance .skills/
```

## Usage

The skill activates automatically when you're working on AI-powered projects. You can also summon it explicitly:

```
Classify the AI Act risk level of my project
```

```
Generate AI Act compliance documentation for my SaaS
```

```
Run the AI Act pre-deploy checklist
```

```
Audit my codebase for AI Act compliance
```

```
Update the AI Act compliance skill with the latest regulatory news
```

### What Triggers It

- Building a chatbot → skill suggests Art. 50 obligations
- Integrating Claude API → skill classifies you as Provider
- Adding AI features to an e-commerce → skill evaluates risk
- Preparing to deploy → skill runs the pre-deploy checklist
- Mentioning "AI Act", "compliance", "transparency", "GPAI", "high-risk" → skill wakes up

## Who It's For

- **SaaS builders** integrating AI via API (Claude, OpenAI, Mistral, etc.)
- **Digital agencies** building AI products for clients
- **Indie hackers** and **vibe coders** shipping AI features fast
- **European SMEs** that need to comply without hiring a law firm
- **Consultants** helping clients navigate AI regulation

## Compatibility

| Platform | Support |
|----------|---------|
| Claude Code | Native |
| Claude.ai (Pro/Max/Team/Enterprise) | Via upload |
| Claude API (code execution) | Via Skills API |
| OpenAI Codex CLI | SKILL.md format compatible |
| Cursor | SKILL.md format compatible |
| Gemini CLI | SKILL.md format compatible |

## Keeping It Current

Regulations change. Standards get published. Authorities issue guidance. The skill includes a structured update workflow — just ask:

```
Update the AI Act compliance skill with the latest regulatory news
```

Claude will search primary EU and national sources, update the relevant files, and log changes. See `references/auto-update.md` for the full workflow, monitored sources, and update schedule.

**Recommended cadence**: monthly until August 2026, quarterly after that.

## AI Act Timeline

| Date | What | Status |
|------|------|--------|
| Feb 2025 | Prohibited practices + AI literacy | In force |
| Aug 2025 | GPAI model obligations + governance | In force |
| **Aug 2026** | **Art. 50 transparency + high-risk (Annex III standalone)** | Next deadline |
| Aug 2027 | High-risk in regulated products (medical devices, machinery) | Coming |

## Contributing

We'd love your help making this THE reference for AI Act compliance. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to:

- Report regulatory inaccuracies (highest priority — compliance tools can't be wrong)
- Add your country's national context
- Add code patterns for new frameworks
- Add sector-specific guides
- Translate content

## How to Cite

If you reference this skill in articles, papers, or documentation:

**Plain text:**
> Studio121 Srls. (2026). AI Act Compliance Skill for Claude Code. GitHub. https://github.com/studio121-develop/ai-act-compliance-skill

**BibTeX:**
```bibtex
@misc{studio121_aiact_2026,
  author = {Studio121 Srls},
  title = {AI Act Compliance Skill for Claude Code},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/studio121-develop/ai-act-compliance-skill}
}
```

## License

Apache License 2.0 — see [LICENSE](LICENSE).

## Author

**Studio121 Srls** — Web design, digital communications & AI-powered products.
Ragusa, Sicily

- Web: [studio121.it](https://studio121.it)
- GitHub: [@studio121-develop](https://github.com/studio121-develop)

---

> **Disclaimer**: This skill provides operational guidance for EU AI Act compliance but **does not constitute legal advice** and **does not guarantee compliance**. It is not endorsed by or affiliated with the European Commission, the AI Office, or any national competent authority. You use this skill at your own risk. Regulatory interpretation may change as implementing acts, delegated acts, harmonized standards, and case law develop. For specific cases, consult a qualified legal professional specializing in EU digital regulation. For full terms, see [LEGAL_NOTICE.md](LEGAL_NOTICE.md). That said — if you're reading 219-point checklists at midnight, you're probably more prepared than most.
