# HR-tech — Hiring, Firing, and Everything In Between

Your AI just screened 10,000 CVs in 30 seconds. Impressive. It also just potentially discriminated against 10,000 people in 30 seconds. The AI Act would like a word.

Employment AI is the area where the EU AI Act's teeth are sharpest. Regulators are deeply suspicious of automated hiring, and with good reason — the history of AI in recruitment is a history of bias amplified at scale. Amazon's infamous recruiting tool that downgraded CVs containing the word "women's" was not an anomaly. It was a preview.

## What the AI Act Says About Employment AI

### Annex III, Category 4 — Employment, Workers Management, and Access to Self-Employment

The AI Act lists these HR use cases as high-risk:

1. **Recruitment and selection** — AI for placing targeted job advertisements, screening or filtering applications, evaluating candidates during interviews or tests
2. **Promotion and termination decisions** — AI making or influencing decisions about promotions, terminations, or contract endings
3. **Task allocation** — AI allocating tasks to workers based on individual behavior, personal traits, or characteristics
4. **Performance monitoring** — AI monitoring and evaluating the performance and behavior of workers in employment relationships

This is one of the broadest Annex III categories. It covers the entire employee lifecycle from job ad to exit interview.

## The Profiling Trap (Again, But Worse)

This deserves its own section because it is the single most important rule for HR-tech:

**If the system profiles individuals, the Art. 6(3) derogation does NOT apply. The system is ALWAYS high-risk.**

Now think about what HR-tech AI does. It evaluates candidates based on their skills, experience, education, personality traits, communication style. It monitors employee performance, productivity, engagement. It analyzes behavioral patterns to allocate tasks or predict attrition.

All of that is profiling. By definition.

The Art. 6(3) derogation — which allows some Annex III systems to be reclassified as not-high-risk if they perform narrow procedural tasks — is essentially unavailable for any HR AI system that evaluates individual people. Which is almost all of them.

If your HR AI system looks at individual humans and makes assessments about them, it is high-risk. Full stop. Plan accordingly.

## When HR-tech AI IS High-Risk

- **CV screening and filtering** — Any automated system that selects, ranks, or eliminates candidates
- **Automated interview scoring** — AI evaluating video interviews, analyzing speech patterns, facial expressions, or response content
- **Job ad targeting** — AI deciding which demographic groups see which job postings
- **Performance evaluation** — AI scoring employee performance, productivity metrics, engagement levels
- **Promotion recommendations** — AI suggesting or ranking employees for promotion
- **Termination risk scoring** — AI identifying employees "at risk" of underperformance or departure
- **Workforce monitoring** — Keystroke logging, screen monitoring, email analysis, location tracking analyzed by AI
- **Task allocation by behavior** — AI assigning tasks based on individual behavioral profiles or personality assessments
- **Sentiment analysis of employees** — AI analyzing employee communications to gauge morale or detect "problems"

## When HR-tech AI Is NOT High-Risk

The safe zone is narrow:

- **Meeting scheduling** — Calendar optimization, room booking
- **Expense reporting** — Automated expense categorization and policy checking
- **Internal knowledge search** — Search across company wikis and documents (not evaluating the searcher)
- **Payroll processing** — Automated calculations based on defined rules
- **Benefits administration** — Enrollment systems, eligibility calculators based on fixed criteria
- **Anonymous survey analysis** — Aggregated employee satisfaction data (truly anonymous, not individually attributable)
- **General HR chatbots** — Answering policy questions ("how many vacation days do I have?")

Notice the pattern: safe HR AI handles logistics and information. The moment it evaluates, ranks, scores, or profiles individual humans, it crosses into high-risk territory.

## Bias and Discrimination: The Highest-Scrutiny Area

HR AI is where regulators will look first for discriminatory outcomes. The reasons are obvious:

- **Training data reflects historical bias** — If your model learns from past hiring decisions made by humans, it learns their biases too. Every pattern of discrimination in your historical data becomes a pattern of discrimination in your AI.
- **Proxy discrimination is rampant** — You removed gender from the model? Great. But the AI can still discriminate via proxies: university name, zip code, hobbies, even writing style correlate with protected characteristics.
- **Scale amplifies harm** — A biased human recruiter might unfairly reject dozens of candidates. A biased AI rejects thousands before anyone notices.
- **Opacity hides the problem** — When a human says "I just didn't feel they were a good fit," at least you can investigate. When an AI outputs a score of 0.3, the discrimination is hidden behind mathematics.

### What Regulators Expect

Art. 10 (data governance) and Art. 9 (risk management) require proactive bias prevention:

- Regular bias audits across all protected characteristics (gender, age, race, ethnicity, disability, religion, sexual orientation)
- Testing for proxy discrimination (features correlated with protected characteristics)
- Documentation of bias testing methodology and results
- Mitigation measures when disparities are found
- Ongoing monitoring in production, not just pre-deployment testing

## GDPR Art. 22 — The Right to Not Be Decided by a Machine

Art. 22 gives individuals the right not to be subject to decisions based solely on automated processing that produce legal effects or similarly significant effects. Employment decisions clearly qualify.

This means:

- **No fully automated hiring decisions** — A human must meaningfully participate in the decision. "Click to approve the AI's recommendation" is not meaningful participation.
- **Right to explanation** — Candidates and employees have the right to understand the logic involved in automated decisions
- **Right to contest** — Individuals can challenge automated decisions and request human intervention
- **Suitable safeguards** — You must implement measures to safeguard individuals' rights, including the right to express their point of view

The practical implication: your AI can score, rank, and recommend. It cannot decide. And the human who decides must have genuine capacity to override, not just a rubber stamp.

## Works Councils and Trade Unions

This is the requirement most non-European HR-tech companies miss entirely.

In many EU member states, deploying AI in the workplace requires consultation with — or even approval from — employee representatives:

- **Germany**: The Works Council (Betriebsrat) has co-determination rights on many aspects of workplace technology deployment. Deploying AI monitoring tools without Works Council agreement can be illegal under the Works Constitution Act.
- **France**: The CSE (Comite Social et Economique) must be informed and consulted before introducing AI systems that affect working conditions.
- **Netherlands**: The Works Council has a right of consent for decisions on systems that monitor employee performance.
- **Italy**: Workers' Statute (Art. 4) restricts remote monitoring of workers. AI monitoring systems require trade union agreement or Labor Inspectorate authorization.
- **Spain**: The Workers' Statute requires informing workers' representatives about algorithmic decision-making parameters.

If you sell HR AI into the EU, your sales process needs to account for these requirements. Your customer's legal team will ask about them.

## Code Patterns for Compliant HR AI

### Bias Audit Logging

Every model evaluation must be auditable for bias analysis:

```python
from dataclasses import dataclass
from datetime import datetime, timezone
from typing import Any, Optional
import hashlib
import json

@dataclass(frozen=True)
class RecruitmentAuditEntry:
    """Immutable audit record for AI-assisted recruitment decisions."""
    entry_id: str
    timestamp: str
    job_posting_id: str
    candidate_id_hash: str
    model_version: str
    stage: str  # "cv_screening", "interview_scoring", "final_ranking"
    ai_score: float
    ai_recommendation: str  # "advance", "hold", "reject"
    score_factors: tuple[dict[str, Any], ...]  # Contributing factors
    demographic_category_hashes: tuple[str, ...]  # For bias analysis, hashed
    human_reviewer_id: Optional[str] = None
    human_decision: Optional[str] = None
    human_override: bool = False
    override_reason: Optional[str] = None

def create_recruitment_audit(
    entry_id: str,
    job_posting_id: str,
    candidate_id: str,
    model_version: str,
    stage: str,
    ai_score: float,
    ai_recommendation: str,
    score_factors: list[dict],
) -> RecruitmentAuditEntry:
    """Create immutable audit entry for a recruitment AI evaluation."""
    return RecruitmentAuditEntry(
        entry_id=entry_id,
        timestamp=datetime.now(timezone.utc).isoformat(),
        job_posting_id=job_posting_id,
        candidate_id_hash=hashlib.sha256(candidate_id.encode()).hexdigest(),
        model_version=model_version,
        stage=stage,
        ai_score=ai_score,
        ai_recommendation=ai_recommendation,
        score_factors=tuple(score_factors),
        demographic_category_hashes=(),
    )
```

### Candidate Data Minimization

Only process what you actually need. The temptation to feed everything into the model is strong. Resist it:

```python
@dataclass(frozen=True)
class MinimizedCandidateProfile:
    """Candidate profile stripped to job-relevant features only."""
    candidate_id_hash: str
    relevant_skills: tuple[str, ...]
    years_experience: Optional[int]
    education_level: Optional[str]  # Not institution name — that's a bias vector
    job_relevant_certifications: tuple[str, ...]
    excluded_fields: tuple[str, ...]  # Document what was intentionally dropped
    minimization_reason: str

# Fields that should NEVER reach the AI model
PROHIBITED_FIELDS = frozenset({
    "name", "gender", "age", "date_of_birth", "nationality",
    "ethnicity", "religion", "marital_status", "number_of_children",
    "photo", "address", "zip_code",  # Zip code is a proxy for ethnicity/income
    "hobbies",  # Often proxies for gender/cultural background
    "university_name",  # Proxy for socioeconomic background
})

def minimize_candidate_data(
    raw_profile: dict,
    job_relevant_fields: frozenset[str],
    candidate_id: str,
) -> MinimizedCandidateProfile:
    """Extract only job-relevant data. Drop everything that could introduce bias."""
    excluded = tuple(
        key for key in sorted(raw_profile.keys())
        if key in PROHIBITED_FIELDS or key not in job_relevant_fields
    )
    return MinimizedCandidateProfile(
        candidate_id_hash=hashlib.sha256(candidate_id.encode()).hexdigest(),
        relevant_skills=tuple(raw_profile.get("skills", [])),
        years_experience=raw_profile.get("years_experience"),
        education_level=raw_profile.get("education_level"),
        job_relevant_certifications=tuple(raw_profile.get("certifications", [])),
        excluded_fields=excluded,
        minimization_reason="AI Act Art. 10 data governance + bias prevention",
    )
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
    ai_score: float
    ai_explanation: str
    human_review_required: bool  # Always True
    minimum_review_time_seconds: int  # Prevent instant rubber-stamping
    review_started_at: Optional[str]
    review_completed_at: Optional[str]
    reviewer_id: Optional[str]
    reviewer_decision: Optional[str]
    reviewer_notes: Optional[str]  # Require substantive notes

def validate_review_quality(gate: HiringDecisionGate) -> tuple[bool, list[str]]:
    """Check whether the human review meets minimum quality standards."""
    issues = []
    if not gate.review_completed_at or not gate.review_started_at:
        issues.append("Review timestamps missing")
        return False, issues

    start = datetime.fromisoformat(gate.review_started_at)
    end = datetime.fromisoformat(gate.review_completed_at)
    elapsed = (end - start).total_seconds()

    if elapsed < gate.minimum_review_time_seconds:
        issues.append(
            f"Review completed in {elapsed:.0f}s, minimum is {gate.minimum_review_time_seconds}s. "
            "This suggests rubber-stamping rather than genuine review."
        )
    if not gate.reviewer_notes or len(gate.reviewer_notes.strip()) < 20:
        issues.append("Reviewer notes are missing or too brief for meaningful review")

    return len(issues) == 0, issues
```

## FRIA: Fundamental Rights of Workers

The Fundamental Rights Impact Assessment (Art. 27) for HR AI must specifically address:

1. **Right to non-discrimination** (Charter Art. 21) — The most critical right in hiring AI. Assess proxy discrimination, not just direct discrimination.
2. **Right to privacy** (Charter Art. 7) — Workplace monitoring AI intrudes on employee privacy. How much monitoring is proportionate?
3. **Right to data protection** (Charter Art. 8) — Employees' personal data must be processed lawfully, with clear purpose limitation.
4. **Freedom of expression** (Charter Art. 11) — Sentiment analysis of employee communications can chill free expression. If employees know the AI is reading their messages, they self-censor.
5. **Right to fair working conditions** (Charter Art. 31) — AI-driven task allocation and performance monitoring must not create inhumane working conditions (Amazon warehouse AI being the cautionary tale).
6. **Workers' right to information and consultation** (Charter Art. 27) — Workers have a right to be informed about AI systems that affect them.

## Compliance Checklist for HR-tech

- [ ] Accept that your HR AI is almost certainly high-risk (profiling individuals = no derogation)
- [ ] Implement full Art. 9-15 obligations: risk management, data governance, technical documentation, logging, transparency, human oversight, accuracy
- [ ] Build comprehensive bias audit framework covering all protected characteristics
- [ ] Remove or neutralize known bias proxies from training data
- [ ] Implement genuine human review with anti-rubber-stamping measures
- [ ] Provide clear explanations to candidates and employees about AI-assisted decisions
- [ ] Enable individuals to contest automated decisions (GDPR Art. 22)
- [ ] Document works council / trade union consultation requirements per target country
- [ ] Conduct FRIA with specific focus on worker rights
- [ ] Monitor for disparate impact in production, not just pre-deployment
- [ ] Register in the EU high-risk AI database (Art. 49)
- [ ] Prepare for the inevitable regulator inquiry — employment AI is priority enforcement territory
