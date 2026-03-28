# Healthtech — Where AI Act Meets Medical Device Regulation

You thought complying with one EU regulation was hard. In healthtech, your AI might need to satisfy the AI Act, the Medical Device Regulation, the IVDR, GDPR special category rules, and possibly national healthcare legislation — all at the same time. For the same system.

Nobody said building AI for healthcare would be simple. They just said it would be regulated.

## The Dual Regulation Problem

The AI Act does not replace existing sector-specific regulation. It stacks on top.

### The Three Layers

1. **Medical Device Regulation (MDR 2017/745)** — If your AI qualifies as a medical device (and most clinical AI does), you need CE marking, a notified body assessment, clinical evidence, and post-market surveillance.
2. **In Vitro Diagnostic Regulation (IVDR 2017/746)** — If your AI analyzes samples from the human body (lab results, genetic data, pathology images), IVDR applies instead of MDR.
3. **EU AI Act** — On top of whichever device regulation applies, the AI Act adds its own requirements.

Art. 6(1) says that if your AI is a safety component of a product regulated under Annex I legislation (which includes MDR and IVDR) and requires a third-party conformity assessment, it is automatically high-risk under the AI Act. No Annex III analysis needed.

The conformity assessment under MDR/IVDR is supposed to also cover the AI Act requirements. One notified body, one process. In practice, notified bodies are still figuring out how to integrate AI Act requirements into their MDR assessments.

## When Healthcare AI Is High-Risk

### Via Annex I (Safety Component of Regulated Product)

High-risk under Art. 6(1) if your AI is a medical device requiring third-party conformity assessment (MDR Classes IIa, IIb, III; IVDR Classes B, C, D). This covers: diagnostic algorithms, treatment recommendation engines, clinical decision support, AI imaging analysis, pathology classification.

### Via Annex III (Standalone)

Even if not a medical device, high-risk under Annex III if it performs triage, supports diagnostic decisions, or evaluates individual health risks.

### MDR Classification — Rule 11

Most AI software as a medical device (SaMD) falls under Rule 11:
- **Class IIa minimum** — Software providing information for diagnosis or therapeutic decisions
- **Class IIb** — Software monitoring vital processes where variations could cause immediate danger
- **Class III** — Software providing information directly determining patient treatment

Almost all clinical AI is at least Class IIa, meaning third-party assessment, meaning automatic high-risk under AI Act.

## When Healthcare AI Is NOT High-Risk

- **Wellness apps** — Fitness tracking, meditation, general health tips (not for diagnosis or treatment)
- **Appointment scheduling** — Clinic schedule optimization, patient flow management
- **Medical records search** — Text search in EHR systems (not interpreting clinical content)
- **Hospital logistics** — Supply chain, bed management, staffing prediction
- **Administrative coding** — Suggesting billing codes for human review (if genuinely preparatory)

But the line between "wellness" and "medical device" is notoriously blurry. If your wellness app claims it detects atrial fibrillation, you have crossed into MDR territory.

## Clinical Decision Support Classification

The key question: does the software provide information a clinician can independently review, or a recommendation the clinician would not reasonably reach alone?

- **Possibly not a medical device**: CDS retrieving patient-specific information from established literature/guidelines where the clinician can independently verify the basis
- **Likely a medical device**: CDS applying algorithms to patient data to generate novel diagnostic or treatment recommendations

If your CDS uses ML to output a risk score or diagnostic suggestion, it is almost certainly a medical device. "The doctor still decides" does not change the software's classification.

## GDPR Art. 9 — Health Data as Special Category

Health data gets the highest GDPR protection. Lawful processing requires:

- **Explicit consent** (Art. 9(2)(a)) — Freely given, specific, informed, unambiguous. In healthcare, "freely given" is complicated.
- **Healthcare provision** (Art. 9(2)(h)) — Necessary for medical diagnosis/treatment, under responsibility of a professional bound by secrecy.
- **Public health interest** (Art. 9(2)(i)) — For research and public health, with appropriate safeguards.

For AI training on health data: you need clear legal basis, data minimization, purpose limitation, and typically a DPIA.

## Notified Body Requirements

- **MDR CE marking**: Your AI as medical device needs CE marking through notified body assessment.
- **AI Act conformity**: For safety components of MDR products, AI Act conformity assessment integrates into MDR conformity assessment (Art. 43(1)).
- **In practice**: Expect notified body questions about risk management, data governance, bias testing, and human oversight that go beyond traditional MDR requirements.

## Code Patterns for Compliant Healthcare AI

### Patient Data Minimization

```python
@dataclass(frozen=True)
class MinimizedPatientRecord:
    """Patient record with only task-relevant features."""
    record_id_hash: str                          # Pseudonymized identifier
    clinical_features: tuple[tuple[str, Any], ...]  # Only task-relevant
    excluded_fields: tuple[str, ...]             # What was intentionally dropped
    minimization_policy_version: str
```

Build a `minimize_patient_record()` function that takes raw records and a `frozenset` of required features. Hash the patient ID, extract only required fields, and document excluded fields. Everything else is dropped before it reaches the model.

### Clinical Audit Logging

```python
@dataclass(frozen=True)
class ClinicalAIAuditEntry:
    """Immutable audit record for AI-assisted clinical decisions."""
    audit_id: str
    timestamp: str
    clinician_id: str                  # Who received the AI output
    patient_id_hash: str               # Pseudonymized
    system_id: str
    model_version: str
    intended_use: str                  # e.g., "chest_xray_triage"
    ai_output: dict[str, Any]          # The recommendation/classification
    confidence_score: float
    clinician_action: Optional[str] = None
    clinician_agreed_with_ai: Optional[bool] = None
    adverse_event_reported: bool = False
```

Log at the moment AI output is presented to the clinician. Update with clinician action after review. Track agreement rates — if clinicians always agree, they may not be exercising meaningful oversight.

### Human-in-the-Loop for Diagnosis

Art. 14 requires meaningful human oversight. Use an immutable `ClinicalOversightGate` pattern:

1. Create gate when AI produces diagnostic output — `review_completed = False`
2. Gate blocks the output from becoming actionable until a clinician reviews it
3. Clinician records decision: "accept", "modify", or "reject"
4. Return a new gate object (never mutate the original) with review details
5. Only "accept" or "modify" decisions allow the output to reach clinical workflows

The gate is not a suggestion. No clinical AI output should bypass it.

## DPIA Requirements for Health Data AI

When processing health data with AI, a Data Protection Impact Assessment is mandatory under GDPR Art. 35. This is separate from the AI Act's FRIA but overlaps:

1. **Systematic description** — What data, what processing, what purpose, what legal basis
2. **Necessity and proportionality** — Why AI? Why this data? Could you achieve the purpose with less?
3. **Risk assessment** — Re-identification risks, discrimination, incorrect diagnosis consequences
4. **Mitigation measures** — Pseudonymization, access controls, audit logging, human oversight, patient rights mechanisms

The DPIA must be completed before you begin processing. Not after. Not "when we get around to it."

## Practical Timeline

1. **Immediate**: Classify under both MDR/IVDR and AI Act
2. **Before deployment**: Complete DPIA, establish audit logging, implement human oversight
3. **At conformity assessment**: Demonstrate integrated compliance (MDR + AI Act)
4. **Ongoing**: Post-market surveillance, bias monitoring, incident reporting, periodic DPIA review

The healthcare sector has the least room for creative compliance interpretations. When your AI influences clinical decisions, regulators expect rigorous, documented, demonstrable compliance. Not a README that says "we take compliance seriously."
