# Changelog

All notable changes to this skill are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [2.1.0] - 2026-07-20

### Changed — Regulatory Timeline (Digital Omnibus on AI)
- Updated all high-risk deadlines per the **Digital Omnibus on AI** (COM(2025) 836; endorsed by the European Parliament 16 Jun 2026 and the Council 29 Jun 2026):
  - Annex III stand-alone high-risk systems: **2 Aug 2026 → 2 December 2027**
  - Annex I high-risk (AI in regulated products): **2 Aug 2027 → 2 August 2028**
  - National regulatory sandboxes: **2 Aug 2026 → 2 August 2027**
- **Article 50 transparency obligations unchanged** — still apply from 2 August 2026
- Added the Art. 50(2) watermarking grace period (to 2 December 2026 for systems already on the market before 2 Aug 2026)
- Refreshed stale model-name examples (e.g. "Claude Sonnet 4" → current models)

### Changed — Maintenance
- **Centralized verification tracking** into a single root file `LAST_VERIFIED.md`. Per-file `<!-- Last verified: DATE -->` headers replaced with dateless `<!-- Verification status: see LAST_VERIFIED.md -->` pointers — one date to update per pass instead of ~40, eliminating drift.
- Removed committed build artifacts (`ai-act-compliance.zip`, `files.zip`)

### Added — New Regulatory Developments
- Two new **Art. 5 prohibited practices** (non-consensual intimate imagery / "nudifiers", CSAM), effective December 2026
- **Transparency Code of Practice** (marking and labelling of AI-generated content), finalized 10 June 2026
- Note on the draft **Art. 6 high-risk classification guidelines** (published 19 May 2026; consultation open to 23 July 2026; not yet adopted)
- Italy: **Legge n. 132/2025** national AI law (in force 10 October 2025; AgID = notifying authority, ACN = market-surveillance authority)
- GPAI Code of Practice signatories (Anthropic, OpenAI, Google, Microsoft, Mistral; Meta declined)
- National market-surveillance authority designations: BNetzA (DE), CNIL AI division (FR), AESIA (ES), RDI (NL)

### Note
- At the time of this update the Digital Omnibus's final **Official Journal** regulation number and exact entry-into-force date were not yet confirmed — verify on [EUR-Lex](https://eur-lex.europa.eu) before relying on any date.
- As of July 2026, **no AI Act harmonized standards** have yet been cited in the Official Journal (no presumption of conformity available; availability expected in 2026).

## [2.0.0] - 2026-03-28

### Added — Regulatory Coverage
- `references/value-chain-obligations.md` — Arts. 22-28 value chain responsibilities
- `references/deployer-obligations.md` �� Art. 26-27 deployer duties + FRIA template
- `references/gpai-obligations.md` — Arts. 51-56, when fine-tuning crosses the line
- `references/regulatory-sandbox.md` — Arts. 57-62, how to get into an EU sandbox
- `references/annex-iv-template.md` — Full Annex IV technical documentation template
- `references/conformity-assessment.md` — Step-by-step self-assessment and CE marking
- `references/incident-response.md` — Incident playbook with Art. 73 reporting
- `references/standards-tracker.md` — CEN/CENELEC harmonized standards tracking
- `references/provider-comparison.md` — AI provider comparison (compliance edition)
- Art. 95 voluntary codes of conduct section in SKILL.md
- Recital references throughout

### Added — Internationalization
- Full English-first content (all core files)
- `references/national/germany.md` — BfDI, BSI, BNetzA
- `references/national/france.md` — CNIL, ANSSI
- `references/national/spain.md` — AEPD, first EU sandbox
- `references/national/netherlands.md` — AP, Algorithm Register
- `references/national/TEMPLATE.md` — For community contributions

### Added — Code Patterns (9 frameworks)
- Next.js, FastAPI, Django, Go, Spring Boot, .NET
- CI/CD (GitHub Actions, pre-commit), Testing (Jest, Pytest, Playwright), C2PA

### Added — Sector Guides (5 sectors)
- Fintech, Healthtech, Edtech, HR-tech, Legaltech

### Added — Interactivity
- Risk classification decision tree (executable by agent)
- Compliance scoring system (0-100)
- Formal compliance report template
- Multi-system compliance dashboard

### Added — Ecosystem
- `CONTRIBUTING.md` with style guide and tone guidelines
- `LEGAL_NOTICE.md` — Full limitation of liability (you use this at your own risk)
- `.github/ISSUE_TEMPLATE/` — 5 structured templates
- How to Cite section with BibTeX

### Changed
- **BREAKING**: Directory restructured. `italian-context.md` → `national/italy.md`, `checklist-completa.md` → `checklist.md`
- All core content now English-first
- Enhanced auto-update workflow with critical events monitoring
- Strengthened legal disclaimers everywhere
- README rewritten — lighter tone, comprehensive tables

## [1.0.0] - 2026-03-28

### Added
- Initial release with risk classification workflow
- 219-point compliance checklist (Italian)
- Pre-deploy checklist and documentation templates
- Code patterns: React, Python, SQL, API
- Common SaaS scenarios
- High-risk requirements (Arts. 9-17)
- Art. 50 transparency guide with code
- Italian regulatory context (Garante, AgID, ACN)
- Auto-update workflow
- Apache 2.0 License

### Regulatory Coverage
- Art. 4 (AI Literacy), Art. 5 (Prohibited Practices)
- Art. 6 + Annex III (High-Risk Classification)
- Arts. 9-17 (High-Risk Requirements)
- Art. 22 GDPR (Automated Decisions), Art. 25 (Value Chain)
- Art. 50 (Transparency), Art. 71 (EU Database)
- Art. 73 (Incident Reporting), Art. 99 (Penalties)
