<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Fintech — When Your AI Starts Making Money Decisions

> **Disclaimer**: This document provides general guidance — not legal advice. See [LEGAL_NOTICE.md](/LEGAL_NOTICE.md) for full terms.

Your AI just denied someone a loan. Or priced their insurance at triple the average. Or flagged their account for fraud and froze it over the weekend. Welcome to the most scrutinized intersection of AI and regulation in the EU.

Financial services were already one of the most regulated sectors in Europe before the AI Act showed up. Now you get to comply with both. Congratulations.

## What the AI Act Says About Financial AI

### Annex III, Category 5 — Essential Private and Public Services

The AI Act lists these financial use cases as high-risk:

1. **Creditworthiness assessment** — AI evaluating credit scores or creditworthiness of natural persons
2. **Insurance risk assessment and pricing** — AI for risk assessment and pricing in life and health insurance
3. **Emergency services dispatch** — AI evaluating and classifying emergency calls (relevant for insurance call centers)
4. **Social benefits eligibility** — AI evaluating eligibility for public benefits (relevant for public-sector fintech)

The common thread: decisions that directly affect someone's access to money, credit, or essential services.

## When Your Fintech AI IS High-Risk

Your system is almost certainly high-risk if it:

- **Scores creditworthiness** — Any model outputting a credit score or lending recommendation used in actual decisions
- **Prices insurance using personal data** — Life or health premiums calculated by AI based on individual risk profiles
- **Makes account access decisions** — Fraud detection that can freeze accounts or block transactions
- **Determines benefits eligibility** — AI deciding who qualifies for financial assistance
- **Profiles individuals** — Any system evaluating aspects of a person's financial behavior or economic situation

### The Profiling Trap

Under Art. 6(3), a derogation can reclassify Annex III systems as not-high-risk for narrow procedural or preparatory tasks. But:

**If the system profiles individuals, the Art. 6(3) derogation does NOT apply. Ever.**

Credit scoring is profiling by definition. So is insurance risk assessment on personal data. So is behavioral fraud detection that builds user profiles. If your AI evaluates a natural person to predict their financial behavior — you are profiling, you are high-risk. No escape hatch.

## When Your Fintech AI is NOT High-Risk

- **Internal fraud detection** — Flagging patterns for human analysts, without directly affecting customer access
- **Market analytics** — Analyzing trends, stock movements, macroeconomic indicators (no individual profiling)
- **Customer support chatbots** — Standard automation (still requires Art. 50 transparency disclosure)
- **AML/KYC document verification** — Automated checks where a human makes the final decision
- **Portfolio analytics** — Tools analyzing performance without making allocation decisions

Be careful with "preparatory task" arguments. If your fraud flag automatically freezes an account before a human reviews it, that is not preparatory — that is the decision itself.

## The Regulatory Stack: AI Act + Everything Else

### PSD2 (Payment Services Directive 2)
- Strong Customer Authentication already requires explainable risk assessment
- AI-based fraud detection must not undermine the right to payment services
- Account blocking must follow PSD2 notification requirements even when AI-triggered

### MiFID II
- If your AI recommends investments, suitability requirements apply ON TOP of AI Act obligations
- Best execution obligations still apply when AI routes orders

### CRD/CRR
- AI credit risk models must satisfy banking regulation model validation AND AI Act requirements
- ECB/SSM model governance expectations overlap significantly with Art. 9 risk management

### Consumer Credit Directive (revised 2023)
- Borrowers have a right to explanation of credit decisions — aligns with AI Act Art. 13
- Explicitly addresses automated decision-making in creditworthiness assessments

### ECB and EBA Guidance
- ECB guidance on AI/ML in credit institutions emphasizes model governance, validation, and human oversight
- EBA guidelines require AI models to be explainable and auditable
- These overlap with AI Act requirements but are not identical — satisfy both

## Code Patterns for Compliant Financial AI

### Audit Trail for Credit Decisions

```python
@dataclass(frozen=True)
class CreditDecisionAuditEntry:
    """Immutable audit record for AI-assisted credit decisions."""
    decision_id: str
    timestamp: str
    applicant_id_hash: str       # Never store raw PII in audit logs
    model_version: str
    model_inputs_hash: str       # Hash of input features, not raw data
    input_feature_names: tuple[str, ...]
    risk_score: float
    decision: str                # "approved", "denied", "referred_to_human"
    confidence: float
    explanation_factors: tuple[dict[str, Any], ...]
    human_reviewer_id: Optional[str] = None
    human_override: bool = False
    human_override_reason: Optional[str] = None
```

### Explainability Hooks

Art. 13 requires deployers to interpret system output. For credit models, provide feature attribution:

```python
@dataclass(frozen=True)
class ExplainabilityReport:
    """Human-readable explanation of a credit decision."""
    decision_id: str
    summary: str                         # Plain-language summary
    top_factors: tuple[dict, ...]        # Ranked contributing factors
    counterfactuals: tuple[str, ...]     # What would change the outcome
    model_confidence: float
    data_quality_warnings: tuple[str, ...]
```

Sort factors by absolute impact, generate counterfactual statements for negative contributors ("If X improved, the score would change by approximately Y"), and always include data quality warnings. The applicant's right to explanation under the Consumer Credit Directive maps directly to this output.

### Bias Monitoring

Art. 10 data governance requires monitoring for discriminatory outcomes. Track approval rates across protected groups and compute disparate impact ratios using the four-fifths rule (threshold 0.80). Store results as immutable `BiasMetrics` snapshots with flagged disparities. Run this continuously in production, not just at validation time.

## FRIA Considerations for Financial Services

A Fundamental Rights Impact Assessment is mandatory for high-risk financial AI (Art. 27). Focus on:

1. **Right to non-discrimination** (Charter Art. 21) — Credit scoring and insurance pricing are prime vectors for proxy discrimination. Does your model penalize protected groups through correlated features (zip code as proxy for ethnicity)?
2. **Right to an effective remedy** (Charter Art. 47) — If your AI denies credit, the applicant must have a meaningful path to contest. "The algorithm said no" is not a remedy.
3. **Right to social security** (Charter Art. 34) — Denial of essential financial services can exclude people from economic participation.
4. **Right to consumer protection** (Charter Art. 38) — AI pricing must not exploit behavioral vulnerabilities.

## Art. 6(3) Derogation Analysis

| Use Case | Derogation? | Reasoning |
|---|---|---|
| Internal fraud analytics dashboard | Yes | Preparatory task, human analyst decides |
| AML pattern detection (flagging only) | Possibly | If genuinely preparatory and human reviews all flags |
| Credit scoring model | **No** | Profiles individuals — derogation excluded |
| Insurance risk pricing | **No** | Profiles individuals based on personal characteristics |
| Automated account freeze on fraud | **No** | Not preparatory — it IS the consequential action |
| Market trend analysis | N/A | Not in Annex III at all |
| Customer segmentation for marketing | **No** | Profiles individuals — derogation excluded |

The moment your AI evaluates individual people to predict their financial behavior, you are profiling and high-risk. In fintech, the derogation covers a narrow category.

## Timeline Considerations

The AI Act's high-risk obligations applied from August 2, 2026 for new systems. Existing fintech AI systems already on the market need to demonstrate compliance at the next significant modification or when the transitional period ends. Financial regulators (ECB, national competent authorities) are expected to coordinate with AI Act market surveillance authorities, meaning you may face inquiries from both sides.

If you are building a new credit scoring or insurance pricing system today: design for compliance from the start. Retrofitting explainability, audit logging, and bias monitoring into a production system is significantly more expensive than building it in. The architecture decisions you make now will determine whether compliance is a minor tax or a major rewrite.

## Practical Compliance Checklist

- [ ] Classify every AI component against Annex III Category 5
- [ ] If high-risk: implement full Art. 9-15 obligations
- [ ] Map AI Act requirements against existing financial regulation (PSD2, MiFID II, CRD/CRR)
- [ ] Implement audit logging for all AI-assisted financial decisions
- [ ] Deploy bias monitoring with regular reporting cadence
- [ ] Build explainability into credit models from day one (retrofitting is painful)
- [ ] Conduct FRIA before deployment, update annually or on significant model changes
- [ ] Establish human oversight mechanisms that are genuine, not rubber-stamp
- [ ] Register in the EU high-risk AI database (Art. 49)
- [ ] Prepare for financial regulator inquiries — they will come
