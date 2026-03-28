<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Harmonized Standards Tracker — What's Coming and When

> **Disclaimer**: This document provides general guidance — not legal advice. See [LEGAL_NOTICE.md](/LEGAL_NOTICE.md) for full terms.

> Standards are the unsung heroes of regulation. Nobody reads them for fun,
> but everyone benefits when they exist. Think of them as the cheat codes
> for compliance — follow the standard, get the presumption of conformity. Nice deal.

This reference tracks the harmonized and relevant international standards for
AI Act compliance, their development status, and how they map to specific
obligations.

---

## What Harmonized Standards Are (and Why You Should Care)

Under the EU's New Legislative Framework, **harmonized standards** are technical
standards developed by European Standards Organizations (CEN, CENELEC, ETSI) at
the request of the European Commission.

The magic property: if you comply with a harmonized standard that covers a
specific AI Act requirement, you get a **presumption of conformity** for that
requirement (Art. 40). This means the burden of proof shifts — the authority must
demonstrate non-compliance rather than you proving compliance.

Without harmonized standards, you must demonstrate compliance through other means
(common specifications, internal evidence, third-party audits). Doable, but more
work and more uncertainty.

**Current status**: The Commission has issued a standardization request to
CEN/CENELEC. Standards are in development but most are not yet published.
This is the awkward period where obligations apply but the easy path to
demonstrating compliance doesn't fully exist yet.

---

## CEN/CENELEC JTC 21 — The Main Event

**Joint Technical Committee 21 (JTC 21)** on Artificial Intelligence is the
primary body developing harmonized standards for the AI Act.

Work programme overview:

| Working Group | Focus Area | AI Act Articles |
|---------------|-----------|-----------------|
| WG 1 | Foundational concepts & terminology | Cross-cutting |
| WG 2 | Risk management | Art. 9 |
| WG 3 | Data governance & quality | Art. 10 |
| WG 4 | Transparency & information | Art. 13 |
| WG 5 | Human oversight | Art. 14 |
| WG 6 | Robustness, accuracy, cybersecurity | Art. 15 |
| WG 7 | AI management system | Art. 17 |

---

## Key Standards in Development

### Risk Management (Art. 9)

**Standard**: prEN — AI Risk Management
**Maps to**: Art. 9 (Risk management system for high-risk AI)

Covers: Establishing, implementing, documenting, and maintaining a risk management
system throughout the AI system lifecycle. Identification and analysis of known and
reasonably foreseeable risks. Estimation and evaluation of risks. Risk treatment
measures. Residual risk assessment.

**What to do now**: Implement risk management based on ISO/IEC 23894 (see below) and
align with ISO 31000 principles. When the harmonized standard publishes, gap-analyze
and adapt.

### Data Governance (Art. 10)

**Standard**: prEN — Data Quality for AI
**Maps to**: Art. 10 (Data and data governance)

Covers: Training, validation, and testing data governance practices. Data quality
criteria (relevance, representativeness, completeness, correctness). Bias detection
and mitigation in datasets. Statistical properties examination. Data collection
processes and documentation.

**What to do now**: Document your data pipelines, quality checks, and bias
assessments. Maintain data provenance records. This is one area where "we use a
third-party API" does not exempt you from understanding the data.

### Technical Documentation (Art. 11)

**Standard**: prEN — Technical Documentation for AI
**Maps to**: Art. 11 (Technical documentation)

Covers: Structure and content of technical documentation. System description,
design specifications, development methodology, validation and testing procedures,
risk management documentation, change management records.

**What to do now**: Start with the Annex IV requirements of the AI Act and build your
documentation template. A harmonized standard will formalize the format, but the
content requirements are already clear.

### Record-Keeping / Logging (Art. 12)

**Standard**: prEN — Logging and Audit Trails for AI
**Maps to**: Art. 12 (Record-keeping)

Covers: Automatic logging capabilities. What events to log, retention periods,
traceability requirements. Ensuring logs enable post-market monitoring and incident
investigation.

**What to do now**: Implement structured logging for all AI interactions — inputs,
outputs, model version, timestamps, user identifiers (pseudonymized). Retain logs
for the period appropriate to your risk level.

### Transparency (Art. 13)

**Standard**: prEN — Transparency of AI Systems
**Maps to**: Art. 13 (Transparency and provision of information to deployers)

Covers: Information to be provided to deployers. Instructions for use. Performance
metrics and known limitations. Intended purpose specification. Human oversight
instructions.

**What to do now**: Write clear deployer documentation. If you are both provider and
deployer (common in SaaS), document for your own operational teams.

### Human Oversight (Art. 14)

**Standard**: prEN — Human Oversight of AI Systems
**Maps to**: Art. 14 (Human oversight)

Covers: Design for human oversight. Mechanisms for human intervention, correction,
and override. Human-machine interface requirements. Competence requirements for
oversight personnel.

**What to do now**: Define who oversees the system, what tools they have to intervene,
and what training they need. Implement a kill switch or override mechanism.

### Accuracy, Robustness, Cybersecurity (Art. 15)

**Standard**: prEN — Accuracy, Robustness and Cybersecurity of AI
**Maps to**: Art. 15 (Accuracy, robustness, and cybersecurity)

Covers: Accuracy metrics and testing. Robustness against errors, faults, and
adversarial attacks. Cybersecurity measures specific to AI (model poisoning,
evasion attacks, data extraction). Resilience and fallback mechanisms.

**What to do now**: Define and measure your accuracy metrics. Test for adversarial
robustness. Apply standard cybersecurity practices plus AI-specific protections.

### Quality Management (Art. 17)

**Standard**: prEN — Quality Management for AI
**Maps to**: Art. 17 (Quality management system)

Covers: Quality management system requirements specific to AI. Procedures for
development, quality control, and quality assurance. Change management. Continuous
improvement processes.

**What to do now**: If you have ISO 9001, extend it for AI. If you don't, implement
a quality management system that covers the Art. 17 requirements.

---

## Relevant International Standards

These are not harmonized standards (no automatic presumption of conformity) but
provide excellent frameworks and may be referenced by future harmonized standards.

### ISO/IEC 42001 — AI Management System

The "ISO 27001 of AI." Specifies requirements for establishing, implementing,
maintaining, and improving an AI management system. Certifiable. Probably the
single most useful standard to adopt right now if you want a structured approach
to AI governance.

### ISO/IEC 23894 — AI Risk Management

Guidance on managing risk specifically for AI systems. Extends ISO 31000 risk
management principles to AI contexts. Covers the full risk management process
from identification through treatment and monitoring.

### ISO/IEC 24029 — Assessment of Robustness of Neural Networks

Technical standard for assessing the robustness of neural networks. Covers formal
methods, statistical testing, and robustness metrics. Useful for Art. 15 compliance
evidence.

### ISO/IEC 25059 — AI Engineering Lifecycle (SQuaRE Series)

Part of the Software Quality Requirements and Evaluation (SQuaRE) series, adapted
for AI. Defines quality models, measures, and evaluation criteria specific to AI
and machine learning systems.

---

## ETSI Standards

The European Telecommunications Standards Institute (ETSI) has its own AI
standardization work through the **Securing AI (SAI)** group:

| Standard | Title | Relevance |
|----------|-------|-----------|
| ETSI GR SAI 001 | AI Threat Ontology | Threat modeling for AI systems |
| ETSI GR SAI 002 | Data Supply Chain Security | Data governance, supply chain |
| ETSI GR SAI 004 | Problem Statement on AI Security | General AI security concerns |
| ETSI GR SAI 005 | Mitigation Strategy Report | Security mitigation approaches |
| ETSI GR SAI 006 | Role of Hardware in AI Security | Hardware-level protections |

These are Group Reports (informational), not harmonized standards, but they provide
useful technical guidance especially for cybersecurity aspects of Art. 15.

---

## C2PA — Content Provenance Standard

**Coalition for Content Provenance and Authenticity (C2PA)** defines a standard for
certifying the provenance of digital content. Relevant to:

- **Art. 50(2)**: Providers of AI systems generating synthetic content must mark
  outputs in a machine-readable format using suitable technical means (including
  C2PA or equivalent).
- **GPAI obligations**: Model providers must support downstream marking of
  AI-generated content.

C2PA is not an EU harmonized standard but is the leading technical solution for
content provenance. If your system generates images, audio, or video, C2PA
compliance is effectively table stakes.

---

## Timeline — Expected Publication Dates

| Standard Area | Expected Draft | Expected Publication |
|---------------|---------------|---------------------|
| Risk management | 2025 Q4 | 2026 Q2–Q3 |
| Data governance | 2025 Q4 | 2026 Q2–Q3 |
| Technical documentation | 2026 Q1 | 2026 Q3–Q4 |
| Logging / record-keeping | 2026 Q1 | 2026 Q3–Q4 |
| Transparency | 2026 Q1 | 2026 Q3 |
| Human oversight | 2026 Q1 | 2026 Q3–Q4 |
| Accuracy/robustness/security | 2026 Q2 | 2026 Q4–2027 Q1 |
| Quality management | 2026 Q1 | 2026 Q3 |

**Caveat**: Standards development timelines are aspirational. Delays are the norm,
not the exception. Plan accordingly.

---

## Practical Guidance

You don't need to wait for harmonized standards to be compliant. The AI Act obligations
exist independently of the standards. Standards just give you the *easy* path to
demonstrating conformity.

**What to do right now**:

1. **Adopt ISO/IEC 42001** as your AI management framework. It covers most of the
   structural requirements.
2. **Use ISO/IEC 23894** for risk management until the harmonized standard publishes.
3. **Follow the AI Act text directly** (Annex IV for documentation, Art. 9-15 for
   technical requirements) and document your compliance evidence.
4. **Track JTC 21 progress** so you can align early when drafts become available.
5. **Participate in standards development** if you can — you'll get early access to
   drafts and can influence the outcome.

---

## How to Track Standards Development

- **CEN/CENELEC JTC 21**: [cencenelec.eu](https://www.cencenelec.eu/) — Look for JTC 21 work programme updates
- **ISO/IEC JTC 1/SC 42**: [iso.org/committee/6794475](https://www.iso.org/committee/6794475.html) — AI standards committee
- **ETSI SAI**: [etsi.org/technologies/securing-artificial-intelligence](https://www.etsi.org/technologies/securing-artificial-intelligence)
- **EU AI Office**: Official communications on harmonized standards requests and citations
- **EU Official Journal**: Where harmonized standard references are formally published
- **C2PA**: [c2pa.org](https://c2pa.org/) — Content provenance standard updates

Subscribe to CEN/CENELEC and ISO newsletters for the relevant committees. The EU AI
Office also publishes updates on standardization progress. If you rely on a consultant
or law firm for regulatory intelligence, make sure AI Act standards tracking is in scope.
