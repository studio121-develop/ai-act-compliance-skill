# Conformity Assessment Walkthrough

The conformity assessment is where all your compliance work gets validated. It is the
formal process by which you (or a notified body) verify that your high-risk AI system
meets all the requirements of the AI Act before you can legally place it on the EU market.

For most SaaS products using AI APIs, you will self-assess under Annex VI. This document
walks you through both paths, step by step.

---

## When Annex VI (Self-Assessment) Applies vs. Annex VII (Third-Party)

The default for high-risk AI systems is **self-assessment under Annex VI** (internal
control). This is the path for the vast majority of systems.

**Third-party assessment under Annex VII** is required only when the high-risk AI system
is (Art. 43(1)):

- A **remote biometric identification system** for law enforcement purposes
  (Annex III, point 1, insofar as those systems use biometric identification)

For all other high-risk AI systems listed in Annex III, the provider may choose between
Annex VI and Annex VII, but Annex VI is sufficient (Art. 43(2)).

### Special case: products under Union harmonisation legislation

If the AI system is a safety component of a product already covered by Union
harmonisation legislation listed in **Annex I, Section A** (e.g., machinery, medical
devices, toys), the conformity assessment follows the procedure already established under
that sector-specific legislation (Art. 43(3)). The AI Act requirements (Arts. 8-15)
are assessed as part of the existing conformity assessment for that product.

### Decision tree:

```
Is your system used for remote biometric identification by law enforcement?
  YES → Annex VII (third-party assessment by notified body) is MANDATORY
  NO  → Is your system a safety component of a product under Annex I, Section A?
          YES → Follow the existing conformity assessment for that product sector
          NO  → Annex VI (self-assessment) is sufficient
                (You may also voluntarily choose Annex VII)
```

---

## Step-by-Step: Annex VI Procedure (Self-Assessment)

Annex VI is titled "Internal control." You perform this assessment yourself — no notified
body required. But "self-assessment" does not mean "quick and easy." It means you are
taking full responsibility for verifying compliance.

### Step 1: Verify your Quality Management System conforms to Art. 17

Art. 17 requires providers of high-risk AI systems to have a QMS that covers:

- **Strategy for regulatory compliance** (Art. 17(1)(a)) — including conformity
  assessment procedures and procedures for managing changes
- **Techniques, procedures, and systematic actions** for design, development, quality
  control, and quality assurance (Art. 17(1)(b))
- **Examination, test, and validation procedures** before, during, and after development
  (Art. 17(1)(c))
- **Technical specifications** including standards to be applied (Art. 17(1)(d))
- **Systems and procedures for data management** including data acquisition, collection,
  analysis, labeling, storage, filtration, mining, aggregation, retention, and any other
  operation regarding the data (Art. 17(1)(e))
- **Risk management system** as described in Art. 9 (Art. 17(1)(f))
- **Post-market monitoring system** as described in Art. 72 (Art. 17(1)(g))
- **Procedures for incident reporting** as in Art. 73 (Art. 17(1)(h))
- **Communication with authorities, notified bodies, and deployers** (Art. 17(1)(i))
- **Systems and procedures for record keeping** (Art. 17(1)(j))
- **Resource management** including security-of-supply measures (Art. 17(1)(k))
- **Accountability framework** for management and other staff (Art. 17(1)(l))

**How to verify:** Document your QMS, map each Art. 17 requirement to your specific
processes, and confirm coverage. If you have ISO 9001 or ISO 13485 certification, you
have a solid foundation — but you will need AI-specific additions.

**Deliverable:** QMS documentation with AI Act Art. 17 compliance mapping.

### Step 2: Examine technical documentation (Annex IV)

This is the bulk of the work. Your technical documentation must be complete, accurate, and
current. See [annex-iv-template.md](./annex-iv-template.md) for the full template.

**How to verify:**
- Walk through every section of your Annex IV documentation
- Confirm that each section accurately reflects the current state of the system
- Verify that performance metrics are based on actual testing (not projections)
- Confirm that the risk management section reflects real risks and real mitigations
- Ensure the documentation covers the specific version being placed on the market

**Deliverable:** Completed Annex IV technical documentation.

### Step 3: Verify design and development process

This step confirms that the process you used to build the system actually implements
what your QMS and technical documentation describe.

**How to verify:**
- Review development records against QMS procedures
- Confirm that data governance (Art. 10) was actually followed during training
- Verify that the testing described in the documentation was actually performed
- Confirm that risk management was an iterative process throughout development,
  not a retrospective exercise (Art. 9(1) requires continuous risk management)
- Check that human oversight measures (Art. 14) are actually implemented, not
  just documented

**Deliverable:** Design and development review report with evidence references.

### Step 4: Verify post-market monitoring system

Art. 72 requires a post-market monitoring system proportionate to the nature of the
AI system and its risks.

**How to verify:**
- Confirm that the monitoring system is designed and documented
- Verify it can detect performance degradation, drift, and emerging risks
- Confirm it includes a process for analyzing data collected during operation
- Verify the connection between monitoring findings and corrective actions
- Confirm the post-market monitoring plan is included in the technical documentation

**Deliverable:** Post-market monitoring plan and system verification.

### Step 5: Document the assessment

The final step is to formally record your assessment findings.

**How to verify:**
- Compile all evidence from Steps 1-4
- Prepare the EU Declaration of Conformity (Art. 47) — see template in
  [annex-iv-template.md](./annex-iv-template.md), Section (h)
- Affix CE marking (Art. 48)
- Register in the EU Database (Art. 71)
- Archive all documentation for 10 years (Art. 18(1))

**Deliverable:** Conformity assessment report, EU Declaration of Conformity, CE marking,
EU Database registration.

---

## Step-by-Step: Annex VII Procedure (Third-Party Assessment)

Annex VII applies to remote biometric identification systems used by law enforcement.
A notified body (an organization designated by a Member State to perform conformity
assessments) conducts this assessment.

### Step 1: Select a notified body

- Notified bodies are listed in the **NANDO database** (New Approach Notified and
  Designated Organisations): https://ec.europa.eu/growth/tools-databases/nando/
- Choose a body notified specifically for AI Act assessments
- Verify their scope covers your system's Annex III category
- Expect notified body availability to be limited in the early years — plan ahead

### Step 2: Submit application to the notified body

Provide:
- Your complete technical documentation (Annex IV)
- Your QMS documentation (Art. 17)
- Evidence of your design and development process
- Access to the AI system for testing (if requested)

### Step 3: Notified body assesses the QMS

The notified body verifies your QMS against Art. 17, including (Annex VII, Section 3):
- That the QMS is established and implemented
- That it covers all Art. 17 requirements
- That management review and internal audit processes are in place
- That corrective and preventive action processes are established

### Step 4: Notified body examines technical documentation

The notified body reviews your Annex IV documentation to verify (Annex VII, Section 4):
- The system was designed and developed in conformity with Arts. 8-15
- The testing and validation results are adequate
- The risk management system is appropriate
- The documentation is complete and accurate

### Step 5: Notified body tests the system (if necessary)

The notified body may (Annex VII, Section 4.4):
- Perform or request additional testing of the AI system
- Require access to training and testing data
- Request source code review (under strict confidentiality)
- Test the system in conditions reflecting the intended purpose

### Step 6: Notified body issues certificate

If the assessment is positive, the notified body issues a **certificate of conformity**
(Annex VII, Section 6). This certificate:
- Is valid for a maximum of **5 years**
- Can be renewed
- Can be suspended or withdrawn if the provider no longer complies
- Must specify any conditions or restrictions

### Step 7: Provider completes the process

With the notified body certificate in hand:
- Prepare the EU Declaration of Conformity (referencing the certificate)
- Affix CE marking
- Register in the EU Database
- Archive all documentation for 10 years

---

## EU Declaration of Conformity (Art. 47)

The declaration is the provider's formal, legally binding statement that the system
complies with the AI Act. Key requirements:

- Must be **continuously updated** (Art. 47(2))
- Must contain the information set out in **Annex V** (see template in
  [annex-iv-template.md](./annex-iv-template.md), Section (h))
- Must be translated into the language(s) required by the Member State(s) where
  the system is placed on the market (Art. 47(4))
- Must be kept available for national competent authorities for **10 years**
  (Art. 47(3))
- Must be provided to deployers with the system (Art. 47(5))

A single declaration may cover multiple AI systems, provided all relevant information
for each system is included (Art. 47(1)).

---

## CE Marking (Art. 48)

The CE marking indicates conformity with the AI Act. Requirements:

### Placement:
- Must be affixed **visibly, legibly, and indelibly** to the AI system (Art. 48(1))
- For AI systems (which are often software), the CE marking must appear in the
  **accompanying documentation** and, where applicable, on the packaging (Art. 48(2))
- For digital products: display the CE marking in the user interface, documentation,
  and any digital marketplace listing

### Format:
- Must follow the format specified in **Annex V** of Regulation (EC) No 765/2008
- Minimum height of **5 mm** (where physically affixed)
- Proportions must be maintained if enlarged or reduced

### Timing:
- Affix the CE marking **before** placing the system on the market (Art. 48(1))
- For Annex VII systems: the CE marking is accompanied by the identification number
  of the notified body (Art. 48(3))

### Do not misuse:
- Art. 48(4) prohibits affixing any marking that could mislead about the meaning or
  form of the CE marking
- Other markings are permitted only if they do not affect the visibility, legibility,
  or meaning of the CE marking

---

## EU Database Registration (Art. 71)

Before placing a high-risk AI system on the market (or when a deployer begins use),
registration in the EU Database is mandatory.

### What must be registered (Art. 71(2)):

**By the provider:**
- Provider name and contact details
- Name and description of the AI system
- Intended purpose
- Status (on the market, no longer on the market, recalled)
- Annex III classification
- Member States where the system is placed on the market
- Conformity assessment procedure followed (Annex VI or VII)
- Notified body details (if Annex VII)
- CE marking confirmation
- URL to instructions of use

**By the deployer (Art. 71(3)):**
- Deployer name and contact details
- Name of the AI system and provider reference
- Member States where the system is in use
- Fundamental Rights Impact Assessment summary (if applicable under Art. 27)

### Database access:
- The EU Database is publicly accessible for high-risk AI systems listed in Annex III
  (Art. 71(4))
- For systems used by law enforcement, migration, and asylum authorities, a separate
  non-public section exists (Art. 71(5))

### Timeline:
The EU Database is managed by the Commission and has been operational since the
regulation's entry into force. Registration is a prerequisite — you cannot legally place
a high-risk system on the market without it.

---

## Practical Timelines and Cost Estimates for SMEs

### Annex VI (Self-Assessment) Timeline:

| Phase | Duration | Notes |
|-------|----------|-------|
| QMS establishment / gap analysis | 2-4 months | Less if you have ISO 9001 |
| Technical documentation (Annex IV) | 2-6 months | Depends on system complexity |
| Testing and validation | 1-3 months | Parallel with documentation |
| Risk management formalization | 1-2 months | Should be ongoing from development |
| Self-assessment review | 2-4 weeks | Internal review of all materials |
| Declaration + CE marking + registration | 1-2 weeks | Administrative completion |
| **Total estimate** | **6-12 months** | From scratch; faster with existing QMS |

### Cost estimates (SME with 10-50 employees):

| Cost Category | Estimate | Notes |
|---------------|----------|-------|
| Legal consultation | EUR 5,000-20,000 | For compliance strategy and review |
| Technical documentation | EUR 10,000-30,000 | Internal effort + external support |
| Testing and validation | EUR 5,000-15,000 | Bias testing, performance evaluation |
| QMS development | EUR 5,000-15,000 | Less with existing quality systems |
| Regulatory sandbox (if used) | EUR 0-5,000 | Reduced fees for SMEs under Art. 62 |
| **Total Annex VI** | **EUR 25,000-85,000** | One-time; ongoing maintenance lower |

### Annex VII (Third-Party) Additional Costs:

| Cost Category | Estimate | Notes |
|---------------|----------|-------|
| Notified body fees | EUR 20,000-80,000 | Depending on system complexity |
| Additional testing | EUR 5,000-20,000 | If requested by notified body |
| Certification renewal (5-year cycle) | EUR 10,000-30,000 | Periodic |
| **Total Annex VII additional** | **EUR 35,000-130,000** | On top of Annex VI costs |

These estimates are based on early industry experience and may vary significantly by
Member State, system complexity, and the maturity of the notified body market.

Art. 62(1)(b) requires notified bodies to reduce fees proportionately for SMEs — do not
hesitate to request reduced rates and cite this provision.

---

## For Most SaaS Products: Your Annex VI Playbook

If you are building SaaS products that use AI APIs (Claude, GPT, Gemini, etc.) and your
system is classified as high-risk under Annex III, here is your concrete path:

### 1. Confirm your classification
Re-read Annex III carefully. Many SaaS products are **not** high-risk. If yours is,
identify the exact Annex III point.

### 2. Build your QMS (or extend your existing one)
If you have ISO 27001, SOC 2, or ISO 9001, you have a foundation. Create a compliance
mapping document showing how your existing quality processes map to Art. 17, and fill
the gaps.

### 3. Complete the Annex IV technical documentation
Use the template in [annex-iv-template.md](./annex-iv-template.md). Start with the
sections you can fill in today and work through the rest.

### 4. Formalize your risk management
If you have not been doing formal risk management per Art. 9, start now. It must be
continuous and iterative — a one-time risk assessment will not pass scrutiny.

### 5. Test for bias and performance
Document real metrics. Pay special attention to fairness across protected groups if your
system affects natural persons.

### 6. Set up post-market monitoring
At minimum: performance monitoring, drift detection, incident reporting, and a feedback
loop to your development process.

### 7. Conduct the self-assessment
Walk through Steps 1-5 of the Annex VI procedure above. Be honest — if you find gaps,
fix them before issuing the declaration.

### 8. Issue your declaration, affix CE marking, register
This is the administrative finish line. Once complete, you can legally place your system
on the EU market.

### 9. Maintain everything
This is not a one-time process. Update documentation, monitor the system, respond to
incidents, and re-assess on significant changes.

---

## Key Takeaways

1. **Self-assessment (Annex VI) is the path for most high-risk AI SaaS products.**
   Third-party assessment is only mandatory for biometric identification systems used by
   law enforcement.
2. **The QMS is the foundation.** Without a documented quality management system that
   covers all Art. 17 requirements, you cannot self-assess.
3. **Technical documentation is the evidence.** It must be complete, specific, and current.
   Regulators will judge your compliance by its quality.
4. **CE marking + EU Database registration = market access.** You cannot skip these steps.
5. **Budget EUR 25,000-85,000 for an SME's first Annex VI assessment.** Ongoing
   maintenance is less, but plan for annual reviews and updates.
6. **Start 6-12 months before you need to be compliant.** This is not something you can
   rush in the final weeks before a deadline.
