# Technical Documentation Template (Annex IV)

This is the full technical documentation template required for **high-risk AI systems**
under Annex IV of the AI Act (Regulation (EU) 2024/1689). Every high-risk AI system must
have this documentation drawn up before being placed on the market or put into service
(Art. 11(1)).

This template is more detailed than a general compliance checklist. It follows the exact
structure of Annex IV, with fill-in fields and explanatory guidance for each section.
Maintain this as a living document — Art. 11(2) requires it to be kept up to date
throughout the system's lifecycle.

---

## How to Use This Template

1. Copy this template into your compliance documentation system
2. Replace all `[FILL IN]` placeholders with your system-specific information
3. Remove the guidance comments (in parentheses) once the section is complete
4. Review with your legal and technical teams
5. Update upon any significant modification (Art. 11(2))
6. Retain for **10 years** after the system is placed on the market (Art. 18(1))

---

## SECTION (a): General Description of the AI System

*Annex IV, Section 1(a): A general description of the AI system.*

### a.1 System Identification

```
System Name:           [FILL IN]
Version:               [FILL IN]
Date of Documentation: [FILL IN]
Provider Name:         [FILL IN]
Provider Address:      [FILL IN]
Provider Contact:      [FILL IN — name, email, phone]
Authorized Rep (if non-EU): [FILL IN — name, address, mandate reference]
```

### a.2 Intended Purpose

```
Intended Purpose:      [FILL IN — describe the specific purpose as precisely as possible.
                        This defines the scope of your conformity assessment. Example:
                        "Automated screening of job applications to rank candidates by
                        predicted suitability for the advertised role, intended for use
                        by HR professionals as a decision-support tool."]

Annex III Category:    [FILL IN — specify which point of Annex III classifies this system
                        as high-risk. Example: "Annex III, point 4(a) — AI systems used
                        for recruitment or selection of natural persons"]

Intended Users:        [FILL IN — describe the deployers/end users. Example:
                        "HR departments of enterprise organizations with 50+ employees"]

Intended Context:      [FILL IN — geographic scope, sector, operating environment.
                        Example: "EU market, all sectors, integrated into existing ATS
                        (Applicant Tracking System) platforms via API"]
```

### a.3 Interaction with Hardware and Software

```
Hardware Requirements: [FILL IN — minimum infrastructure specs, cloud requirements]

Software Dependencies: [FILL IN — operating systems, frameworks, libraries, APIs.
                        Include versions where relevant]

Integration Points:    [FILL IN — how the system connects to other systems.
                        Example: "REST API integration with third-party ATS platforms;
                        receives candidate data in JSON format, returns ranked list
                        with confidence scores"]

Network Requirements:  [FILL IN — connectivity, bandwidth, latency constraints]
```

### a.4 Versions and History

```
Current Version:       [FILL IN]
Previous Versions:     [FILL IN — list major versions with dates and key changes]
Version Changelog:     [FILL IN — reference to version control system or changelog doc]
```

(Guidance: Recital 69 notes that the general description should enable competent
authorities to understand the system's basic character and identify the provider.)

---

## SECTION (b): Detailed Description of System Elements

*Annex IV, Section 1(b): A detailed description of the elements of the AI system and of
the process for its development.*

### b.1 Development Process

```
Development Methodology: [FILL IN — e.g., Agile, Waterfall, MLOps pipeline.
                          Describe the end-to-end process from problem definition
                          to deployment]

Development Team:        [FILL IN — team composition, relevant expertise,
                          organizational structure]

Development Timeline:    [FILL IN — key milestones from inception to current version]

Quality Assurance:       [FILL IN — testing protocols, code review processes,
                          validation procedures applied during development]
```

### b.2 System Architecture

```
Architecture Overview:   [FILL IN — high-level description of system components.
                          Include a diagram reference if available]

AI Model(s) Used:        [FILL IN — for each model:
                          - Model type (e.g., transformer, CNN, decision tree)
                          - Model source (proprietary, open-source, API-based)
                          - If GPAI model: provider name, model identifier, version
                          - Training approach (supervised, unsupervised, RL, fine-tuned)]

Processing Pipeline:     [FILL IN — describe the data flow from input to output.
                          Example: "Input text → preprocessing (tokenization,
                          normalization) → embedding → model inference → post-processing
                          (threshold application, ranking) → output"]

Third-Party Components:  [FILL IN — list all third-party AI components, APIs, or
                          models integrated into the system, with version numbers
                          and provider names]
```

### b.3 Algorithmic Details

```
Core Algorithm(s):       [FILL IN — describe the key algorithms, their function in the
                          system, and the rationale for choosing them]

Key Parameters:          [FILL IN — hyperparameters, decision thresholds, confidence
                          levels, and how they were determined]

Optimization Objective:  [FILL IN — what the system optimizes for.
                          Example: "Maximize precision of top-10 candidate ranking
                          while maintaining fairness metrics across protected groups"]

Known Limitations:       [FILL IN — technical limitations of the algorithmic approach.
                          Example: "Performance degrades on applications with fewer
                          than 50 words of free text; limited accuracy for roles
                          without historical hiring data"]
```

### b.4 Training Data

(Reference: Art. 10 — Data and Data Governance)

```
Training Dataset Name:    [FILL IN]
Dataset Size:             [FILL IN — number of records, storage size]
Data Sources:             [FILL IN — where the data came from. List all sources]
Data Collection Period:   [FILL IN — date range of collected data]
Data Collection Method:   [FILL IN — how data was gathered]

Data Governance:
  Data Quality Measures:  [FILL IN — cleaning, deduplication, validation steps]
  Bias Examination:       [FILL IN — what biases were tested for and results.
                           Reference Art. 10(2)(f) — examination for possible biases]
  Data Gaps:              [FILL IN — known gaps or underrepresentation in the data]
  Representativeness:     [FILL IN — how well the data represents the intended
                           deployment population]
  Personal Data:          [FILL IN — does the dataset contain personal data?
                           If yes: legal basis for processing, DPIA reference,
                           anonymization/pseudonymization measures]
  Copyright Compliance:   [FILL IN — how copyright obligations were met for
                           training data, especially if using third-party content]
```

### b.5 Validation and Testing Data

```
Validation Dataset:       [FILL IN — separate from training? Size, source, composition]
Test Dataset:             [FILL IN — separate from training and validation?]
Holdout Strategy:         [FILL IN — how train/validation/test splits were created]
Cross-Validation:         [FILL IN — if used, describe the approach]
```

### b.6 Performance Metrics and Testing Results

```
Primary Metrics:          [FILL IN — accuracy, precision, recall, F1, AUC, etc.
                           Include specific numeric results]

Fairness Metrics:         [FILL IN — demographic parity, equalized odds, disparate
                           impact ratio, etc. Include results broken down by
                           protected characteristics where applicable]

Robustness Testing:       [FILL IN — adversarial testing, edge cases, stress testing
                           results]

Benchmark Comparisons:    [FILL IN — if applicable, comparison to industry benchmarks
                           or baseline approaches]

Test Environment:         [FILL IN — hardware, software, configuration used for testing]
```

---

## SECTION (c): Monitoring, Functioning, and Control

*Annex IV, Section 1(c): Detailed information about the monitoring, functioning, and
control of the AI system.*

### c.1 Operational Monitoring

```
Monitoring Approach:      [FILL IN — how the system is monitored during operation.
                           Include tools, dashboards, alert systems]

Performance Monitoring:   [FILL IN — how ongoing accuracy/performance is tracked.
                           Example: "Monthly drift detection comparing production
                           outputs against validation baseline"]

Logging:                  [FILL IN — what the system logs automatically (Art. 12).
                           Include: input data, outputs, confidence scores,
                           human oversight actions, system errors]

Log Retention:            [FILL IN — minimum 6 months for deployers (Art. 26(6));
                           specify provider-side retention policy]
```

### c.2 Human Oversight (Art. 14)

```
Oversight Model:          [FILL IN — Human-in-the-loop / Human-on-the-loop /
                           Human-in-command. Describe which and why]

Oversight Interface:      [FILL IN — how human overseers interact with the system.
                           Describe the UI/dashboard/tools provided]

Override Capability:      [FILL IN — how a human can override, reverse, or stop
                           the system's operation]

Competence Requirements:  [FILL IN — what training/qualifications are required for
                           the human overseer]

Automation Bias Safeguards: [FILL IN — measures to prevent over-reliance on the
                              system's outputs. Reference Art. 14(4)(b)]
```

### c.3 System Controls

```
Access Controls:          [FILL IN — who can access the system, authentication
                           requirements, role-based access]

Input Validation:         [FILL IN — how the system validates and sanitizes inputs]

Output Controls:          [FILL IN — confidence thresholds, output filtering,
                           explanations provided with outputs]

Fail-Safe Mechanisms:     [FILL IN — what happens when the system fails, encounters
                           an error, or produces low-confidence results]
```

---

## SECTION (d): Risk Management System

*Annex IV, Section 1(d): A description of the risk management system in accordance with
Art. 9.*

```
Risk Management Process:  [FILL IN — describe the continuous, iterative risk management
                           process as required by Art. 9(1)]

Risk Identification:      [FILL IN — list identified risks and the methodology used to
                           identify them. Reference Art. 9(2)(a) — foreseeable risks
                           and misuse risks]

Risk Analysis:            [FILL IN — for each identified risk:
                           - Likelihood (Low / Medium / High)
                           - Severity (Low / Medium / High)
                           - Affected persons/groups
                           - Risk mitigation measures adopted]

Residual Risk:            [FILL IN — risks remaining after mitigation. Art. 9(4)
                           requires that residual risks are communicated to deployers]

Risk Acceptability:       [FILL IN — how residual risk levels were determined to be
                           acceptable. Reference Art. 9(2)(c)]

Testing for Risk:         [FILL IN — how the system was tested against identified risks.
                           Art. 9(7) requires testing in real-world conditions
                           where appropriate]

Risk Communication:       [FILL IN — how risks are communicated to deployers in the
                           instructions of use (Art. 13)]
```

---

## SECTION (e): Changes During Lifecycle

*Annex IV, Section 1(e): A detailed description of changes made to the system throughout
its lifecycle.*

```
Change Management Process: [FILL IN — how changes are proposed, reviewed, approved,
                            and documented]

Version History:

  Version [X.Y]:
    Date:                  [FILL IN]
    Changes:               [FILL IN — describe what changed]
    Impact Assessment:     [FILL IN — did this change affect compliance?
                            Was re-assessment needed?]
    Re-testing:            [FILL IN — what testing was performed post-change]

  [Repeat for each significant version]

Substantial Modification Threshold: [FILL IN — define what constitutes a substantial
                                     modification for this system, triggering a new
                                     conformity assessment under Art. 43(4)]

Post-Market Monitoring Feedback: [FILL IN — how post-market monitoring findings feed
                                  back into system changes. Reference Art. 72]
```

---

## SECTION (f): Harmonised Standards Applied

*Annex IV, Section 1(f): A list of the harmonised standards applied in full or in part,
and where those harmonised standards have not been applied, a description of the solutions
adopted to meet the requirements.*

```
Harmonised Standards Applied:

  Standard:               [FILL IN — e.g., "EN XXXXX:202X — AI System Risk Management"]
  Applied Sections:       [FILL IN — full or partial application; specify sections]
  Justification:          [FILL IN — why this standard was chosen]

  [Repeat for each standard]

Where No Harmonised Standard Exists:

  Requirement:            [FILL IN — which Art. 8-15 requirement]
  Alternative Solution:   [FILL IN — how compliance was achieved without a harmonised
                           standard. Include technical specifications, industry standards,
                           or internal methodologies used]
  Justification:          [FILL IN — why this alternative is equivalent]
```

(Guidance: As of 2026, harmonised standards under the AI Act are still being developed by
CEN/CENELEC. Where they are not yet available, document the alternative approaches you
used to meet each requirement. The Commission's common specifications under Art. 41 may
apply as interim measures.)

---

## SECTION (g): Conformity Assessment Description

*Annex IV, Section 1(g): A description of the conformity assessment procedure followed.*

```
Assessment Procedure:     [FILL IN — Annex VI (internal control / self-assessment)
                           or Annex VII (third-party / notified body)]

Annex VI Procedure:       [FILL IN if applicable — describe how each step of Annex VI
                           was completed. Reference conformity-assessment.md for
                           detailed walkthrough]

Notified Body:            [FILL IN if Annex VII — name, identification number,
                           scope of assessment]

Assessment Date:          [FILL IN]
Assessment Outcome:       [FILL IN — compliant / non-compliant with conditions / etc.]
Certificate Reference:    [FILL IN if applicable — certificate number, validity period]
```

See [conformity-assessment.md](./conformity-assessment.md) for the complete step-by-step
walkthrough of both Annex VI and Annex VII procedures.

---

## SECTION (h): EU Declaration of Conformity

*Annex IV, Section 1(h): A copy of the EU declaration of conformity referred to in
Art. 47.*

```
EU DECLARATION OF CONFORMITY

Issued under Article 47, Regulation (EU) 2024/1689

1. AI System Identification:
   Name:                  [FILL IN]
   Version:               [FILL IN]
   Serial/Batch Number:   [FILL IN — if applicable]
   Any additional information enabling identification: [FILL IN]

2. Provider Information:
   Name:                  [FILL IN]
   Address:               [FILL IN]
   EU Authorized Representative (if applicable): [FILL IN — name, address]

3. This declaration of conformity is issued under the sole responsibility of the provider.

4. Object of the declaration:
   [FILL IN — description of the AI system sufficient for traceability purposes]

5. The AI system described above is in conformity with the following provisions of
   Regulation (EU) 2024/1689:
   [FILL IN — list the specific provisions: Arts. 8-15, and any other applicable
    requirements]

6. Harmonised standards or other specifications applied:
   [FILL IN — reference the standards from Section (f)]

7. Where applicable, the notified body:
   Name:                  [FILL IN]
   Identification Number: [FILL IN]
   Certificate Reference: [FILL IN]

8. Additional information:
   [FILL IN — any supplementary information relevant to conformity]

Signed for and on behalf of:
Name:                      [FILL IN]
Position:                  [FILL IN]
Date:                      [FILL IN]
Place:                     [FILL IN]
Signature:                 _____________________
```

(Guidance: The EU declaration of conformity must be kept up to date and available to
national competent authorities for 10 years (Art. 47(3)). It must be translated into the
language(s) required by the Member State(s) where the system is placed on the market.)

---

## Documentation Maintenance Checklist

This documentation is not a one-time exercise. Maintain it with this cadence:

- [ ] **On every release**: Update version history (Section e), re-evaluate metrics (Section b.6)
- [ ] **Quarterly**: Review risk management (Section d), update monitoring data (Section c)
- [ ] **Annually**: Full review of all sections, update declaration of conformity
- [ ] **On substantial modification**: Reassess conformity, update all affected sections
- [ ] **On regulatory change**: Review against updated requirements or standards
- [ ] **On incident**: Update risk section, document corrective actions in change log

---

## Key Takeaways

1. **This is the core compliance artifact for high-risk AI systems.** Regulators will
   ask for it. Your conformity assessment is based on it. Keep it thorough.
2. **Start early.** Do not treat documentation as an afterthought. Build it alongside
   development.
3. **Be specific.** Vague descriptions do not satisfy regulatory scrutiny. Use concrete
   numbers, specific metrics, and detailed process descriptions.
4. **Keep it current.** Art. 11(2) requires continuous updates. Stale documentation is
   non-compliant documentation.
5. **10-year retention.** Plan your document management accordingly.
