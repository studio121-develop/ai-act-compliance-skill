<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Incident Response Playbook — When AI Goes Wrong

> **Disclaimer**: This document provides general guidance — not legal advice. See [LEGAL_NOTICE.md](/LEGAL_NOTICE.md) for full terms.

> Your AI system will eventually produce an output that makes someone very unhappy.
> The question is not *if* but *when*, and whether you'll have a plan or just panic.

This playbook covers how to classify, respond to, and report AI incidents under the
EU AI Act — and how to handle the 99% of incidents that don't require a formal report
but still require your full attention.

---

## What Counts as an "AI Incident"

An AI incident is any event where your AI system behaves in a way that causes or
could cause harm, violates requirements, or degrades trust. Specifically:

- **Bias detected**: The system produces discriminatory outputs against protected groups.
- **Harmful output**: The system generates dangerous, illegal, or deeply inappropriate content.
- **Data leak via AI**: The system exposes personal data, confidential information, or training data through its outputs.
- **Availability failure**: The system becomes unavailable or unresponsive when people depend on it.
- **Systematic errors**: The system consistently produces incorrect results in a specific domain or for a specific population.
- **Unauthorized capability**: The system performs actions beyond its intended scope.
- **Feedback loop degradation**: The system's performance degrades over time due to self-reinforcing errors.

Not every bug is an incident. A typo in a chatbot response is a bug. A chatbot that
systematically refuses service to users with non-Western names is an incident.

---

## Incident Severity Classification

### P0 — Critical

**Definition**: Imminent or actual serious harm to persons, fundamental rights, safety,
or the environment. System must be stopped immediately.

**Examples**:
- Medical AI recommends a drug dosage that could be lethal
- Hiring AI systematically rejects candidates of a specific ethnicity
- AI system leaks personal data of thousands of users in outputs
- Safety-critical AI (e.g., infrastructure monitoring) produces false negatives

**Response time**: Immediately. Drop everything.

### P1 — High

**Definition**: Significant harm has occurred or is likely. Affects many users or
involves sensitive categories. Requires urgent action within hours.

**Examples**:
- Content moderation AI consistently fails to flag harmful content in a specific language
- Financial AI produces systematically biased credit assessments
- AI assistant provides dangerously incorrect medical or legal advice to multiple users
- Data processing violation discovered (e.g., prompts stored without consent)

**Response time**: Within 2 hours of detection.

### P2 — Medium

**Definition**: Moderate impact. Affects a subset of users or produces incorrect but
not dangerous outputs. Requires action within days.

**Examples**:
- Translation AI consistently mistranslates a specific language pair
- Recommendation system shows clear but non-discriminatory bias (e.g., recency bias)
- AI outputs contain hallucinated citations that could mislead researchers
- Performance degradation affects response quality for a specific use case

**Response time**: Within 24 hours of detection.

### P3 — Low

**Definition**: Minor issues. Single-user complaints, cosmetic errors, edge cases.
Track and batch-fix.

**Examples**:
- Chatbot occasionally gives an irrelevant response to an unusual query
- Formatting errors in AI-generated documents
- Minor inconsistencies in AI explanations
- Single user reports an unexpected output

**Response time**: Within 1 week. Track in issue backlog.

---

## Response Procedures by Severity

### P0 Response Procedure

1. **Activate kill switch** — Remove the system from production or switch to fallback. No debate.
2. **Notify incident commander** — A named person owns the incident from this moment.
3. **Assess Art. 73 applicability** — Does this qualify as a serious incident? (See below.)
4. **Preserve all evidence** — Logs, inputs, outputs, model version, timestamps. Lock them down.
5. **Notify affected parties** — Users, deployers, downstream systems. Immediately.
6. **Begin root cause analysis** — Assemble the relevant team within 1 hour.
7. **Report to authorities** — If Art. 73 applies, begin the formal reporting process.
8. **Communicate externally** — Prepare public statement if the incident is visible or affects many.
9. **Implement fix and validate** — Do not restore service until the fix is verified.
10. **Conduct post-incident review** — Within 5 business days.

### P1 Response Procedure

1. **Implement immediate mitigation** — Rate limiting, output filtering, feature flag, partial rollback.
2. **Notify incident commander** and relevant team leads.
3. **Assess Art. 73 applicability** — Probably not, but check.
4. **Preserve evidence** — Logs, affected user data, model state.
5. **Notify affected users** — Within 24 hours.
6. **Root cause analysis** — Begin within 4 hours.
7. **Deploy fix** — Within 48 hours.
8. **Post-incident review** — Within 10 business days.

### P2 Response Procedure

1. **Document the issue** with full context and reproduction steps.
2. **Implement workaround** if available (prompt adjustment, output filter, user guidance).
3. **Prioritize fix** in current sprint.
4. **Notify affected users** if they reported the issue.
5. **Deploy fix and monitor** for recurrence.

### P3 Response Procedure

1. **Log the issue** in the incident tracker.
2. **Assess patterns** — Is this the third "low" incident of the same type? Upgrade.
3. **Schedule fix** in upcoming sprint.
4. **Close with documentation**.

---

## Art. 73 — Serious Incident Reporting

### When Is Reporting Required?

Art. 73 requires providers of high-risk AI systems to report **serious incidents** to
the market surveillance authority of the Member State where the incident occurred.

A "serious incident" is an incident that directly or indirectly leads to any of the following:

| Trigger | Examples |
|---------|----------|
| **Death of a person** | AI-controlled system causes fatal accident |
| **Serious damage to health** | Medical AI misdiagnosis leads to incorrect treatment |
| **Serious damage to safety** | Infrastructure AI fails to detect danger |
| **Serious damage to fundamental rights** | Systematic discrimination by public-sector AI |
| **Serious damage to property** | AI trading system causes massive financial loss |
| **Serious damage to the environment** | AI-controlled industrial process causes pollution |

### Reporting Deadline

- **Maximum 15 days** after the provider (or deployer, who must inform the provider) becomes
  aware of the causal link between the AI system and the serious incident.
- If the incident involves a **widespread infringement** affecting multiple Member States,
  report to the authority of the Member State where the incident occurred.
- For **imminent danger**: report immediately, even if information is incomplete. Supplement later.

### Who to Report To

- The **market surveillance authority** of the Member State where the incident occurred.
- Each Member State designates its own authority. Check the EU AI Office database for the
  current list.
- If the incident occurred in multiple Member States, report to each relevant authority.

### Practical Guidance

Most AI product incidents are NOT Art. 73 serious incidents — but document everything anyway.

Your chatbot hallucinating a fake restaurant recommendation is not a serious incident.
Your chatbot systematically providing dangerous medical advice that leads to
hospitalization is. The line between "embarrassing" and "serious" is whether actual
serious harm occurred or was directly risked.

When in doubt, err on the side of reporting. An unnecessary report is a minor
inconvenience. A missed mandatory report is a compliance violation.

---

## Serious Incident Report Template

Per Art. 73 requirements, a serious incident report must include:

```markdown
# Serious Incident Report — [System Name]

## 1. Provider Information
- Provider name:
- Provider address:
- Contact person:
- EU representative (if applicable):

## 2. AI System Identification
- System name and version:
- CE marking / conformity info:
- Intended purpose:
- Risk classification:
- Date system was placed on market / put into service:

## 3. Incident Description
- Date and time of incident:
- Date provider became aware of causal link:
- Location (Member State):
- Description of the incident:
- Number of persons affected:
- Nature of harm (death / health / safety / rights / property / environment):

## 4. Causal Analysis
- How the AI system contributed to the incident:
- Input data involved (if relevant):
- System behavior observed:
- Was the system operating within intended purpose?

## 5. Immediate Actions Taken
- Mitigation measures applied:
- Was the system withdrawn / recalled / disabled?
- Users / deployers notified? When?

## 6. Corrective Actions Planned
- Root cause identified?
- Fix timeline:
- Preventive measures:

## 7. Attachments
- Relevant logs
- Technical documentation excerpts
- Previous risk assessment (relevant sections)
```

---

## Communication Templates

### To Users (P0/P1)

> Subject: Important Notice — [System Name] Service Issue
>
> We have identified an issue with [System Name] that may have affected
> [description of impact]. We have [taken action: suspended the service /
> implemented safeguards / etc.].
>
> What this means for you: [specific user impact].
> What we are doing: [corrective actions].
> What you should do: [user actions if any].
>
> We take this matter seriously and will provide updates as our investigation
> progresses. Contact [support channel] with questions.

### To Market Surveillance Authority

Use the Serious Incident Report Template above. Be factual, complete, and avoid
speculative language. If information is still incomplete, state what you know and
commit to a timeline for supplementary information.

### To Press / Public (P0 only, if visible)

> [Company] has identified and addressed an issue with its [System Name] AI system.
> [Brief factual description]. We have [actions taken]. [Number] users were affected.
> We are cooperating fully with relevant authorities. We have implemented [preventive
> measures] to prevent recurrence.

Keep it short, factual, and avoid technical jargon. Never speculate about causes
before the root cause analysis is complete.

---

## Root Cause Analysis Template

```markdown
# Root Cause Analysis — [Incident ID]

## Timeline
| Time | Event |
|------|-------|
| ... | Incident occurred |
| ... | Incident detected |
| ... | Response initiated |
| ... | Mitigation applied |
| ... | Root cause identified |
| ... | Fix deployed |

## The Five Whys
1. Why did the incident occur?
2. Why did that happen?
3. Why did that happen?
4. Why did that happen?
5. Why did that happen?

## Contributing Factors
- [ ] Training data issue
- [ ] Model behavior change (drift, emergent behavior)
- [ ] Input validation failure
- [ ] Missing guardrail / output filter
- [ ] Infrastructure / availability issue
- [ ] Human oversight gap
- [ ] Third-party dependency failure
- [ ] Deployment / configuration error

## Corrective Actions
| Action | Owner | Deadline | Status |
|--------|-------|----------|--------|
| ... | ... | ... | ... |
```

---

## Post-Incident Review Checklist

- [ ] Timeline of events is documented and verified
- [ ] Root cause is identified (not just symptoms)
- [ ] All affected users have been notified
- [ ] Art. 73 applicability was assessed and documented
- [ ] If Art. 73 applies: report filed within deadline
- [ ] Corrective actions are assigned with owners and deadlines
- [ ] Risk assessment is updated to reflect the incident
- [ ] Monitoring is enhanced to detect similar incidents earlier
- [ ] Technical documentation is updated
- [ ] Lessons learned are shared with the team
- [ ] Incident is logged in the post-market monitoring system
- [ ] If the system was stopped: restart criteria are defined and met

---

## When to Trigger the Kill Switch

Pull the plug — no meetings, no approvals — when:

- The system is causing or may imminently cause physical harm
- The system is leaking personal data at scale
- The system is producing systematically discriminatory outputs and you cannot filter them
- A P0 incident is confirmed and no effective mitigation exists short of shutdown
- A market surveillance authority orders you to stop

Reactivation requires:
1. Root cause identified and fixed
2. Fix validated in staging environment
3. Risk assessment updated
4. Incident commander and DPO sign off
5. Gradual rollout with enhanced monitoring

The kill switch is not a failure. It is your most important safety feature.
Using it when needed is competence. Not using it when needed is negligence.
