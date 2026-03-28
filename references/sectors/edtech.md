<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Edtech — Teaching AI About the Rules (Ironic, Isn't It)

> **Disclaimer**: This document provides general guidance — not legal advice. See [LEGAL_NOTICE.md](/LEGAL_NOTICE.md) for full terms.

You built an AI that grades student essays. Or decides who gets into university. Or monitors students during exams via webcam. The AI Act has opinions about all of this. Strong opinions. And because many of your users are children, so does the GDPR, the UN Convention on the Rights of the Child, and probably a few national education ministries whose regulations you have not read yet.

## What the AI Act Says About Education

### Annex III, Category 3 — Education and Vocational Training

These education use cases are high-risk:

1. **Admission decisions** — AI determining access to educational institutions at any level
2. **Exam and test scoring** — AI evaluating learning outcomes where those outcomes affect progression
3. **Learning assessment** — AI assessing the appropriate level of education an individual should receive
4. **Behavior monitoring** — AI detecting prohibited behavior during tests (proctoring)

The principle: if the AI's output affects a student's educational trajectory, it is high-risk.

## When Your Edtech AI IS High-Risk

- **Exam scoring** with results that affect progression, graduation, or certification
- **Admission decisions** at any educational level
- **Learning level assignment** that determines what education a student can access
- **AI proctoring** — webcam monitoring, keystroke analysis, behavioral analysis during exams
- **Teacher performance evaluation** if those evaluations affect employment (crosses into Annex III Category 4)

### AI Proctoring Deserves Special Attention

Proctoring systems are high-risk under Category 3, and they also raise serious fundamental rights concerns:

- **Biometric processing** — Facial recognition, gaze tracking may trigger Category 1 (biometrics)
- **Discrimination** — Documented false positives for students with disabilities, darker skin tones, neurodivergent behaviors
- **Privacy invasion** — Monitoring students (often minors) in their homes via webcam
- **Psychological impact** — Constant AI surveillance affects test performance

If you build proctoring AI, expect the highest level of regulatory scrutiny.

## When Your Edtech AI Is NOT High-Risk

- **Content recommendation** — Suggesting additional materials without affecting formal assessment
- **Tutoring chatbots** — Interactive learning assistants that do not produce consequential assessments
- **Administrative tools** — Scheduling, attendance tracking (without behavioral analysis)
- **Language learning apps** — Vocabulary drills, pronunciation feedback (unless results count as certification)
- **Classroom engagement** — Polls, informal quizzes, collaborative tools

### Art. 6(3) Derogation for Tutoring AI

A tutoring AI that helps a student learn but does not itself produce the grade could qualify for the derogation — it performs a preparatory task and the teacher evaluates.

**However**: if the tutoring AI tracks student performance and that tracking feeds into formal assessment, the derogation weakens. And if the system profiles individual students (adapting content based on behavioral patterns, learning style analysis), the derogation does not apply at all — profiling always means high-risk.

## Minors: The Extra Regulatory Layer

### GDPR Art. 8 — Child Consent

- Children below 16 (or 13-16 depending on member state) cannot give valid consent themselves
- Parental consent required for information society services directed at children
- Consent must be verifiable — "click to confirm you are an adult" does not qualify
- Data minimization is especially critical for children's data

### UN Convention on the Rights of the Child

Informs regulatory interpretation:
- **Best interests of the child** (Art. 3) — AI must prioritize children's welfare
- **Right to education** (Art. 28) — AI should not create barriers to access
- **Right to privacy** (Art. 16) — AI surveillance can violate children's privacy rights
- **Right to be heard** (Art. 12) — Age-appropriate ways to understand and contest AI decisions

### Age-Appropriate Design

Emerging EU frameworks suggest:
- Default to maximum privacy for users under 18
- No nudge techniques exploiting developmental vulnerabilities
- Transparent, age-appropriate explanations of how AI works
- No profiling of children for commercial purposes

## Code Patterns for Compliant Education AI

### Age Gating and Consent Flow

```python
CONSENT_AGE_BY_COUNTRY = {
    "DE": 16, "FR": 15, "NL": 16, "IT": 14, "ES": 14,
    "BE": 13, "DK": 13, "SE": 13, "IE": 16, "PT": 13,
    "AT": 14, "PL": 16, "FI": 13, "EL": 15, "CZ": 15,
}

@dataclass(frozen=True)
class ConsentRecord:
    """Immutable record of consent status for a student user."""
    student_id_hash: str
    is_minor: bool
    member_state: str
    consent_age_threshold: int
    parental_consent_required: bool
    parental_consent_given: bool
    consent_timestamp: Optional[str]
    consent_scope: tuple[str, ...]      # What processing was consented to
    consent_version: str                # Which consent text was shown
```

Compute `consent_age_threshold` from the country map (default 16). Calculate age from date of birth, determine whether parental consent is needed, and block AI processing until consent requirements are satisfied. The consent record is immutable — any change creates a new record.

### Teacher Review Gate for AI Assessments

```python
@dataclass(frozen=True)
class AssessmentReviewGate:
    """AI assessment cannot affect records without teacher review."""
    gate_id: str
    student_id_hash: str
    assessment_type: str            # "essay_grade", "exam_score", "placement"
    ai_generated_result: dict
    ai_confidence: float
    ai_explanation: str
    teacher_review_required: bool   # Always True for consequential assessments
    teacher_reviewed: bool
    teacher_decision: Optional[str] # "accept", "modify", "reject"
    applied_to_record: bool         # Only True after teacher review
```

Create the gate when AI produces an assessment. The gate blocks application to student records until a teacher reviews. The teacher can accept, modify, or reject. Only accepted or modified results are applied. Return new immutable objects on every state change.

## National Education Regulations: The Wild Card

Education is primarily a national competence in the EU:

- **Germany**: Each of 16 Bundeslaender has its own education and data protection rules for schools
- **France**: CNIL has specific guidance on AI in education; Ministry must approve digital tools in public schools
- **Italy**: The Garante has investigated AI proctoring and student surveillance
- **Netherlands**: AP has taken a strict stance on student profiling

If you deploy across multiple EU countries, check national education regulations for each. The AI Act is the floor, not the ceiling.

## Teacher Oversight: AI as Tool, Not Replacement

Art. 14 human oversight maps naturally to education — the teacher is the overseer. But it must be genuine:

- **Teachers must understand the AI** — Training on how it works, its limitations, when to override
- **Teachers must have time to review** — 200 AI grades with 10 minutes to review is not meaningful oversight
- **Teachers must be empowered to override** — Make it easy to modify or reject AI outputs
- **Override patterns must be monitored** — 0% override rate means oversight is not happening

## Compliance Checklist for Edtech

- [ ] Classify every AI feature against Annex III Category 3
- [ ] Implement age verification and parental consent flows for minors
- [ ] Build teacher review gates for all AI outputs affecting student records
- [ ] Conduct bias testing across demographic groups (age, gender, language, disability)
- [ ] Provide age-appropriate transparency disclosures
- [ ] Default to maximum privacy for users under 18
- [ ] Check national education regulations for each deployment country
- [ ] Complete FRIA with specific attention to children's rights
- [ ] Implement data minimization — collect only what is needed
- [ ] Plan for parental access requests and student data deletion
