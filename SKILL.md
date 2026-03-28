---
name: ai-act-compliance
description: |
  EU AI Act compliance checker and documentation generator for SaaS products built with AI APIs (Claude, OpenAI, etc.) and vibe coding workflows. Use this skill whenever: building a new AI-powered feature or SaaS product, reviewing an existing codebase for AI Act compliance, generating compliance documentation (technical docs, transparency disclosures, risk assessments), adding a chatbot/AI assistant to any product, integrating AI APIs into user-facing applications, preparing for an AI Act audit, classifying AI system risk level, writing privacy policies or terms of service for AI products, deploying AI features to EU markets, or when the user mentions "AI Act", "compliance", "transparency", "GPAI", "high-risk AI", "Article 50", or "CE marking". Also trigger when reviewing system prompts, AI-generated content labeling, or any discussion about AI regulation in Europe.
---

# EU AI Act Compliance Skill

This skill helps you build AI-powered SaaS products that comply with the EU AI Act (Regulation EU 2024/1689). It provides actionable guidance during development, generates compliance documentation, and ensures your products meet all regulatory requirements before deployment.

## Quick Reference: Who Are You Under the AI Act?

Before anything else, determine your role. This drives all obligations.

### You are a PROVIDER if you:
- Write system prompts that define how an AI model behaves in your product
- Integrate AI models via API into user-facing applications
- Build SaaS products that use AI to generate content, make decisions, or interact with users
- White-label or substantially modify an AI system

**This means most SaaS builders using Claude API, OpenAI API, etc. are PROVIDERS — not deployers.**

### You are a DEPLOYER if you:
- Use an AI tool as-is without modification (e.g., using ChatGPT directly)
- Don't define system prompts or customize AI behavior

### You are NOT a GPAI Model Provider if you:
- Don't train foundation models
- Only consume models via API

**Important**: Being a "system provider" (not a model provider) means Art. 53 GPAI obligations don't apply to you, but Art. 50 transparency obligations absolutely do.

## Risk Classification Workflow

Run this classification for every AI feature in your product.

### Step 1: Check Prohibited Practices (Art. 5)
Verify your system does NOT:
- Use subliminal manipulation techniques
- Exploit vulnerabilities of specific groups
- Perform social scoring
- Use real-time remote biometric identification in public spaces (with narrow exceptions)
- Perform emotion recognition in workplace/education (with narrow exceptions)
- Do untargeted scraping of facial images for facial recognition databases
- Infer emotions in workplace or education unless for medical/safety reasons

If any apply → STOP. The practice is banned since Feb 2, 2025.

### Step 2: Check High-Risk (Annex III)
Does your AI system operate in any of these domains?

1. **Biometrics** — remote biometric identification, emotion recognition
2. **Critical infrastructure** — energy, transport, water, gas, electricity management
3. **Education** — exam scoring, admission decisions, learning assessment
4. **Employment** — recruitment, CV screening, performance evaluation, promotion/termination decisions
5. **Essential services** — creditworthiness assessment, insurance pricing, emergency services prioritization, social benefits eligibility
6. **Law enforcement** — evidence evaluation, crime prediction, profiling
7. **Migration** — visa assessment, border control
8. **Justice & democracy** — legal research tools influencing decisions, election-related AI

If YES → High-risk. Read `references/high-risk-requirements.md`.
If NO → Continue to Step 3.

### Step 3: Transparency Risk (Art. 50)
Does your system do any of these?
- Interact directly with humans (chatbots, assistants, conversational AI)
- Generate synthetic text, images, audio, or video
- Perform emotion recognition or biometric categorization
- Generate or manipulate deepfakes

If YES → Limited risk with transparency obligations. This is the most common case for SaaS builders.
If NO → Minimal risk, no specific obligations (but AI literacy still applies).

## Compliance Requirements by Category

### For ALL AI Systems (since Feb 2, 2025)

**AI Literacy (Art. 4)**
- Ensure your team has sufficient AI literacy
- Document training provided to staff involved in AI development and deployment
- Keep records of AI literacy initiatives

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

#### 1. Human Interaction Disclosure (Art. 50.1)
If your AI system interacts with users, inform them they're talking to AI.

**Implementation checklist:**
- [ ] Add visible AI disclosure in UI (before first interaction)
- [ ] Disclosure must be "clear and distinguishable" — not hidden in ToS
- [ ] Exception: if it's "obvious from the circumstances" (rare for chatbots)

**Code pattern:**
```typescript
// Example: AI disclosure component
const AIDisclosure = () => (
  <div role="status" aria-label="AI disclosure" className="ai-disclosure">
    Stai parlando con un assistente basato su intelligenza artificiale.
    Le risposte sono generate automaticamente e potrebbero non essere sempre accurate.
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

#### 2. Synthetic Content Marking (Art. 50.2)
If your system generates text, images, audio, or video:

**Implementation checklist:**
- [ ] Mark outputs as AI-generated in machine-readable format
- [ ] Implement detection mechanisms for downstream systems
- [ ] Use metadata tagging (C2PA, IPTC, or similar standards)
- [ ] Exception: "assistive function" that doesn't substantially alter user input

**Code pattern:**
```typescript
// Example: Content metadata marking
interface AIContentMetadata {
  ai_generated: boolean;
  model_provider: string;      // e.g., "Anthropic Claude"
  system_name: string;         // e.g., "Lucia by Studio121"
  generation_date: string;     // ISO 8601
  content_type: 'text' | 'image' | 'audio' | 'video';
  human_edited: boolean;       // true if human reviewed/modified
}

function markAIContent(content: string, metadata: AIContentMetadata): string {
  // Add machine-readable marker
  return `<!-- AI-GENERATED: ${JSON.stringify(metadata)} -->\n${content}`;
}
```

```python
# Example: AI content watermarking for API responses
def mark_ai_response(response_text, system_name):
    metadata = {
        "ai_generated": True,
        "provider": "Anthropic Claude API",
        "system": system_name,
        "timestamp": datetime.utcnow().isoformat(),
        "regulation": "EU AI Act Art. 50(2)"
    }
    return {
        "content": response_text,
        "ai_metadata": metadata,
        "disclosure": "Questo contenuto è stato generato con l'ausilio dell'intelligenza artificiale."
    }
```

#### 3. Deepfake Disclosure (Art. 50.4)
If your system generates or manipulates images/audio/video resembling real people:
- [ ] Disclose that content is artificially generated or manipulated
- [ ] Exception: artistic, creative, satirical, or fictional works (but still must disclose existence)

#### 4. AI-Generated Text for Public Interest (Art. 50.4)
If your system generates text published to inform the public:
- [ ] Disclose that text was artificially generated or manipulated
- [ ] Exception: if human editorial oversight reviewed and takes responsibility

### For HIGH-RISK Systems — Read `references/high-risk-requirements.md`

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

### 8. Copyright Compliance
- **Training data**: [N/A for API consumers — handled by model provider]
- **Output monitoring**: [How you handle potential copyright issues in outputs]

### 9. Contact
- **AI Act compliance contact**: [Name, email]
- **DPO**: [If applicable]
```

### Privacy Policy AI Addendum (Italian)

```markdown
## Utilizzo dell'Intelligenza Artificiale

Il presente servizio utilizza sistemi di intelligenza artificiale per [DESCRIZIONE FUNZIONALITÀ].

**Modello AI utilizzato**: Il servizio si avvale di [NOME MODELLO] fornito da [PROVIDER],
integrato tramite API nel nostro sistema.

**Trasparenza**: I contenuti generati dall'intelligenza artificiale sono contrassegnati
come tali. Quando interagisci con il nostro assistente virtuale, stai comunicando con
un sistema automatizzato basato su AI, non con un operatore umano.

**Dati trattati**: Per fornire il servizio, i seguenti dati vengono elaborati dal
sistema AI: [ELENCO DATI]. I dati sono trattati in conformità al GDPR (Reg. UE 2016/679)
e alla nostra Informativa Privacy.

**Limitazioni**: Le risposte generate dall'AI potrebbero contenere imprecisioni.
Le informazioni fornite non sostituiscono la consulenza professionale di
[TIPO PROFESSIONISTA RILEVANTE].

**Supervisione umana**: [DESCRIZIONE MECCANISMO DI OVERSIGHT].

**Diritti dell'utente**: Hai il diritto di richiedere che le decisioni che ti riguardano
non siano basate esclusivamente su trattamenti automatizzati (Art. 22 GDPR).
```

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

## Common SaaS Scenarios

### Chatbot / Virtual Assistant (e.g., Lucia, Riciclabolario)
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

### AI Document Analysis / Extraction (e.g., your bilancio extractor)
- **Classification**: Depends on use
  - General document processing → Minimal/Limited risk
  - If used for creditworthiness or financial decisions → HIGH RISK (Annex III)
- **Key obligations**: Ensure human reviews extracted data before consequential decisions

## Penalties Quick Reference

| Violation | Max Fine |
|-----------|----------|
| Prohibited practices | €35M or 7% global turnover |
| High-risk system obligations | €15M or 3% global turnover |
| Incorrect information to authorities | €7.5M or 1% global turnover |

SMEs benefit from the lower of the two thresholds (fixed amount vs. percentage).

## Key Dates

| Date | What |
|------|------|
| Feb 2, 2025 | ✅ Prohibited practices + AI literacy — ALREADY IN FORCE |
| Aug 2, 2025 | ✅ GPAI model obligations — ALREADY IN FORCE |
| **Aug 2, 2026** | **⚠️ Full application: Art. 50 transparency + high-risk (Annex III standalone)** |
| Aug 2, 2027 | High-risk in regulated products (medical devices, machinery, etc.) |

## References

For detailed requirements on specific topics, read:
- `references/checklist-completa.md` — **Checklist esaustiva articolo per articolo** con 150+ punti di verifica, organizzata per fase (governance → classificazione → sviluppo → pre-deploy → post-deploy) + requisiti aggiuntivi high-risk
- `references/high-risk-requirements.md` — Full high-risk system obligations (Arts. 9-15)
- `references/transparency-implementation.md` — Technical guidance for Art. 50 implementation with code patterns
- `references/italian-context.md` — Italy-specific implementation notes (Garante, AgID, ACN), template in italiano
- `references/auto-update.md` — **Workflow di auto-aggiornamento**: fonti da monitorare, frequenza raccomandata, changelog

## Auto-Aggiornamento

Per aggiornare la skill con le ultime novità normative, chiedi a Claude:
```
Aggiorna la skill AI Act compliance con le ultime novità normative.
```
Claude seguirà il workflow in `references/auto-update.md`: cercherà aggiornamenti dalle fonti primarie EU e italiane, e aggiornerà i file della skill di conseguenza.

## Integration with Your Workflow

When building with Claude Code or vibe coding:

1. **At project start**: Run the risk classification workflow above
2. **Add `AI_ACT_COMPLIANCE.md`** to your project root from the template
3. **Add the pre-deploy checklist** to your CI/CD or release process
4. **Every new AI feature**: Re-run classification, update documentation
5. **Before launch**: Complete the full pre-deploy checklist
6. **Post-launch**: Set quarterly compliance review reminders

Remember: documentation is your best defense. If audited, you need to show you assessed risks, classified correctly, and implemented appropriate measures.
