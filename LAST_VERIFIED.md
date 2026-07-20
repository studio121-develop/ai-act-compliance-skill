# Verification Status — Single Source of Truth

> This file is the **single source of truth** for when this skill was last verified against
> the official regulatory sources. Individual files no longer carry their own verification
> date — they point here with `<!-- Verification status: see LAST_VERIFIED.md -->`.
>
> **When you run an update** (see `references/auto-update.md`), change the date and notes
> **here only**. Do not reintroduce per-file dates.

## Last verified: **2026-07-20**

Verified against primary EU / national sources:

- **EUR-Lex** — https://eur-lex.europa.eu
- **European Commission, DG CNECT** — https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai
- **Council of the EU** — https://www.consilium.europa.eu
- **European Parliament (legislative train)** — https://www.europarl.europa.eu/legislative-train
- **Gazzetta Ufficiale (Italy)** — https://www.gazzettaufficiale.it

## What changed at this verification (see CHANGELOG.md → v2.1.0)

- **Digital Omnibus on AI** (COM(2025) 836, procedure 2025/0359(COD)) — final approval by
  Parliament (16 Jun 2026) and Council (29 Jun 2026). Postpones high-risk deadlines:
  - Annex III stand-alone high-risk → **2 December 2027** (was 2 Aug 2026)
  - Annex I regulated-product high-risk → **2 August 2028** (was 2 Aug 2027)
  - National regulatory sandboxes → **2 August 2027** (was 2 Aug 2026)
- **Article 50 transparency — NOT postponed**, still applies from **2 August 2026**
  (watermarking grace for pre-existing systems to 2 December 2026).
- New Art. 5 prohibitions (non-consensual intimate imagery / CSAM) — effective **December 2026**.
- **Code of Practice on marking and labelling of AI-generated content** — finalized **10 June 2026**.
- Draft **Art. 6 high-risk classification guidelines** — published **19 May 2026**
  (consultation open to 23 July 2026; not yet adopted).
- No harmonized standards cited in the Official Journal yet (expected 2026).
- Italy: **Legge n. 132/2025** in force since **10 October 2025**.

## ⚠️ Open verification loops (resolve at next update)

1. **Digital Omnibus — final Official Journal reference and exact entry-into-force date were
   NOT confirmed** as of 2026-07-20. The skill hedges every affected date with
   "adopted, verify final OJ reference on EUR-Lex." Once published, confirm the regulation
   number and entry-into-force date and remove the hedges.
2. **Harmonized standards** — watch for the first CEN/CENELEC standards cited in the OJ
   (presumption of conformity). Update `references/standards-tracker.md`.
3. **Art. 6 high-risk guidelines** — watch for the final adopted version.
4. **First enforcement actions / penalties** under Art. 99.

## Verification depth (honesty note)

Files substantively re-verified against sources on 2026-07-20: `SKILL.md`, `README.md`,
`CHANGELOG.md`, and the deadline/date-bearing references (`checklist.md`,
`decision-trees/risk-classification.md`, `regulatory-sandbox.md`, `standards-tracker.md`,
`transparency-implementation.md`, `high-risk-requirements.md`, `gpai-obligations.md`,
`provider-comparison.md`, `auto-update.md`, `national/*`, `sectors/fintech.md`).

Other files (code patterns, remaining sector guides, templates) were **reviewed for stale
regulatory-date claims and found current**, but not re-read line-by-line against the full
regulation. Treat their guidance as of the date above.
