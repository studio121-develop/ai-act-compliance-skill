<!-- Last verified against EUR-Lex: 2026-03-28 -->

# High-Risk AI System Requirements (Arts. 9-15, 16-17)

> **Disclaimer**: This document provides general guidance — not legal advice. See [LEGAL_NOTICE.md](/LEGAL_NOTICE.md) for full terms.

This reference covers the full set of obligations for providers of high-risk AI systems under the EU AI Act. Most products built with AI APIs won't fall here, but review this if your system operates in any Annex III domain.

## When This Applies

Your system is high-risk if it:
- Is listed in Annex III categories AND poses significant risk to health/safety/fundamental rights
- Is a safety component of a product covered by EU harmonization legislation (Annex I)
- Profiles individuals (automated processing of personal data to evaluate aspects of a person's life)

### Annex III Categories (Detailed)

1. **Biometrics**: Remote biometric identification (not just verification), emotion recognition in sensitive contexts
2. **Critical Infrastructure**: AI managing electricity grids, water supply, gas, heating, road traffic — where failure endangers lives
3. **Education**: AI determining admission to educational institutions, evaluating learning outcomes, assessing appropriate education level, monitoring prohibited behavior during tests
4. **Employment**: AI for recruitment (job ads targeting, CV filtering, interview evaluation), promotion/termination decisions, task allocation based on individual behavior, performance monitoring
5. **Essential Services**: Credit scoring, life/health insurance risk assessment, emergency services dispatch prioritization, social benefits eligibility evaluation
6. **Law Enforcement**: Individual risk assessment (crime prediction), polygraph/similar tools, evidence reliability assessment, profiling during criminal investigation
7. **Migration**: Polygraph use on travelers, visa/asylum application assessment, irregular migration detection
8. **Justice & Democracy**: AI assisting judicial authorities in researching/interpreting facts and law, dispute resolution

### Art. 6(3) Derogation
An Annex III system is NOT high-risk if it:
- Performs a narrow procedural task
- Improves the result of a previously completed human activity
- Detects decision-making patterns without replacing/influencing the human assessment
- Performs a preparatory task to an Annex III assessment

**Important**: If the system profiles individuals, the derogation does NOT apply — it's always high-risk.

## Provider Obligations for High-Risk Systems

### Art. 9 — Risk Management System
- Establish and maintain a continuous risk management system throughout the AI system lifecycle
- Identify and analyze known and reasonably foreseeable risks
- Estimate and evaluate risks from intended use AND reasonably foreseeable misuse
- Adopt risk management measures (design choices, testing, information to deployers)
- Test the system to identify the most appropriate measures
- Document everything

### Art. 10 — Data and Data Governance
- Training, validation, and testing datasets must be relevant, sufficiently representative, and as error-free as possible
- Datasets must be appropriate for the intended purpose and geographic/behavioral/functional setting
- Implement data governance practices covering: design choices, data collection processes, data preparation operations, data labeling, relevance/representativeness assessment, bias examination, gap identification
- For systems using techniques involving training: use training, validation, and testing data sets that meet quality criteria

### Art. 11 — Technical Documentation
- Draw up technical documentation BEFORE placing on market
- Documentation must demonstrate compliance with all requirements
- Must contain at minimum the elements listed in Annex IV:
  - General description of the AI system
  - Detailed description of elements and development process
  - Monitoring, functioning, and control information
  - Risk management system description
  - Description of changes throughout lifecycle
  - List of harmonized standards applied
  - Description of conformity assessment performed
  - EU declaration of conformity

### Art. 12 — Record-Keeping (Logging)
- Design system for automatic logging of events throughout lifecycle
- Logs must enable tracing of system functioning
- Logging must be proportionate to intended purpose
- Must enable post-market monitoring
- Must conform to recognized standards or common specifications

### Art. 13 — Transparency and Information to Deployers
- Design system to be sufficiently transparent for deployers to understand output
- Provide instructions for use including:
  - Provider identity and contact
  - System characteristics, capabilities, limitations
  - Intended purpose and foreseeable misuse
  - Changes made by provider over time
  - Human oversight measures
  - Expected lifetime, maintenance, and care
  - Computational and hardware resources needed

### Art. 14 — Human Oversight
- Design system to allow effective oversight by natural persons
- Oversight must prevent/minimize risks to health, safety, fundamental rights
- Oversight measures must be commensurate with risks and level of autonomy
- Individuals performing oversight must be able to:
  - Fully understand system capabilities/limitations
  - Monitor system operation
  - Decide not to use the system or disregard/override output
  - Intervene or interrupt system operation ("stop button")

### Art. 15 — Accuracy, Robustness, Cybersecurity
- Achieve appropriate levels of accuracy for intended purpose (declared in instructions)
- Be resilient to errors, faults, inconsistencies
- Be resilient to unauthorized third-party attempts to alter use or performance
- Technical redundancy solutions where appropriate (backup, fail-safe plans)

### Art. 16-17 — Quality Management System
- Establish and document a QMS covering:
  - Strategy for regulatory compliance
  - Techniques and procedures for design, development, testing
  - Examination, test, and validation procedures
  - Technical specifications and standards applied
  - Systems and procedures for data management
  - Risk management system
  - Post-market monitoring system
  - Procedures for incident reporting
  - Communication with authorities, competent bodies, deployers, users
  - Procedures for accountability framework in multi-supplier settings

## Conformity Assessment

### Internal Control (Annex VI) — Most Common Path
- Provider self-assesses compliance
- Verify QMS conforms to requirements
- Examine technical documentation
- Verify design and development process and post-market monitoring

### Third-Party Assessment (Annex VII) — Required for Some Categories
- Required for biometric identification systems
- Notified body assessment of QMS and technical documentation
- Ongoing surveillance by notified body

## Registration in EU Database (Art. 71)
- Register high-risk systems BEFORE placing on market
- Database managed by European Commission
- Update within 14 days of significant changes

## CE Marking
- Affix CE marking to high-risk AI system before placing on market
- CE marking indicates conformity with AI Act
- Must be visible, legible, and indelible

## Post-Market Monitoring (Art. 72)
- Establish and document a post-market monitoring system
- Actively and systematically collect, document, and analyze data
- Assess continuous compliance with requirements
- Must be proportionate to nature and risk level

## Serious Incident Reporting (Art. 73)
- Report serious incidents to market surveillance authorities
- Report immediately after establishing causal link (max 15 days)
- "Serious incident" = death, serious damage to health/safety/fundamental rights/property/environment
