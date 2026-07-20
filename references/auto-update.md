<!-- Verification status: see LAST_VERIFIED.md -->

# Keeping This Skill Current

The EU AI Act is a living regulation. Implementing acts, delegated acts, harmonized standards, codes of practice, and national implementation laws are being developed continuously. A compliance skill that doesn't keep up is worse than no skill at all — it gives you false confidence.

This file defines the update workflow, monitored sources, and change management process.

## How to Update

Ask Claude:

```
Update the AI Act compliance skill with the latest regulatory news.
```

Claude will execute this workflow:

### Step 1: Search for Updates

Search the web for recent developments on:
- AI Act implementing and delegated acts
- Harmonized standards from CEN/CENELEC JTC 21
- AI Office guidelines and FAQs
- GPAI Code of Practice updates
- Transparency Code of Practice progress
- National implementation laws across EU member states
- Relevant court decisions and enforcement actions
- Italian authorities (Garante, AgID, ACN) — and other national authorities in covered countries

### Step 2: Check Primary Sources

Verify these sources for new content:

**EU Primary Sources (always check these):**
- https://artificialintelligenceact.eu — Analysis and tracking
- https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai — European Commission
- https://ai-act-service-desk.ec.europa.eu — Official service desk
- https://eur-lex.europa.eu — Official text, amendments, corrigenda
- https://ec.europa.eu/transparency/comitology-register/ — Implementing acts tracker

**AI Office & GPAI:**
- AI Office official communications
- GPAI Code of Practice (published July 2025) — updates and revisions
- Transparency Code of Practice — development progress
- Scientific Panel opinions

**Standards Bodies:**
- CEN/CENELEC JTC 21 — harmonized standards development
- ISO/IEC JTC 1/SC 42 — AI standards (42001, 23894, 24029, etc.)
- ETSI — AI-related standards
- C2PA — Content Provenance and Authenticity

**National Sources (check for covered countries):**

| Country | Authority | URL |
|---------|-----------|-----|
| Italy | Garante Privacy | https://www.garanteprivacy.it |
| Italy | AgID | https://www.agid.gov.it |
| Italy | ACN | https://www.acn.gov.it |
| Germany | BfDI | https://www.bfdi.bund.de |
| Germany | BSI | https://www.bsi.bund.de |
| France | CNIL | https://www.cnil.fr |
| France | ANSSI | https://www.ssi.gouv.fr |
| Spain | AEPD | https://www.aepd.es |
| Netherlands | AP | https://www.autoriteitpersoonsgegevens.nl |

**Enforcement & Case Law:**
- Market surveillance authority decisions
- Court of Justice of the EU (CJEU) — AI-related cases
- National court decisions on AI regulation
- Penalty decisions and enforcement actions

### Step 3: Update Files

Based on findings, update the relevant files:

| Change Type | Files to Update |
|-------------|----------------|
| New article interpretation | `SKILL.md`, relevant reference file |
| New deadline or date change | `SKILL.md` (Key Dates), `references/checklist.md` (timeline matrix) |
| New harmonized standard published | `references/standards-tracker.md` |
| New national implementation law | `references/national/{country}.md` |
| New enforcement action or penalty | `references/checklist.md` (if new requirement emerges), relevant sector file |
| Code of Practice update | `references/transparency-implementation.md`, `references/gpai-obligations.md` |
| New sector-specific guidance | Relevant `references/sectors/{sector}.md` |
| Provider policy change (Anthropic, OpenAI, etc.) | `references/provider-comparison.md` |
| New conformity assessment guidance | `references/conformity-assessment.md` |

### Step 4: Log Changes

After updating, add an entry to `CHANGELOG.md` with:
- Date
- What changed
- Source (URL or document reference)
- Which files were modified

### Step 5: Verify Consistency

After updates, verify:
- [ ] All dates are still correct across all files
- [ ] No contradictions between SKILL.md and reference files
- [ ] Article references still point to correct provisions
- [ ] National context files are consistent with EU-level content
- [ ] Code patterns still align with current best practices

## Update Schedule

| Period | Frequency | Why |
|--------|-----------|-----|
| **Now through Aug 2026** | **Monthly** | Pre-application phase: many guidelines, standards, and codes of practice being published |
| **Aug-Dec 2026** | **Bi-weekly** | First months of full application: enforcement posture becoming clear, early guidance |
| **2027 onwards** | **Quarterly** | Stable regime: focus on case law, new standards, and regulatory evolution |
| **On critical events** | **Immediately** | New harmonized standard published, major enforcement action, deadline change, CJEU ruling |

## Critical Events to Watch

These are the events that should trigger an immediate update:

1. **Harmonized standards publication** — When CEN/CENELEC JTC 21 publishes a standard referenced in the Official Journal, it becomes the presumption-of-conformity benchmark. This directly affects what "compliance" means in practice.

2. **Implementing acts adoption** — The Commission can adopt implementing acts specifying technical requirements. These are legally binding and override general guidance.

3. **First enforcement action** — The first penalty under Art. 99 will set the tone for enforcement across the EU. It will clarify what authorities actually prioritize.

4. **Transparency Code of Practice finalization** — Expected late 2026. This will standardize how synthetic content should be marked. Current patterns may need revision.

5. **National implementation laws** — Each member state must designate competent authorities and may add national-level requirements. These affect the `references/national/` files directly.

6. **AI provider policy changes** — If Anthropic, OpenAI, or other providers change their data processing policies, DPA terms, or EU data residency options, the `references/provider-comparison.md` needs updating.

7. **Major CJEU ruling on AI** — Any Court of Justice decision interpreting the AI Act creates binding precedent across all member states.

## Version Tracking

Verification status is tracked in **ONE place**: the root file [`LAST_VERIFIED.md`](/LAST_VERIFIED.md). It holds the global last-verified date, the sources checked, what changed, and the open verification loops.

Individual files do **not** carry their own date. Each points to the single source of truth with:

```markdown
<!-- Verification status: see LAST_VERIFIED.md -->
```

(National context files use a visible `**Verification status:** see [LAST_VERIFIED.md](...)` line instead of a comment.)

**When you update**: change the date and notes in `LAST_VERIFIED.md` only. Do **not** reintroduce per-file dates — that was the old model (v2.0) and it drifted out of sync. If a specific file was verified more or less deeply than the global pass, record that under "Verification depth" in `LAST_VERIFIED.md`.

## Changelog

### v2.1 — July 2026
- **Digital Omnibus on AI** (COM(2025) 836; adopted by Parliament 16 Jun 2026 and Council 29 Jun 2026 — final OJ reference/entry-into-force to be verified on EUR-Lex): postponed high-risk deadlines — Annex III standalone → 2 Dec 2027, Annex I regulated products → 2 Aug 2028, national sandboxes → 2 Aug 2027. Art. 50 transparency unchanged (2 Aug 2026); Art. 50(2) marking grace to 2 Dec 2026 for pre-existing systems
- Added two new Art. 5 prohibitions (non-consensual intimate imagery / "nudifiers", CSAM), effective Dec 2026
- **Transparency Code of Practice** (marking and labelling of AI-generated content) finalized 10 Jun 2026
- Draft **Art. 6 high-risk classification guidelines** published 19 May 2026 (consultation open to 23 Jul 2026, not yet adopted)
- Italy: **Legge n. 132/2025** in force since 10 Oct 2025 (AgID = notifying authority, ACN = market-surveillance authority)
- GPAI Code of Practice signatories recorded (Anthropic, OpenAI, Google, Microsoft, Mistral; Meta declined)
- Harmonized standards: still none cited in the Official Journal as of Jul 2026
- Refreshed stale model-name examples
- **Centralized verification tracking** into a single root file `LAST_VERIFIED.md`; per-file date headers replaced with `<!-- Verification status: see LAST_VERIFIED.md -->` pointers (one date to update instead of ~40)

### v2.0 — March 2026
- Complete restructure: English-first, national contexts separated
- Enhanced update workflow with source tracking and critical events
- Added standards tracker, provider comparison, incident response
- Expanded from 1 national context (Italy) to 5 (IT, DE, FR, ES, NL)
- Added sector-specific guides and framework code patterns

### v1.0 — March 2026
- Initial release
- Coverage: risk classification, Art. 50, Annex III, penalties
- Italian documentation templates
- Pre-deployment checklist
- Italian regulatory context (Garante, AgID, ACN)
