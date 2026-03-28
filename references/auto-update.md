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

Each file in this skill should include a comment or header indicating when it was last verified against the official regulatory text:

```markdown
<!-- Last verified against EUR-Lex: 2026-03-28 -->
```

When updating, refresh this date for every file you verify — even if no changes are needed. This tells users the content was checked, not just stale.

## Changelog

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
