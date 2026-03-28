<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Compliance Scoring Methodology

A structured approach to measuring how compliant your AI system is with the EU AI Act. Use this to track progress, identify gaps, and prioritize remediation.

> **Disclaimer**: This scoring system is an informal assessment tool. A perfect score does not guarantee legal compliance. A low score does not necessarily mean you're non-compliant — it depends on your specific obligations.

## How It Works

1. Determine your risk classification (use `references/decision-trees/risk-classification.md`)
2. Answer the applicable checklist items below
3. Each item is weighted by legal obligation and severity
4. Calculate your score as a percentage

## Scoring Weights

| Weight | Meaning | What happens if you skip it |
|--------|---------|----------------------------|
| **BLOCKER (10 pts)** | Legally mandatory, enforceable, with penalties | Regulatory risk — potential fines |
| **REQUIRED (5 pts)** | Legally required or strongly implied by the regulation | Compliance gap — likely flagged in audit |
| **RECOMMENDED (2 pts)** | Best practice, good faith compliance, defensive measure | Not penalized, but weakens your position |
| **BONUS (1 pt)** | Above and beyond — competitive advantage | No negative consequence |

## Score Card: ALL AI Systems

These apply regardless of risk classification. Max: 30 points.

| # | Item | Weight | Status |
|---|------|--------|--------|
| A1 | AI literacy training documented for team (Art. 4) | REQUIRED (5) | [ ] |
| A2 | AI system inventory/registry maintained | RECOMMENDED (2) | [ ] |
| A3 | Risk classification documented with rationale | REQUIRED (5) | [ ] |
| A4 | Prohibited practices check completed (Art. 5) | BLOCKER (10) | [ ] |
| A5 | Compliance contact person designated | RECOMMENDED (2) | [ ] |
| A6 | Quarterly compliance review scheduled | RECOMMENDED (2) | [ ] |
| A7 | DPA with AI model provider in place | REQUIRED (5) | [ ] |

## Score Card: LIMITED RISK (Art. 50)

Add these if your system has transparency obligations. Max: 70 points.

| # | Item | Weight | Status |
|---|------|--------|--------|
| L1 | AI interaction disclosure visible in UI (Art. 50.1) | BLOCKER (10) | [ ] |
| L2 | Disclosure shown before/at first interaction | REQUIRED (5) | [ ] |
| L3 | Disclosure accessible on all devices (mobile, desktop) | REQUIRED (5) | [ ] |
| L4 | Disclosure accessible to screen readers (WCAG) | RECOMMENDED (2) | [ ] |
| L5 | AI-generated content marked machine-readable (Art. 50.2) | BLOCKER (10) | [ ] |
| L6 | Visible AI label on generated content | REQUIRED (5) | [ ] |
| L7 | Deepfake disclosure implemented (if applicable) (Art. 50.4) | BLOCKER (10) | [ ] |
| L8 | Public interest text disclosure (if applicable) (Art. 50.4) | BLOCKER (10) | [ ] |
| L9 | Privacy policy includes AI addendum | REQUIRED (5) | [ ] |
| L10 | Terms of service updated with AI usage | REQUIRED (5) | [ ] |
| L11 | AI_ACT_COMPLIANCE.md in project root | RECOMMENDED (2) | [ ] |
| L12 | Human oversight mechanism (kill switch) | REQUIRED (5) | [ ] |
| L13 | Error handling for AI failures | RECOMMENDED (2) | [ ] |
| L14 | AI interaction logging enabled | RECOMMENDED (2) | [ ] |
| L15 | Rate limiting and abuse prevention | RECOMMENDED (2) | [ ] |
| L16 | Incident response plan documented | RECOMMENDED (2) | [ ] |
| L17 | Data minimization verified | REQUIRED (5) | [ ] |
| L18 | User consent mechanism in place | REQUIRED (5) | [ ] |
| L19 | Content marking tested end-to-end | RECOMMENDED (2) | [ ] |
| L20 | Compliance checks in CI/CD pipeline | BONUS (1) | [ ] |

## Score Card: HIGH-RISK (Arts. 9-17)

Add these on top of ALL + LIMITED RISK items. Max: 120 points.

| # | Item | Weight | Status |
|---|------|--------|--------|
| H1 | Risk management system established (Art. 9) | BLOCKER (10) | [ ] |
| H2 | Risk assessment documented | BLOCKER (10) | [ ] |
| H3 | Risk mitigation measures implemented | REQUIRED (5) | [ ] |
| H4 | Data governance practices documented (Art. 10) | REQUIRED (5) | [ ] |
| H5 | Bias examination performed | REQUIRED (5) | [ ] |
| H6 | Technical documentation per Annex IV (Art. 11) | BLOCKER (10) | [ ] |
| H7 | Automatic event logging enabled (Art. 12) | BLOCKER (10) | [ ] |
| H8 | Instructions for deployers provided (Art. 13) | BLOCKER (10) | [ ] |
| H9 | Human oversight measures designed (Art. 14) | BLOCKER (10) | [ ] |
| H10 | Accuracy levels declared (Art. 15) | REQUIRED (5) | [ ] |
| H11 | Robustness tested | REQUIRED (5) | [ ] |
| H12 | Cybersecurity measures implemented (Art. 15) | REQUIRED (5) | [ ] |
| H13 | Quality management system documented (Art. 17) | BLOCKER (10) | [ ] |
| H14 | Conformity assessment completed | BLOCKER (10) | [ ] |
| H15 | CE marking affixed | BLOCKER (10) | [ ] |
| H16 | EU database registration completed (Art. 71) | BLOCKER (10) | [ ] |
| H17 | Post-market monitoring system in place (Art. 72) | REQUIRED (5) | [ ] |
| H18 | Serious incident reporting procedure defined (Art. 73) | REQUIRED (5) | [ ] |
| H19 | FRIA completed (if deployers required) (Art. 27) | REQUIRED (5) | [ ] |
| H20 | Deployer instructions include all Art. 13 elements | REQUIRED (5) | [ ] |

## Calculating Your Score

### Step 1: Determine applicable items

- **Minimal risk**: Only ALL items (A1-A7)
- **Limited risk**: ALL items (A1-A7) + LIMITED items (L1-L20)
- **High-risk**: ALL items (A1-A7) + LIMITED items (L1-L20) + HIGH items (H1-H20)

### Step 2: Calculate

```
Score = (points achieved / total applicable points) × 100
```

### Step 3: Interpret

| Score | Status | Interpretation |
|-------|--------|---------------|
| 90-100% | Green | Well-prepared for compliance. Address remaining items for completeness |
| 70-89% | Yellow | Good foundation but gaps remain. Prioritize BLOCKER items |
| 50-69% | Orange | Significant gaps. Focus on BLOCKER and REQUIRED items immediately |
| Below 50% | Red | Major compliance work needed. Start with Art. 5 check and risk classification |

### Step 4: Check for blockers

**Regardless of your percentage score**, any unchecked BLOCKER item means you have a critical compliance gap. A system with 85% score but a missing BLOCKER is in worse shape than one with 70% and all BLOCKERs checked.

## Tracking Over Time

Re-run this score card:
- After every major release with AI features
- Quarterly as part of compliance review
- After regulatory updates (new standards, guidance, or enforcement actions)
- When adding new AI features (they may change your risk level)

Keep a log:

```markdown
## Compliance Score History
| Date | Classification | Score | Blockers Open | Notes |
|------|---------------|-------|---------------|-------|
| 2026-03-28 | Limited | 45% | 3 | Initial assessment |
| 2026-05-15 | Limited | 72% | 0 | Implemented Art. 50 measures |
| 2026-07-30 | Limited | 88% | 0 | Pre-deadline review |
```

## Generating a Report

Ask Claude:
```
Generate a compliance score report for my project
```

This will produce a structured report suitable for management review or audit preparation. See `references/templates/compliance-report.md` for the report template.
