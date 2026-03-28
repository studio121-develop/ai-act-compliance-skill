# HR-tech — Hiring, Firing, and Everything In Between

Your AI just screened 10,000 CVs in 30 seconds. Impressive. It also just potentially discriminated against 10,000 people in 30 seconds. The AI Act would like a word.

Employment AI is where the AI Act's teeth are sharpest. Regulators are deeply suspicious of automated hiring, and with reason — the history of AI in recruitment is a history of bias amplified at scale. Amazon's infamous recruiting tool that downgraded CVs containing the word "women's" was not an anomaly. It was a preview.

## What the AI Act Says About Employment AI

### Annex III, Category 4 — Employment, Workers Management, and Access to Self-Employment

High-risk use cases:

1. **Recruitment and selection** — AI for targeted job ads, screening/filtering applications, evaluating candidates
2. **Promotion and termination** — AI making or influencing promotion, termination, or contract decisions
3. **Task allocation** — AI allocating tasks based on individual behavior, traits, or characteristics
4. **Performance monitoring** — AI monitoring and evaluating worker performance and behavior

This covers the entire employee lifecycle from job ad to exit interview.

## The Profiling Trap (But Worse)

**CRITICAL: If the system profiles individuals, the Art. 6(3) derogation does NOT apply. Always high-risk.**

Think about what HR-tech AI does. It evaluates candidates on skills, experience, personality. It monitors employee performance, productivity, engagement. It analyzes behavioral patterns for task allocation or attrition prediction.

All of that is profiling. By definition. The Art. 6(3) derogation is essentially unavailable for any HR AI that evaluates individual people. Which is almost all of them. If your HR AI looks at individual humans and makes assessments, it is high-risk. Full stop.

## When HR-tech AI IS High-Risk

- **CV screening and filtering** — Any system that selects, ranks, or eliminates candidates
- **Automated interview scoring** — AI evaluating video interviews, speech patterns, response content
- **Job ad targeting** — AI deciding which demographics see which postings
- **Performance evaluation** — AI scoring productivity, engagement, performance
- **Promotion recommendations** — AI ranking employees for promotion
- **Workforce monitoring** — Keystroke logging, screen monitoring, email analysis by AI
- **Task allocation by behavior** — AI assigning tasks based on behavioral profiles
- **Sentiment analysis of employees** — AI analyzing communications to gauge morale

## When HR-tech AI Is NOT High-Risk

The safe zone is narrow:

- **Meeting scheduling** — Calendar optimization, room booking
- **Expense reporting** — Automated categorization and policy checking
- **Internal knowledge search** — Searching company wikis (not evaluating the searcher)
- **Payroll processing** — Automated calculations based on defined rules
- **Benefits administration** — Enrollment and eligibility based on fixed criteria
- **Anonymous survey analysis** — Truly anonymous aggregated satisfaction data
- **HR chatbots** — Answering policy questions ("how many vacation days do I have?")

The pattern: safe HR AI handles logistics and information. The moment it evaluates, ranks, or profiles individuals, it is high-risk.

## Bias and Discrimination: Highest-Scrutiny Area

HR AI is where regulators look first for discriminatory outcomes:

- **Training data reflects historical bias** — Your model learns from past human decisions, including their biases
- **Proxy discrimination** — You removed gender? Great. University name, zip code, hobbies, writing style still correlate with protected characteristics
- **Scale amplifies harm** — A biased human rejects dozens. A biased AI rejects thousands before anyone notices.
- **Opacity hides the problem** — When an AI outputs a score of 0.3, discrimination hides behind mathematics

Art. 10 and Art. 9 require proactive prevention: regular bias audits across all protected characteristics, proxy discrimination testing, documented methodology and results, mitigation measures, and ongoing production monitoring.

## GDPR Art. 22 — The Right to Not Be Decided by a Machine

Art. 22 gives individuals the right not to be subject to decisions based solely on automated processing with legal or significant effects. Employment decisions clearly qualify:

- **No fully automated hiring decisions** — A human must meaningfully participate. "Click to approve" is not meaningful.
- **Right to explanation** — Candidates and employees can demand the logic behind automated decisions
- **Right to contest** — Individuals can challenge decisions and request human intervention
- **Suitable safeguards** — Including the right to express their point of view

Your AI can score, rank, and recommend. It cannot decide. The human who decides must genuinely be able to override.

## Works Councils and Trade Unions

The requirement most non-European HR-tech companies miss entirely.

- **Germany**: The Betriebsrat has co-determination rights on workplace technology. Deploying AI monitoring without agreement can be illegal under the Works Constitution Act.
- **France**: The CSE must be consulted before introducing AI affecting working conditions.
- **Netherlands**: Works Council has consent rights for employee performance monitoring systems.
- **Italy**: Workers' Statute (Art. 4) restricts remote monitoring. AI systems need trade union agreement or Labor Inspectorate authorization.
- **Spain**: Workers' Statute requires informing representatives about algorithmic decision-making parameters.

Your sales process needs to account for these. Your customer's legal team will ask.

## Code Patterns for Compliant HR AI

### Candidate Data Minimization

```python
PROHIBITED_FIELDS = frozenset({
    "name", "gender", "age", "date_of_birth", "nationality",
    "ethnicity", "religion", "marital_status", "number_of_children",
    "photo", "address", "zip_code",       # Proxy for ethnicity/income
    "hobbies",                             # Proxy for gender/culture
    "university_name",                     # Proxy for socioeconomic background
})

@dataclass(frozen=True)
class MinimizedCandidateProfile:
    """Candidate profile stripped to job-relevant features only."""
    candidate_id_hash: str
    relevant_skills: tuple[str, ...]
    years_experience: Optional[int]
    education_level: Optional[str]        # Not institution name
    job_relevant_certifications: tuple[str, ...]
    excluded_fields: tuple[str, ...]      # Document what was dropped
```

Extract only job-relevant data. Drop everything in `PROHIBITED_FIELDS` before it reaches the model. Document what was excluded and why. The temptation to feed everything into the model is strong. Resist it.

### Bias Audit Logging

```python
@dataclass(frozen=True)
class RecruitmentAuditEntry:
    """Immutable audit record for AI-assisted recruitment."""
    entry_id: str
    timestamp: str
    job_posting_id: str
    candidate_id_hash: str
    model_version: str
    stage: str                    # "cv_screening", "interview_scoring", "ranking"
    ai_score: float
    ai_recommendation: str        # "advance", "hold", "reject"
    score_factors: tuple[dict, ...]
    human_reviewer_id: Optional[str] = None
    human_decision: Optional[str] = None
    human_override: bool = False
```

### Human Review Enforcement

The human decision-maker must be real, not a fiction:

```python
@dataclass(frozen=True)
class HiringDecisionGate:
    """Enforces genuine human review before any hiring action."""
    gate_id: str
    candidate_id_hash: str
    ai_recommendation: str
    ai_explanation: str
    minimum_review_time_seconds: int  # Prevent instant rubber-stamping
    review_started_at: Optional[str]
    review_completed_at: Optional[str]
    reviewer_notes: Optional[str]     # Require substantive notes
```

Validate review quality: if elapsed time is below minimum or reviewer notes are missing/too brief, flag it as potential rubber-stamping. This is not about bureaucracy — it is about proving to regulators that human oversight is genuine.

## FRIA: Fundamental Rights of Workers

Art. 27 FRIA for HR AI must address:

1. **Non-discrimination** (Charter Art. 21) — Assess proxy discrimination, not just direct
2. **Privacy** (Charter Art. 7) — How much workplace monitoring is proportionate?
3. **Data protection** (Charter Art. 8) — Lawful processing with clear purpose limitation
4. **Freedom of expression** (Charter Art. 11) — Sentiment analysis chills free expression
5. **Fair working conditions** (Charter Art. 31) — AI task allocation must not create inhumane conditions
6. **Information and consultation** (Charter Art. 27) — Workers have a right to know about AI affecting them

## Compliance Checklist

- [ ] Accept that your HR AI is almost certainly high-risk (profiling = no derogation)
- [ ] Implement full Art. 9-15 obligations
- [ ] Build comprehensive bias audit framework across all protected characteristics
- [ ] Remove or neutralize known bias proxies from training data
- [ ] Implement genuine human review with anti-rubber-stamping measures
- [ ] Provide clear explanations to candidates and employees about AI decisions
- [ ] Enable individuals to contest automated decisions (GDPR Art. 22)
- [ ] Document works council/trade union requirements per target country
- [ ] Conduct FRIA focused on worker rights
- [ ] Monitor for disparate impact in production, not just pre-deployment
- [ ] Register in the EU high-risk AI database (Art. 49)
