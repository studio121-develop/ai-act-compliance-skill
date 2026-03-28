---
name: ai-act-compliance
description: |
  EU AI Act compliance checker and documentation generator for SaaS products built with AI APIs (Claude, OpenAI, etc.) and vibe coding workflows. Use this skill whenever: building a new AI-powered feature or SaaS product, reviewing an existing codebase for AI Act compliance, generating compliance documentation (technical docs, transparency disclosures, risk assessments), adding a chatbot/AI assistant to any product, integrating AI APIs into user-facing applications, preparing for an AI Act audit, classifying AI system risk level, writing privacy policies or terms of service for AI products, deploying AI features to EU markets, or when the user mentions "AI Act", "compliance", "transparency", "GPAI", "high-risk AI", "Article 50", or "CE marking". Also trigger when reviewing system prompts, AI-generated content labeling, or any discussion about AI regulation in Europe.
---

<!-- Last verified against EUR-Lex: 2026-03-28 -->

# EU AI Act Compliance Skill

> **Important**: This skill provides general informational guidance — not legal advice. It does not guarantee compliance with any regulation. See [LEGAL_NOTICE.md](LEGAL_NOTICE.md) for full terms. Always consult a qualified legal professional for your specific situation.

This skill helps you build AI-powered SaaS products that comply with the EU AI Act (Regulation EU 2024/1689). It provides actionable guidance during development, generates compliance documentation, and helps you assess regulatory requirements before deployment.

## Quick Reference: Who Are You Under the AI Act?

Before anything else, determine your role. This drives all obligations.

### You are a PROVIDER if you:
- Write system prompts that define how an AI model behaves in your product
- Integrate AI models via API into user-facing applications
- Build SaaS products that use AI to generate content, make decisions, or interact with users
- White-label or substantially modify an AI system (Art. 25 — see `references/value-chain-obligations.md`)

**This means most SaaS builders using Claude API, OpenAI API, etc. are PROVIDERS — not deployers.** (See Recitals 25-27 for the reasoning behind this classification.)

### You are a DEPLOYER if you:
- Use an AI tool as-is without modification (e.g., using ChatGPT directly)
- Don't define system prompts or customize AI behavior
- For deployer obligations, see `references/deployer-obligations.md`

### About GPAI Model Providers (Arts. 51-56):
- If you only consume models via API: Art. 53 GPAI obligations do **not** apply to you
- If you fine-tune models, train LoRA adapters, or otherwise modify the model itself: you **may** become a GPAI model provider — see `references/gpai-obligations.md`
- Art. 50 transparency obligations apply to you regardless

## Risk Classification Workflow

Run this classification for every AI feature in your product.

### Step 1: Check Prohibited Practices (Art. 5)
Verify your system does NOT:
- Use subliminal manipulation techniques (Recital 29)
- Exploit vulnerabilities of specific groups (age, disability, social situation)
- Perform social scoring (Recital 31)
- Use real-time remote biometric identification in public spaces (narrow exceptions in Art. 5(2))
- Perform emotion recognition in workplace/education (exceptions for medical/safety — Recital 44)
- Do untargeted scraping of facial images for facial recognition databases
- Infer emotions in workplace or education unless for medical/safety reasons
- Use predictive policing based solely on profiling (Recital 42)

If any apply → STOP. The practice is banned since Feb 2, 2025.

### Step 2: Check High-Risk (Annex III)
Does your AI system operate in any of these domains?

1. **Biometrics** — remote biometric identification, emotion recognition
2. **Critical infrastructure** — energy, transport, water, gas, electricity management
3. **Education** — exam scoring, admission decisions, learning assessment (see `references/sectors/edtech.md`)
4. **Employment** — recruitment, CV screening, performance evaluation, promotion/termination (see `references/sectors/hrtech.md`)
5. **Essential services** — creditworthiness, insurance pricing, emergency dispatch, social benefits (see `references/sectors/fintech.md`)
6. **Law enforcement** — evidence evaluation, crime prediction, profiling
7. **Migration** — visa assessment, border control
8. **Justice & democracy** — legal research tools influencing decisions, election AI (see `references/sectors/legaltech.md`)

If YES → check Art. 6(3) derogation first. If system profiles individuals, derogation does NOT apply — always high-risk.
Read `references/high-risk-requirements.md` for full obligations.
If NO → Continue to Step 3.

### Step 3: Transparency Risk (Art. 50)
Does your system do any of these?
- Interact directly with humans (chatbots, assistants, conversational AI)
- Generate synthetic text, images, audio, or video
- Perform emotion recognition or biometric categorization
- Generate or manipulate deepfakes

If YES → Limited risk with transparency obligations. This is the most common case for SaaS builders.
If NO → Minimal risk, no specific obligations (but AI literacy still applies).

For interactive risk classification, see `references/decision-trees/risk-classification.md`.

## Compliance Requirements by Category

### For ALL AI Systems (since Feb 2, 2025)

**AI Literacy (Art. 4)** (Recital 20)
- Ensure your team has sufficient AI literacy
- Document training provided to staff involved in AI development and deployment
- Keep records of AI literacy initiatives
- Extend to freelancers and external collaborators involved in AI work

**Action items for your codebase:**
```
// Add to your project README or CLAUDE.md
## AI Act Compliance
- Risk classification: [MINIMAL | LIMITED | HIGH]
- Classification date: [DATE]
- Classification rationale: [WHY]
- AI literacy training: [DOCUMENTED]
```

### For LIMITED RISK Systems (Art. 50) — Deadline: Aug 2, 2026

This is where most SaaS products with AI features land. Requirements:

#### 1. Human Interaction Disclosure (Art. 50.1) (Recitals 132-133)
If your AI system interacts with users, inform them they're talking to AI.

**Implementation checklist:**
- [ ] Add visible AI disclosure in UI (before first interaction)
- [ ] Disclosure must be "clear and distinguishable" — not hidden in ToS
- [ ] Exception: if it's "obvious from the circumstances" (rare for chatbots — when in doubt, disclose)

**Code pattern:**
```typescript
// Example: AI disclosure component
const AIDisclosure = () => (
  <div role="status" aria-label="AI disclosure" className="ai-disclosure">
    You are interacting with an AI-powered assistant.
    Responses are generated automatically and may not always be accurate.
  </div>
);
```

```python
# Example: API response header
def add_ai_disclosure(response):
    response.headers['X-AI-Generated'] = 'true'
    response.headers['X-AI-System'] = 'Claude API via [Your Product Name]'
    return response
```

For comprehensive implementation patterns, see `references/transparency-implementation.md` and framework-specific guides in `references/patterns/`.

#### 2. Synthetic Content Marking (Art. 50.2) (Recitals 133-134)
If your system generates text, images, audio, or video:

**Implementation checklist:**
- [ ] Mark outputs as AI-generated in machine-readable format
- [ ] Implement detection mechanisms for downstream systems
- [ ] Use metadata tagging (C2PA, IPTC, or similar standards — see `references/patterns/c2pa.md`)
- [ ] Exception: "assistive function" that doesn't substantially alter user input (spell-check, grammar correction)

**Code pattern:**
```typescript
// Example: Content metadata marking
interface AIContentMetadata {
  ai_generated: boolean;
  model_provider: string;      // e.g., "Anthropic Claude"
  system_name: string;         // your product name
  generation_date: string;     // ISO 8601
  content_type: 'text' | 'image' | 'audio' | 'video';
  human_edited: boolean;       // true if human reviewed/modified
}

function markAIContent(content: string, metadata: AIContentMetadata): string {
  return `<!-- AI-GENERATED: ${JSON.stringify(metadata)} -->\n${content}`;
}
```

#### 3. Deepfake Disclosure (Art. 50.4) (Recital 136)
If your system generates or manipulates images/audio/video resembling real people:
- [ ] Disclose that content is artificially generated or manipulated
- [ ] Exception: artistic, creative, satirical, or fictional works (but still must disclose existence)

#### 4. AI-Generated Text for Public Interest (Art. 50.4) (Recital 137)
If your system generates text published to inform the public:
- [ ] Disclose that text was artificially generated or manipulated
- [ ] Exception: if human editorial oversight reviewed and takes responsibility

### For HIGH-RISK Systems

Read `references/high-risk-requirements.md` for full Arts. 9-17 obligations.
For Annex IV technical documentation, use `references/annex-iv-template.md`.
For conformity assessment walkthrough, see `references/conformity-assessment.md`.

### Voluntary Compliance (Art. 95)

Even if your system is not high-risk, you can voluntarily adopt high-risk practices. This signals trust to enterprise customers, may give you a head start if your system's classification changes, and can be a competitive advantage. See also the codes of conduct that industry associations may develop under Art. 95.

## Documentation Templates

### Technical Documentation Template (for your product)

Create a file called `AI_ACT_COMPLIANCE.md` in your project root:

```markdown
# AI Act Compliance Documentation
## Product: [Name]
## Version: [X.Y.Z]
## Last Updated: [Date]

### 1. System Description
- **Purpose**: [What the AI system does]
- **Intended use**: [How it should be used]
- **Not intended for**: [Explicit exclusions]
- **Target users**: [Who uses it]
- **Geographic scope**: [Where it's available]

### 2. Risk Classification
- **Classification**: [Minimal | Limited | High]
- **Rationale**: [Why this classification]
- **Annex III check**: [Which categories checked, why N/A]
- **Art. 6(3) derogation**: [If applicable, why system is not high-risk despite Annex III listing]

### 3. AI Model Information
- **Model provider**: [e.g., Anthropic]
- **Model name**: [e.g., Claude Sonnet 4]
- **Integration method**: [API / SDK / embedded]
- **System prompt**: [Summary of behavior instructions — NOT the full prompt for IP reasons]
- **Data processed**: [What user data is sent to the model]
- **Data retention**: [Model provider's data policy + your retention policy]

### 4. Transparency Measures
- **User disclosure**: [How users are informed they interact with AI]
- **Content marking**: [How AI-generated content is labeled]
- **Machine-readable marking**: [Technical implementation details]

### 5. Data Governance
- **Input data**: [What data the system processes]
- **Personal data**: [GDPR compliance cross-reference]
- **Data minimization**: [What data is NOT sent to the model]
- **User consent**: [How consent is obtained]

### 6. Human Oversight
- **Oversight mechanism**: [How humans can review/override AI decisions]
- **Escalation path**: [When and how AI decisions are escalated to humans]
- **Kill switch**: [How to disable AI features if needed]

### 7. Risk Management
- **Identified risks**: [What could go wrong]
- **Mitigation measures**: [What you do about it]
- **Monitoring**: [How you track issues post-deployment]
- **Incident response**: [What happens when something goes wrong]

### 8. Value Chain
- **Upstream provider**: [Model provider, DPA status]
- **Downstream deployers**: [If B2B — what information provided to deployers]

### 9. Contact
- **AI Act compliance contact**: [Name, email]
- **DPO**: [If applicable]
```

For high-risk systems, use the more detailed Annex IV template in `references/annex-iv-template.md`.

## Pre-Deployment Checklist

Run this checklist before every deployment of an AI-powered feature:

```
## AI Act Pre-Deploy Checklist — [Product Name] v[X.Y.Z]

### Classification
- [ ] Risk classification documented and up to date
- [ ] Prohibited practices check completed (Art. 5)
- [ ] Annex III categories reviewed

### Transparency (Art. 50)
- [ ] AI interaction disclosure visible in UI
- [ ] AI-generated content marked (machine-readable)
- [ ] Deepfake disclosure (if applicable)
- [ ] AI text disclosure for public interest content (if applicable)

### Documentation
- [ ] AI_ACT_COMPLIANCE.md updated
- [ ] Privacy policy AI addendum in place
- [ ] Terms of service updated with AI usage

### Data & Privacy
- [ ] GDPR compliance verified
- [ ] Data minimization applied (only necessary data sent to AI)
- [ ] User consent mechanism in place
- [ ] Data processing agreement with AI provider (e.g., Anthropic DPA)

### Technical
- [ ] Human oversight mechanism functional
- [ ] AI feature kill switch tested
- [ ] Error handling for AI failures implemented
- [ ] Logging of AI interactions enabled (for compliance audit trail)
- [ ] Rate limiting and abuse prevention in place

### Operations
- [ ] AI literacy training documented for team
- [ ] Incident response plan for AI-related issues
- [ ] Post-market monitoring plan defined
- [ ] Compliance review scheduled (quarterly recommended)
```

For the full 219-point checklist by lifecycle phase, see `references/checklist.md`.

## Common SaaS Scenarios

### Chatbot / Virtual Assistant
- **Classification**: Limited risk (Art. 50)
- **Key obligations**: Inform users it's AI, mark generated content
- **NOT high-risk** unless it makes decisions about employment, credit, education, etc.

### AI Content Generation Tool
- **Classification**: Limited risk (Art. 50)
- **Key obligations**: Mark outputs as AI-generated (machine-readable + visible)
- **Watch out**: If content is published for public interest → additional disclosure

### AI-Powered Search / Recommendation
- **Classification**: Typically minimal risk
- **Key obligations**: None specific, but AI literacy and good practices apply
- **Becomes high-risk if**: Recommendations influence essential services access

### AI Document Analysis / Extraction
- **Classification**: Depends on use
  - General document processing → Minimal/Limited risk
  - If used for creditworthiness or financial decisions → HIGH RISK (Annex III)
- **Key obligations**: Ensure human reviews extracted data before consequential decisions

## Penalties Quick Reference

| Violation | Max Fine | Article |
|-----------|----------|---------|
| Prohibited practices | €35M or 7% global turnover | Art. 99(3) |
| High-risk system obligations | €15M or 3% global turnover | Art. 99(4) |
| Incorrect information to authorities | €7.5M or 1% global turnover | Art. 99(5) |

SMEs and startups: the applicable fine is the lower of the two thresholds (fixed amount vs. percentage). See Art. 99(6).

## Key Dates

| Date | What |
|------|------|
| Feb 2, 2025 | Prohibited practices + AI literacy — IN FORCE |
| Aug 2, 2025 | GPAI model obligations — IN FORCE |
| **Aug 2, 2026** | **Full application: Art. 50 transparency + high-risk (Annex III standalone)** |
| Aug 2, 2027 | High-risk in regulated products (medical devices, machinery, etc.) |

## Available Commands

You can ask for specific workflows:

| Command | What it does |
|---------|-------------|
| `Classify the AI Act risk level of [feature/product]` | Interactive risk classification |
| `Generate AI Act compliance documentation` | Fill in the documentation template for your project |
| `Run AI Act pre-deploy checklist` | Execute the pre-deployment checklist |
| `Audit my codebase for AI Act compliance` | Scan for compliance gaps (disclosure, marking, logging) |
| `Compare my compliance to [sector] requirements` | Sector-specific analysis |
| `Update the AI Act compliance skill` | Check for regulatory updates |
| `Help me prepare for an AI Act audit` | Audit preparation walkthrough |

## References

For detailed requirements on specific topics:

**Core references:**
- `references/checklist.md` — 219 verification points by lifecycle phase
- `references/high-risk-requirements.md` — Full high-risk system obligations (Arts. 9-17)
- `references/transparency-implementation.md` — Technical guidance for Art. 50 with code patterns
- `references/auto-update.md` — Regulatory update workflow with sources and schedule

**Regulatory depth:**
- `references/value-chain-obligations.md` — Value chain responsibilities (Arts. 22-28)
- `references/deployer-obligations.md` — Deployer obligations and FRIA (Arts. 26-27)
- `references/gpai-obligations.md` — GPAI model provider obligations (Arts. 51-56)
- `references/regulatory-sandbox.md` — Regulatory sandboxes (Arts. 57-62)
- `references/annex-iv-template.md` — Annex IV technical documentation template
- `references/conformity-assessment.md` — Conformity assessment walkthrough
- `references/incident-response.md` — Incident response playbook
- `references/standards-tracker.md` — Harmonized standards tracking
- `references/provider-comparison.md` — AI provider comparison matrix

**National contexts:**
- `references/national/italy.md` — Italy (Garante, AgID, ACN)
- `references/national/germany.md` — Germany (BfDI, BSI, BNetzA)
- `references/national/france.md` — France (CNIL, ANSSI)
- `references/national/spain.md` — Spain (AEPD, first EU sandbox)
- `references/national/netherlands.md` — Netherlands (AP, Algorithm Register)

**Code patterns by framework:**
- `references/patterns/nextjs.md`, `fastapi.md`, `django.md`, `go.md`, `spring-boot.md`, `dotnet.md`
- `references/patterns/cicd.md` — CI/CD compliance automation
- `references/patterns/testing.md` — Compliance testing patterns
- `references/patterns/c2pa.md` — Content provenance implementation

**Sector-specific guides:**
- `references/sectors/fintech.md`, `healthtech.md`, `edtech.md`, `hrtech.md`, `legaltech.md`

## Keeping Current

Ask Claude to update the skill with the latest regulatory developments:
```
Update the AI Act compliance skill with the latest regulatory news.
```
Claude will follow the workflow in `references/auto-update.md`: search primary EU and national sources, update files, and log changes. Recommended: monthly until August 2026, quarterly after.

## Integration with Your Workflow

1. **At project start**: Run the risk classification workflow above
2. **Add `AI_ACT_COMPLIANCE.md`** to your project root from the template
3. **Add the pre-deploy checklist** to your CI/CD (see `references/patterns/cicd.md`)
4. **Every new AI feature**: Re-run classification, update documentation
5. **Before launch**: Complete the full pre-deploy checklist
6. **Post-launch**: Set quarterly compliance review reminders, monitor for regulatory updates

Documentation is your best defense. If audited, you need to show you assessed risks, classified correctly, and implemented appropriate measures. This skill helps you build that evidence — but the responsibility for compliance remains yours.
