# Healthtech — Where AI Act Meets Medical Device Regulation

You thought complying with one EU regulation was hard. In healthtech, your AI might need to satisfy the AI Act, the Medical Device Regulation, the IVDR, GDPR special category rules, and possibly national healthcare legislation — all at the same time. For the same system. With different notified bodies potentially involved.

Nobody said building AI for healthcare would be simple. They just said it would be regulated.

## The Dual Regulation Problem

Here is the fundamental challenge: the AI Act does not replace existing sector-specific regulation. It stacks on top of it.

### The Three Layers

1. **Medical Device Regulation (MDR 2017/745)** — If your AI qualifies as a medical device (and most clinical AI does), you need CE marking under MDR, a notified body assessment, clinical evidence, and post-market surveillance.
2. **In Vitro Diagnostic Regulation (IVDR 2017/746)** — If your AI analyzes samples from the human body (lab results, genetic data, pathology images), IVDR applies instead of MDR.
3. **EU AI Act** — On top of whichever device regulation applies, the AI Act adds its own requirements for high-risk systems.

The silver lining: Art. 6(1) says that if your AI system is already a safety component of a product regulated under Annex I legislation (which includes MDR and IVDR), and it requires a third-party conformity assessment under that legislation, then it is automatically high-risk under the AI Act. No Annex III analysis needed. You already know what you are dealing with.

The less-silver lining: you now have two sets of requirements to satisfy, and the conformity assessment under MDR/IVDR is supposed to also cover the AI Act requirements. In theory, one notified body, one process. In practice, notified bodies are still figuring out how to integrate AI Act requirements into their MDR assessments.

## When Healthcare AI Is High-Risk

### Via Annex I (Safety Component of Regulated Product)

Your AI is high-risk under Art. 6(1) if it is:
- A medical device or component of a medical device under MDR
- An in vitro diagnostic or component thereof under IVDR
- And requires third-party conformity assessment (Classes IIa, IIb, III under MDR; Classes B, C, D under IVDR)

This covers most clinical AI: diagnostic algorithms, treatment recommendation engines, clinical decision support that influences clinical outcomes, AI-powered imaging analysis, pathology classification systems.

### Via Annex III (Standalone Classification)

Even if your system is not a medical device, it can be high-risk under Annex III if it:
- Performs triage or prioritization of patients for emergency care
- Supports diagnostic decisions in clinical settings
- Evaluates health risks for individuals

### MDR Classification for AI Software — Rule 11

Most AI-based software as a medical device (SaMD) falls under MDR Rule 11:

- **Class IIa minimum** — Software intended to provide information used to take decisions with diagnosis or therapeutic purposes
- **Class IIb** — Software intended to monitor vital physiological processes where variations could result in immediate danger
- **Class III** — Software intended to provide information used for decisions with diagnosis or therapeutic purposes that directly determine the patient's treatment

The practical effect: almost all clinical AI software is at least Class IIa, which means third-party notified body assessment, which means automatic high-risk under the AI Act.

## When Healthcare AI Is NOT High-Risk

Some healthcare-adjacent AI avoids both MDR and high-risk AI Act classification:

- **Wellness apps** — Fitness tracking, meditation guidance, general health tips (not intended for diagnosis or treatment)
- **Appointment scheduling** — Optimizing clinic schedules, patient flow management
- **Medical records search** — Text search and retrieval in EHR systems (not interpreting or analyzing clinical content)
- **Hospital logistics** — Supply chain optimization, bed management, staffing prediction
- **Administrative coding** — Suggesting medical billing codes for human review (if genuinely preparatory)
- **Medical education** — Training simulations, educational content delivery

But the line between "wellness" and "medical device" is notoriously blurry. If your wellness app starts claiming it can detect atrial fibrillation, you have crossed into MDR territory whether you intended to or not.

## Clinical Decision Support Classification

CDS systems sit in a particularly tricky regulatory grey zone. The key question: does the software provide information that a clinician can independently review, or does it provide a recommendation that the clinician would not reasonably reach independently?

- **Not a medical device (possibly)**: CDS that retrieves patient-specific information from established medical literature, guidelines, or the patient's own record — where the clinician can independently verify the basis
- **Medical device (likely)**: CDS that applies algorithms to patient data to generate novel diagnostic or treatment recommendations that the clinician could not independently derive from the raw data

If your CDS uses machine learning to analyze patient data and output a risk score or diagnostic suggestion, it is almost certainly a medical device. The "the doctor still decides" argument does not change the classification of the software itself.

## GDPR Art. 9 — Health Data as Special Category

Health data gets the highest protection under GDPR. Processing it requires:

- **Explicit consent** (Art. 9(2)(a)) — Must be freely given, specific, informed, and unambiguous. In healthcare contexts, "freely given" is complicated because patients may feel they cannot refuse.
- **Necessary for healthcare provision** (Art. 9(2)(h)) — Processing necessary for medical diagnosis, treatment, or health system management, under the responsibility of a professional bound by professional secrecy.
- **Public interest in public health** (Art. 9(2)(i)) — For research and public health purposes, with appropriate safeguards.

For AI training on health data, the legal basis matters enormously. Training a model on patient data requires clear legal basis, data minimization, purpose limitation, and typically a Data Protection Impact Assessment.

## Notified Body Requirements: Two CE Marks?

Not exactly two CE marks, but the interaction is complex:

- **MDR CE marking**: Your AI as a medical device needs CE marking through a notified body assessment under MDR. The notified body evaluates safety, performance, and clinical evidence.
- **AI Act conformity**: For AI systems that are safety components of MDR products, the AI Act conformity assessment is integrated into the MDR conformity assessment (Art. 43(1)). The same notified body should assess both.
- **In practice**: Notified bodies are still building competence in AI-specific requirements. Expect questions about your risk management system, data governance, bias testing, and human oversight mechanisms that go beyond traditional MDR requirements.

The timeline matters: AI Act obligations for high-risk systems in Annex I products applied from August 2, 2026. If your medical AI device was already on the market, you need to demonstrate compliance at the next conformity assessment or significant device modification.

## Code Patterns for Compliant Healthcare AI

### Patient Data Minimization

Art. 10 of the AI Act requires appropriate data governance. Combined with GDPR's data minimization principle, healthcare AI must be aggressive about reducing data exposure:

```python
from dataclasses import dataclass, field
from typing import Any, Optional
import hashlib

@dataclass(frozen=True)
class MinimizedPatientRecord:
    """Patient record with only features needed for the specific AI task."""
    record_id_hash: str  # Pseudonymized identifier
    clinical_features: tuple[tuple[str, Any], ...]  # Only task-relevant features
    excluded_fields: tuple[str, ...]  # Document what was intentionally excluded
    minimization_policy_version: str

def minimize_patient_record(
    raw_record: dict,
    required_features: frozenset[str],
    policy_version: str,
) -> MinimizedPatientRecord:
    """Extract only the features required for the AI task. Everything else is dropped."""
    patient_id = raw_record.get("patient_id", "")
    id_hash = hashlib.sha256(patient_id.encode()).hexdigest()

    included = tuple(
        (key, raw_record[key]) for key in sorted(required_features) if key in raw_record
    )
    excluded = tuple(
        key for key in sorted(raw_record.keys())
        if key not in required_features and key != "patient_id"
    )
    return MinimizedPatientRecord(
        record_id_hash=id_hash,
        clinical_features=included,
        excluded_fields=excluded,
        minimization_policy_version=policy_version,
    )
```

### Clinical Audit Logging

Every AI-assisted clinical decision must be auditable — both for AI Act Art. 12 and for medical device post-market surveillance:

```python
from dataclasses import dataclass
from datetime import datetime, timezone
from typing import Any, Optional

@dataclass(frozen=True)
class ClinicalAIAuditEntry:
    """Immutable audit record for AI-assisted clinical decisions."""
    audit_id: str
    timestamp: str
    session_id: str
    clinician_id: str  # Who received the AI output
    patient_id_hash: str  # Pseudonymized
    system_id: str
    model_version: str
    intended_use: str  # e.g., "chest_xray_triage", "sepsis_risk_screening"
    ai_output: dict[str, Any]  # The system's recommendation/classification
    confidence_score: float
    clinician_action: Optional[str] = None  # What the clinician actually did
    clinician_agreed_with_ai: Optional[bool] = None
    clinician_override_reason: Optional[str] = None
    adverse_event_reported: bool = False

def log_clinical_ai_interaction(
    audit_id: str,
    session_id: str,
    clinician_id: str,
    patient_id: str,
    system_id: str,
    model_version: str,
    intended_use: str,
    ai_output: dict[str, Any],
    confidence_score: float,
) -> ClinicalAIAuditEntry:
    """Create immutable audit entry at the moment AI output is presented to clinician."""
    return ClinicalAIAuditEntry(
        audit_id=audit_id,
        timestamp=datetime.now(timezone.utc).isoformat(),
        session_id=session_id,
        clinician_id=clinician_id,
        patient_id_hash=hashlib.sha256(patient_id.encode()).hexdigest(),
        system_id=system_id,
        model_version=model_version,
        intended_use=intended_use,
        ai_output=ai_output,
        confidence_score=confidence_score,
    )
```

### Human-in-the-Loop for Diagnosis

Art. 14 requires meaningful human oversight. In clinical AI, "meaningful" means the clinician can actually understand and override the AI:

```python
@dataclass(frozen=True)
class ClinicalOversightGate:
    """Enforces human review before AI diagnostic output becomes actionable."""
    gate_id: str
    ai_recommendation: dict[str, Any]
    requires_clinician_review: bool  # Always True for diagnostic AI
    review_completed: bool
    clinician_id: Optional[str]
    review_timestamp: Optional[str]
    clinician_decision: Optional[str]  # "accept", "modify", "reject"

def create_oversight_gate(
    gate_id: str,
    ai_recommendation: dict[str, Any],
) -> ClinicalOversightGate:
    """Create an oversight gate. Output is NOT actionable until reviewed."""
    return ClinicalOversightGate(
        gate_id=gate_id,
        ai_recommendation=ai_recommendation,
        requires_clinician_review=True,
        review_completed=False,
        clinician_id=None,
        review_timestamp=None,
        clinician_decision=None,
    )

def complete_oversight_review(
    gate: ClinicalOversightGate,
    clinician_id: str,
    decision: str,
) -> ClinicalOversightGate:
    """Record clinician review. Returns new immutable gate — never mutate the original."""
    if decision not in ("accept", "modify", "reject"):
        raise ValueError(f"Invalid decision: {decision}. Must be accept, modify, or reject.")
    return ClinicalOversightGate(
        gate_id=gate.gate_id,
        ai_recommendation=gate.ai_recommendation,
        requires_clinician_review=gate.requires_clinician_review,
        review_completed=True,
        clinician_id=clinician_id,
        review_timestamp=datetime.now(timezone.utc).isoformat(),
        clinician_decision=decision,
    )
```

## DPIA Requirements for Health Data AI

When you process health data (GDPR Art. 9 special category) using AI, a Data Protection Impact Assessment is mandatory under GDPR Art. 35. This is separate from the AI Act's FRIA but overlaps substantially:

1. **Systematic description** — What data, what processing, what purpose, what legal basis
2. **Necessity and proportionality** — Why AI? Why this data? Could you achieve the purpose with less?
3. **Risk assessment** — Risks to patients' rights and freedoms (re-identification, discrimination, incorrect diagnosis)
4. **Mitigation measures** — Pseudonymization, access controls, audit logging, human oversight, patient rights mechanisms

The DPIA should be completed before you begin processing. Not after. Not "when we get around to it." Before.

## Practical Timeline and Priority

1. **Immediate**: Classify your AI system under both MDR/IVDR and AI Act
2. **Before deployment**: Complete DPIA, establish audit logging, implement human oversight
3. **At conformity assessment**: Demonstrate integrated compliance (MDR + AI Act)
4. **Ongoing**: Post-market surveillance, bias monitoring, incident reporting, periodic DPIA review

The healthcare sector has the least room for creative compliance interpretations. When your AI can influence clinical decisions, regulators expect rigorous, documented, demonstrable compliance. Not a README that says "we take compliance seriously."
