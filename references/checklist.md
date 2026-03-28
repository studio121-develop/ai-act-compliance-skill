<!-- Last verified against EUR-Lex: 2026-03-28 -->

> **Disclaimer**: This checklist provides general guidance — not legal advice. See LEGAL_NOTICE.md for full terms.

# AI Act Compliance Checklist — Comprehensive Version

Article-by-article checklist for developers building AI-powered products. Organized by phase: pre-development, development, pre-deployment, post-deployment.

---

## PHASE 0 — GOVERNANCE AND ORGANIZATION

### 0.1 Roles and Responsibilities
- [ ] Identify the person responsible for AI Act compliance within the organization
- [ ] Determine whether your company is a Provider or Deployer for each AI system
- [ ] If acting as Provider: document that you are the entity "placing on the market" the AI system
- [ ] If substantially modifying a third-party AI system: document that you are assuming Provider obligations (Art. 25)
- [ ] Define the responsibility chain: model provider (e.g. Anthropic) → system provider (you) → deployer (customer)
- [ ] Appoint an authorized representative if the company is based outside the EU (Art. 22)

### 0.2 AI Literacy (Art. 4) — IN FORCE SINCE 2 FEB 2025
- [ ] Assess the AI competency level of your team
- [ ] Plan and document AI training for all staff involved with AI
- [ ] Training must cover: how AI models work, limitations, risks, regulatory obligations
- [ ] Maintain training records (dates, participants, topics covered)
- [ ] Update training at least annually or whenever there is a significant technology change
- [ ] Extend the literacy requirement to freelancers and external collaborators working with AI

### 0.3 AI Systems Inventory
- [ ] Create a complete registry of all AI systems used or provided
- [ ] For each system, document: name, description, underlying AI model, intended purpose
- [ ] For each system, document: data processed, target users, deployment date
- [ ] For each system, document: company role (Provider/Deployer), risk classification
- [ ] Update the registry whenever a new AI feature is added or a substantial modification is made
- [ ] Keep historical versions of the registry (version control)

---

## PHASE 1 — RISK CLASSIFICATION

### 1.1 Prohibited Practices Check (Art. 5) — IN FORCE SINCE 2 FEB 2025
- [ ] Verify the system does NOT use subliminal techniques to manipulate behavior
- [ ] Verify the system does NOT exploit vulnerabilities of specific groups (age, disability, social situation)
- [ ] Verify the system does NOT perform social scoring (evaluating individuals based on social behavior)
- [ ] Verify the system does NOT use real-time remote biometric identification in public spaces (except for strictly limited exceptions)
- [ ] Verify the system does NOT carry out untargeted scraping of facial images from the internet or CCTV
- [ ] Verify the system does NOT infer emotions in workplace or educational settings (except for medical/safety reasons)
- [ ] Verify the system does NOT biometrically categorize people to deduce race, political opinions, sexual orientation, etc.
- [ ] Verify the system does NOT use predictive AI to assess the risk of criminal offending based on profiling
- [ ] Document the outcome of this check, including date and responsible person

### 1.2 High-Risk Check (Annex III)
- [ ] Review EACH of the 8 Annex III categories for every AI system:
  - [ ] 1. Biometrics: does the system identify or categorize people using biometric data?
  - [ ] 2. Critical infrastructure: does the system manage energy, transport, water, gas, or heating?
  - [ ] 3. Education: does the system influence admissions, assessments, exams, or learning paths?
  - [ ] 4. Employment: does the system influence hiring, CV screening, performance evaluations, promotions, or dismissals?
  - [ ] 5. Essential services: does the system affect creditworthiness, insurance, access to public services, or emergency prioritization?
  - [ ] 6. Law enforcement: does the system evaluate evidence, predict crime, or perform profiling?
  - [ ] 7. Migration: does the system assess visa/asylum applications or monitor borders?
  - [ ] 8. Justice/Democracy: does the system assist in legal research, dispute resolution, or electoral processes?
- [ ] If the system falls under Annex III → check whether the Art. 6(3) exemption applies:
  - [ ] Does the system perform a narrow procedural task?
  - [ ] Does the system improve the result of a previously completed human activity?
  - [ ] Does the system detect decision-making patterns without replacing or influencing human judgment?
  - [ ] Does the system perform a preparatory task for an Annex III assessment?
- [ ] If the system profiles individuals (automated processing of personal data to evaluate aspects of a person) → the Art. 6(3) exemption does NOT apply → it is ALWAYS high-risk
- [ ] Document the classification with a detailed justification
- [ ] If declaring "not high-risk" for an Annex III system: document this before placing on the market (Art. 6(3))

### 1.3 Transparency Risk Check (Art. 50)
- [ ] Does the system interact directly with people? → Disclosure obligation
- [ ] Does the system generate synthetic text? → Marking obligation
- [ ] Does the system generate synthetic images? → Marking obligation
- [ ] Does the system generate synthetic audio? → Marking obligation
- [ ] Does the system generate synthetic video? → Marking obligation
- [ ] Does the system recognize emotions? → Notification obligation
- [ ] Does the system perform biometric categorization? → Notification obligation
- [ ] Does the system generate or manipulate deepfakes? → Specific disclosure obligation
- [ ] Does the system generate text to inform the public on matters of public interest? → Specific disclosure obligation
- [ ] Document all applicable obligations along with an implementation plan

---

## PHASE 2 — DEVELOPMENT (Design & Build)

### 2.1 Transparency — AI Interaction Disclosure (Art. 50.1)
- [ ] Implement a visible banner or modal BEFORE the first AI interaction
- [ ] The disclosure message must be "clear and distinguishable" — NOT buried in the ToS
- [ ] Use language that is understandable to the target user (local language for local markets)
- [ ] Include: that it is an AI system, what it does, and what its limitations are
- [ ] Implement periodic reminders during long conversations
- [ ] Test that the disclosure is visible on all devices (mobile, desktop, tablet)
- [ ] Test with screen readers for accessibility (WCAG 2.1)
- [ ] Document the technical implementation of the disclosure

### 2.2 Transparency — AI Content Marking (Art. 50.2)
- [ ] Implement machine-readable marking on ALL AI-generated content
- [ ] Choose and implement a marking standard (C2PA / IPTC / custom metadata)
- [ ] Include in metadata: ai_generated flag, model provider, system name, timestamp
- [ ] Implement visible marking for the end user (label, badge, footer)
- [ ] Verify that the marking is robust (not easily removable by the user)
- [ ] Implement a downstream detection mechanism (for recipients of the content)
- [ ] If the content is an "assistive function" for standard editing → document why the exemption applies
- [ ] Test marking end-to-end: generation → storage → display → export

### 2.3 Transparency — Deepfakes and Public Interest Text (Art. 50.4)
- [ ] If generating images/audio/video that resemble real people: implement visible disclosure
- [ ] If generating text to inform the public: implement disclosure
- [ ] For artistic or satirical content: disclosure must exist but should not hinder the experience
- [ ] If content has human editorial oversight + editorial responsibility: document the exemption

### 2.4 AI Privacy Notice (GDPR + AI Act)
- [ ] Update the privacy policy with a dedicated AI usage section
- [ ] Specify which data is sent to the AI model
- [ ] Specify the GDPR legal basis for AI processing (consent / legitimate interest / contract)
- [ ] Specify the AI model provider and its data retention policy
- [ ] Specify whether data is used for model training (typically NO with commercial APIs)
- [ ] Inform about the existence of automated decision-making processes (Art. 22 GDPR)
- [ ] Guarantee the right to opt out of purely automated decisions (Art. 22 GDPR)
- [ ] If processing special category data (Art. 9 GDPR): conduct a DPIA
- [ ] Implement data minimization: send only strictly necessary data to the model
- [ ] Implement pseudonymization/anonymization where possible before sending data to the model

### 2.5 Terms of Service
- [ ] Update ToS with an AI usage clause
- [ ] Specify: description of AI features, limitations, disclaimer for inaccuracies
- [ ] Specify: that AI-generated content does not replace professional advice
- [ ] Specify: the user's responsibility in verifying AI-generated content
- [ ] Specify: compliance with the AI Act (EU Reg. 2024/1689)
- [ ] Have the clauses reviewed by legal counsel

### 2.6 Data Governance (best practice for all, mandatory for high-risk)
- [ ] Document which data is sent to the AI model for each feature
- [ ] Implement input filters: remove unnecessary sensitive data before sending
- [ ] Implement output filters: review AI responses before showing them to the user
- [ ] Implement rate limiting to prevent abuse
- [ ] Implement content moderation on AI outputs
- [ ] Document the data processing chain: user → your system → API provider → response → user

### 2.7 Human Oversight
- [ ] Implement a mechanism to disable AI features ("kill switch")
- [ ] Implement a mechanism for users to report inappropriate responses (feedback/flag)
- [ ] Define an escalation process: when and how a human operator intervenes
- [ ] For consequential decisions: implement a mandatory human review step
- [ ] Test the kill switch end-to-end
- [ ] Document the oversight process

### 2.8 Logging and Audit Trail
- [ ] Implement logging of all AI interactions (pseudonymized)
- [ ] Logs must include: timestamp, interaction type, disclosure shown, content marked
- [ ] Logs must include: model used, system version, any errors
- [ ] Define a retention period for logs (at least 6 months recommended — verify against GDPR)
- [ ] Protect logs from tampering (integrity)
- [ ] Implement a log export mechanism for audits

### 2.9 Accuracy and Robustness (Art. 15 — best practice for all)
- [ ] Document the known limitations of the AI system
- [ ] Implement error handling for API failures (timeouts, rate limits, model errors)
- [ ] Implement graceful fallback when AI is unavailable
- [ ] Test system behavior with adversarial inputs (prompt injection)
- [ ] Implement baseline protections against prompt injection
- [ ] Monitor AI response quality over time

### 2.10 Cybersecurity (Art. 15 — best practice for all)
- [ ] Protect AI model API keys (environment variables, secrets manager)
- [ ] Implement HTTPS for all communications with the AI API
- [ ] Implement user authentication before granting access to AI features
- [ ] Rate limiting for AI endpoints
- [ ] Monitor for anomalous usage (attacks, abuse)
- [ ] Sign a Data Processing Agreement (DPA) with the AI provider

---

## PHASE 3 — PRE-DEPLOYMENT

### 3.1 Technical Documentation
- [ ] Create or update the `AI_ACT_COMPLIANCE.md` file in the project root
- [ ] Complete all sections: system description, classification, AI model, transparency, data, oversight, risks
- [ ] Have the documentation reviewed internally
- [ ] Store the documentation in version control

### 3.2 Contractual Verification
- [ ] Verify that the contract with the AI provider (e.g. Anthropic Terms of Service) is compatible with AI Act obligations
- [ ] Verify the Data Processing Agreement with the AI provider
- [ ] If you have B2B customers using the system as deployers: provide them with the usage instructions needed for their own compliance

### 3.3 Compliance Testing
- [ ] Test disclosure: verify that the AI notice is visible across all user journeys
- [ ] Test marking: verify that AI metadata is present on all generated content
- [ ] Test kill switch: verify that AI features can be disabled
- [ ] Test human oversight: verify that the escalation process works
- [ ] Test logging: verify that all interactions are correctly logged
- [ ] Test accessibility: verify that disclosure and labels are accessible (screen reader, contrast)
- [ ] Test mobile: verify compliance on all target devices
- [ ] Test privacy: verify that the privacy policy is up to date and accessible
- [ ] Test ToS: verify that the terms of service are up to date

### 3.4 Final Review
- [ ] Art. 5 checklist (prohibited practices): confirmed
- [ ] Risk classification: documented and confirmed
- [ ] Art. 50 obligations: all implemented and tested
- [ ] Privacy policy: updated
- [ ] ToS: updated
- [ ] Technical documentation: complete and up to date
- [ ] Team trained on AI literacy: confirmed
- [ ] DPA with AI provider: in place

---

## PHASE 4 — POST-DEPLOYMENT

### 4.1 Ongoing Monitoring
- [ ] Quarterly review of risk classification (new features → new classification)
- [ ] Monitor user reports of inappropriate AI responses
- [ ] Analyze logs to identify problematic patterns
- [ ] Periodically verify that disclosure and marking are working correctly
- [ ] Update documentation with every release that includes AI features
- [ ] Monitor regulatory updates (see references/auto-update.md)

### 4.2 Incident Management
- [ ] Define what constitutes an "AI incident" for your system
- [ ] Examples: an AI response that causes harm to a user, data leak through AI, systematic discrimination
- [ ] Response procedure: identification → containment → analysis → resolution → report
- [ ] For high-risk systems: mandatory reporting to market surveillance authorities within 15 days (Art. 73)
- [ ] Maintain an incident register with corrective actions

### 4.3 Updates and Modifications
- [ ] Every substantial modification to the AI system → re-classify risk
- [ ] AI model change (e.g. from Claude Sonnet to Claude Opus) → update documentation
- [ ] Significant system prompt change → verify that the classification still holds
- [ ] New AI feature → run the entire checklist for the new feature
- [ ] Update to the AI provider's terms → verify compatibility

### 4.4 Cooperation with Authorities (Art. 21)
- [ ] Be prepared to provide documentation to authorities upon request
- [ ] Keep compliance records accessible and organized
- [ ] Designate a point of contact for the competent authorities
- [ ] For systems registered in the EU database: keep the information up to date

---

## ADDITIONAL REQUIREMENTS FOR HIGH-RISK SYSTEMS

If your system is classified as high-risk, add these requirements (see also references/high-risk-requirements.md):

### HR.1 Risk Management System (Art. 9)
- [ ] Establish a continuous risk management system covering the entire lifecycle
- [ ] Identify and analyze known and reasonably foreseeable risks
- [ ] Estimate and evaluate risks from intended use AND from reasonably foreseeable misuse
- [ ] Adopt appropriate risk management measures
- [ ] Test the system to identify the most appropriate measures
- [ ] Document the entire risk management process

### HR.2 Data Governance (Art. 10)
- [ ] Training, validation, and test datasets must be relevant and sufficiently representative
- [ ] Implement data governance practices: design choices, collection, preparation, labeling
- [ ] Examine data for bias
- [ ] Identify gaps in the data

### HR.3 Technical Documentation (Art. 11 + Annex IV)
- [ ] General description of the AI system
- [ ] Detailed description of elements and development process
- [ ] Information on monitoring, operation, and control
- [ ] Description of the risk management system
- [ ] Description of changes throughout the lifecycle
- [ ] List of harmonized standards applied
- [ ] Description of the conformity assessment performed
- [ ] EU declaration of conformity

### HR.4 Record-Keeping / Logging (Art. 12)
- [ ] Automatic event logging throughout the entire lifecycle
- [ ] Logs must enable traceability of system operation
- [ ] Logging must be proportionate to the intended purpose
- [ ] Comply with recognized standards or common specifications

### HR.5 Transparency to Deployers (Art. 13)
- [ ] Instructions for use provided to deployers, including:
  - [ ] Provider identity and contact details
  - [ ] System characteristics, capabilities, and limitations
  - [ ] Intended purpose and reasonably foreseeable misuse
  - [ ] Changes made by the provider over time
  - [ ] Human oversight measures
  - [ ] Expected lifetime and maintenance requirements
  - [ ] Required computational resources and hardware

### HR.6 Human Oversight (Art. 14)
- [ ] System designed to allow effective human oversight
- [ ] Supervisory personnel must be able to:
  - [ ] Fully understand the system's capabilities and limitations
  - [ ] Monitor system operation
  - [ ] Decide not to use the system, or to ignore/override its output
  - [ ] Intervene or halt operation ("stop button")

### HR.7 Accuracy, Robustness, Cybersecurity (Art. 15)
- [ ] Accuracy levels appropriate for the intended purpose (declared in the instructions)
- [ ] Resilience to errors, faults, and inconsistencies
- [ ] Resilience to unauthorized attempts to alter use or performance
- [ ] Technical redundancy solutions where appropriate

### HR.8 Quality Management System (Art. 17)
- [ ] Strategy for regulatory compliance
- [ ] Techniques and procedures for design, development, and testing
- [ ] Examination, testing, and validation procedures
- [ ] Technical specifications and standards applied
- [ ] Data management systems and procedures
- [ ] Risk management system
- [ ] Post-market monitoring system
- [ ] Incident reporting procedures
- [ ] Communication with authorities, competent bodies, deployers, and users

### HR.9 Conformity Assessment
- [ ] Self-assessment (Annex VI) for most AI systems
- [ ] Notified body assessment (Annex VII) for biometric identification systems
- [ ] EU declaration of conformity issued
- [ ] CE marking affixed

### HR.10 Registration
- [ ] Register in the EU database BEFORE placing on the market
- [ ] Update within 14 days of significant changes

---

## TIMELINE MATRIX

| Requirement | Deadline | Status |
|-------------|----------|--------|
| Prohibited practices (Art. 5) | 2 Feb 2025 | IN FORCE |
| AI Literacy (Art. 4) | 2 Feb 2025 | IN FORCE |
| GPAI model provider obligations | 2 Aug 2025 | IN FORCE |
| Governance and penalty regime | 2 Aug 2025 | IN FORCE |
| **Transparency Art. 50** | **2 Aug 2026** | **NEXT DEADLINE** |
| **High-risk Annex III standalone** | **2 Aug 2026** | **NEXT DEADLINE** |
| High-risk in regulated products | 2 Aug 2027 | Upcoming |
| GPAI pre-existing models | 2 Aug 2027 | Upcoming |
| Large-scale IT systems (Annex X) | 31 Dec 2030 | Future |
