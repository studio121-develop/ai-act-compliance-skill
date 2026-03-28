# Edtech — Teaching AI About the Rules (Ironic, Isn't It)

You built an AI that grades student essays. Or decides who gets into the university. Or monitors students during exams via webcam. Or recommends learning paths that determine whether a student advances to the next level.

The AI Act has opinions about all of this. Strong opinions. And because many of your users are children, so does the GDPR, the UN Convention on the Rights of the Child, and probably a few national education ministries whose regulations you have not read yet.

## What the AI Act Says About Education

### Annex III, Category 3 — Education and Vocational Training

The AI Act specifically flags these education use cases as high-risk:

1. **Admission decisions** — AI determining access to or admission into educational institutions at any level
2. **Exam and test scoring** — AI evaluating learning outcomes, including where those outcomes determine a student's progression
3. **Learning assessment** — AI assessing the appropriate level of education an individual should receive or be able to access
4. **Behavior monitoring** — AI monitoring and detecting prohibited behavior of students during tests and examinations (proctoring)

The common principle: if the AI's output affects a student's educational trajectory — their grades, their admission, their placement — it is high-risk.

## When Your Edtech AI IS High-Risk

Your system is almost certainly high-risk if it:

- **Scores exams or assessments** with results that affect student progression, graduation, or certification
- **Makes or informs admission decisions** at any educational level — primary school through university
- **Assigns learning levels or tracks** that determine what education a student can access
- **Monitors student behavior during exams** (AI proctoring) — webcam monitoring, keystroke analysis, screen recording with behavioral analysis
- **Evaluates teacher performance** if those evaluations affect employment decisions (this crosses into Annex III Category 4 — employment)

### AI Proctoring Deserves Special Attention

AI proctoring systems are high-risk under Annex III Category 3, and they also raise serious fundamental rights concerns:

- **Biometric processing** — Facial recognition, gaze tracking, and behavioral analysis may trigger Annex III Category 1 (biometrics)
- **Discrimination risk** — Proctoring AI has documented issues with false positives for students with disabilities, darker skin tones, non-standard home environments, and neurodivergent behaviors
- **Privacy invasion** — Monitoring students in their homes via webcam is a significant intrusion, especially for minors
- **Stress and anxiety** — The psychological impact of constant AI surveillance on test performance is real and documented

If you build proctoring AI, expect the highest level of regulatory scrutiny.

## When Your Edtech AI Is NOT High-Risk

Not all education AI triggers Annex III:

- **Content recommendation** — Suggesting additional reading, videos, or exercises without affecting formal assessment ("you might also like this lesson")
- **Tutoring chatbots** — Interactive learning assistants that help students understand material, as long as they do not produce consequential assessments
- **Administrative tools** — Scheduling, attendance tracking (without behavioral analysis), resource allocation
- **Language learning apps** — Vocabulary drills, pronunciation feedback, conversational practice (unless results count as formal certification)
- **Classroom engagement tools** — Polls, quizzes for engagement (not formal grading), collaborative whiteboards

### The Art. 6(3) Derogation for Tutoring AI

This is where it gets interesting. Art. 6(3) says an Annex III system is not high-risk if it performs a preparatory task or improves the result of a previously completed human activity. A tutoring AI that helps a student learn but does not itself produce the grade could potentially qualify for the derogation.

**However**: if the tutoring AI tracks student performance and that tracking feeds into formal assessment, the derogation argument weakens considerably. And if the system profiles individual students (adapting content based on behavioral patterns, learning style analysis, engagement metrics), the derogation does not apply at all — profiling always means high-risk.

The safe interpretation: if your adaptive learning system builds and maintains a profile of the individual student to personalize content, it profiles individuals, and the derogation is unavailable.

## Minors: The Extra Regulatory Layer

Most edtech serves children and teenagers. This triggers additional requirements that stack on top of the AI Act.

### GDPR Art. 8 — Conditions for Child Consent

- Children below 16 (or 13-16 depending on member state) cannot give valid consent to data processing themselves
- Parental consent is required for information society services offered directly to children
- The consent must be verifiable — "click here to confirm you are an adult" does not qualify
- Data minimization is especially critical when processing children's data

### UN Convention on the Rights of the Child

While not directly enforceable as EU regulation, it informs regulatory interpretation:

- **Best interests of the child** (Art. 3) — AI systems affecting children must prioritize their welfare
- **Right to education** (Art. 28) — AI should not create barriers to educational access
- **Right to privacy** (Art. 16) — Children have privacy rights that AI surveillance can violate
- **Right to be heard** (Art. 12) — Children should have age-appropriate ways to understand and contest AI decisions that affect them

### Age-Appropriate Design

The UK's Age Appropriate Design Code (not EU law, but influential) and similar emerging EU frameworks suggest:

- **Default to maximum privacy** for users under 18
- **No nudge techniques** that exploit children's developmental vulnerabilities
- **Transparent, age-appropriate explanations** of how AI works
- **No profiling** of children for commercial purposes (and be very careful about profiling for educational purposes)

## Code Patterns for Compliant Education AI

### Age Gating and Consent Flow

Before any AI processing of student data, verify age and obtain appropriate consent:

```python
from dataclasses import dataclass
from datetime import date, datetime, timezone
from typing import Optional

@dataclass(frozen=True)
class ConsentRecord:
    """Immutable record of consent status for a student user."""
    student_id_hash: str
    date_of_birth: date
    is_minor: bool
    member_state: str  # Consent age varies by country
    consent_age_threshold: int  # 13-16 depending on member state
    parental_consent_required: bool
    parental_consent_given: bool
    parent_email_hash: Optional[str]
    consent_timestamp: Optional[str]
    consent_scope: tuple[str, ...]  # What processing was consented to
    consent_version: str  # Track which consent text was shown

CONSENT_AGE_BY_COUNTRY = {
    "DE": 16, "FR": 15, "NL": 16, "IT": 14, "ES": 14,
    "BE": 13, "DK": 13, "SE": 13, "IE": 16, "PT": 13,
    "AT": 14, "PL": 16, "FI": 13, "EL": 15, "CZ": 15,
}
DEFAULT_CONSENT_AGE = 16  # GDPR default

def evaluate_consent_requirements(
    student_id_hash: str,
    date_of_birth: date,
    member_state: str,
    today: Optional[date] = None,
) -> ConsentRecord:
    """Determine consent requirements based on age and jurisdiction."""
    today = today or date.today()
    age = (today - date_of_birth).days // 365
    threshold = CONSENT_AGE_BY_COUNTRY.get(member_state, DEFAULT_CONSENT_AGE)
    is_minor = age < 18
    needs_parental_consent = age < threshold

    return ConsentRecord(
        student_id_hash=student_id_hash,
        date_of_birth=date_of_birth,
        is_minor=is_minor,
        member_state=member_state,
        consent_age_threshold=threshold,
        parental_consent_required=needs_parental_consent,
        parental_consent_given=False,  # Must be updated through verification flow
        parent_email_hash=None,
        consent_timestamp=None,
        consent_scope=(),
        consent_version="",
    )
```

### Teacher Review Gate for AI-Generated Assessments

Art. 14 human oversight, applied to education: a teacher must review AI-generated assessments before they affect student records:

```python
@dataclass(frozen=True)
class AssessmentReviewGate:
    """Ensures AI-generated assessment cannot affect records without teacher review."""
    gate_id: str
    student_id_hash: str
    assessment_type: str  # "essay_grade", "exam_score", "placement_recommendation"
    ai_generated_result: dict
    ai_confidence: float
    ai_explanation: str  # Why the AI reached this result
    teacher_review_required: bool  # Always True for consequential assessments
    teacher_id: Optional[str]
    teacher_reviewed: bool
    teacher_decision: Optional[str]  # "accept", "modify", "reject"
    teacher_modified_result: Optional[dict]
    review_timestamp: Optional[str]
    applied_to_record: bool  # Only True after teacher review

def create_assessment_gate(
    gate_id: str,
    student_id_hash: str,
    assessment_type: str,
    ai_result: dict,
    ai_confidence: float,
    ai_explanation: str,
) -> AssessmentReviewGate:
    """Create a review gate. Result is NOT applied until a teacher reviews it."""
    return AssessmentReviewGate(
        gate_id=gate_id,
        student_id_hash=student_id_hash,
        assessment_type=assessment_type,
        ai_generated_result=ai_result,
        ai_confidence=ai_confidence,
        ai_explanation=ai_explanation,
        teacher_review_required=True,
        teacher_id=None,
        teacher_reviewed=False,
        teacher_decision=None,
        teacher_modified_result=None,
        review_timestamp=None,
        applied_to_record=False,
    )

def submit_teacher_review(
    gate: AssessmentReviewGate,
    teacher_id: str,
    decision: str,
    modified_result: Optional[dict] = None,
) -> AssessmentReviewGate:
    """Record teacher review. Returns new immutable gate."""
    if decision not in ("accept", "modify", "reject"):
        raise ValueError(f"Invalid decision: {decision}")
    if decision == "modify" and modified_result is None:
        raise ValueError("Modified result required when decision is 'modify'")

    final_result = (
        modified_result if decision == "modify"
        else gate.ai_generated_result if decision == "accept"
        else None
    )
    return AssessmentReviewGate(
        gate_id=gate.gate_id,
        student_id_hash=gate.student_id_hash,
        assessment_type=gate.assessment_type,
        ai_generated_result=gate.ai_generated_result,
        ai_confidence=gate.ai_confidence,
        ai_explanation=gate.ai_explanation,
        teacher_review_required=gate.teacher_review_required,
        teacher_id=teacher_id,
        teacher_reviewed=True,
        teacher_decision=decision,
        teacher_modified_result=final_result,
        review_timestamp=datetime.now(timezone.utc).isoformat(),
        applied_to_record=decision in ("accept", "modify"),
    )
```

## National Education Regulations: The Wild Card

Education is primarily a national competence in the EU. This means:

- **Germany**: Each of the 16 Bundeslaender has its own education laws and data protection rules for schools. AI in Bavarian classrooms may face different requirements than AI in Berlin.
- **France**: The CNIL has issued specific guidance on AI in education. The Ministry of Education must approve digital tools used in public schools.
- **Italy**: The Garante per la protezione dei dati personali has been actively investigating AI proctoring and student surveillance.
- **Netherlands**: The AP (data protection authority) has taken a strict stance on student profiling.

There is no shortcut here. If you deploy edtech AI across multiple EU countries, you need to check national education regulations for each. The AI Act provides the floor, not the ceiling.

## Teacher Oversight: AI as Tool, Not Replacement

The AI Act's human oversight requirement (Art. 14) maps naturally onto education: the teacher is the human overseer. But this must be genuine:

- **Teachers must understand the AI** — Training on how the system works, its limitations, and when to override it
- **Teachers must have time to review** — If your system generates 200 AI grades and gives the teacher 10 minutes to review them all, that is not meaningful oversight
- **Teachers must be empowered to override** — The system must make it easy to modify or reject AI outputs, not just rubber-stamp them
- **Override patterns must be monitored** — If teachers override the AI 80% of the time, the system is not fit for purpose. If they override 0% of the time, they are not exercising oversight.

## Compliance Checklist for Edtech

- [ ] Classify every AI feature against Annex III Category 3
- [ ] Implement age verification and parental consent flows for minor users
- [ ] Build teacher review gates for all AI outputs that affect student records
- [ ] Conduct bias testing across demographic groups (age, gender, language background, disability)
- [ ] Provide age-appropriate transparency disclosures
- [ ] Default to maximum privacy settings for users under 18
- [ ] Check national education regulations for each deployment country
- [ ] Complete FRIA with specific attention to children's rights
- [ ] Implement data minimization — collect only what is needed for the specific educational purpose
- [ ] Plan for parental access requests and student data deletion
