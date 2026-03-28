<!-- Last verified against EUR-Lex: 2026-03-28 -->

# AI Provider Comparison — Compliance Edition

> Choosing an AI provider used to be about latency, cost, and model quality.
> Now it's also about whether their legal terms will leave you holding the
> compliance bag. Welcome to the regulated era.

This reference compares major AI API providers from a compliance perspective.
It is based on publicly available information and is not a legal opinion.
Provider policies change frequently — verify current terms before making decisions.

---

## Why Provider Choice Matters for Compliance

Under the AI Act, if you build a product using a third-party AI model (API or
hosted), you likely qualify as a **deployer** — and sometimes as a **provider**
if you substantially modify the model or put it on the market under your own name.

Either way, you inherit obligations that depend on what your upstream provider
gives you:

- **Technical documentation** — You need it for your conformity assessment. Does your provider share enough?
- **Data processing terms** — If the provider processes personal data in prompts, you need a solid DPA.
- **Training data opt-out** — If your prompts train the provider's model, you might be contributing to a data governance nightmare.
- **Incident reporting** — If the provider's model causes an incident, how fast can you get information?
- **EU presence** — Under Art. 54, non-EU providers must appoint an EU representative.

Your compliance is only as strong as your weakest link in the value chain.

---

## Provider Comparison Matrix

The following table compares key compliance dimensions across major providers.
Ratings use: Yes / Partial / No / Unknown.

| Dimension | Anthropic (Claude) | OpenAI (GPT) | Google (Gemini) | Mistral | Cohere | Meta (Llama via API) |
|-----------|-------------------|--------------|-----------------|---------|--------|---------------------|
| **DPA available** | Yes | Yes | Yes | Yes | Yes | Yes (via hosting partners) |
| **DPA quality (GDPR-aligned)** | Strong | Strong | Strong | Strong | Good | Varies by host |
| **EU data residency** | Available (EU region) | Available (EU via Azure) | Available (EU region) | Yes (EU-native) | Available | Depends on hosting provider |
| **Data retention (API)** | 30 days (safety), no training | 30 days (safety), no training by default | Varies by product | Short retention, no training | Configurable | N/A (self-hosted or via partner) |
| **Training opt-out (API)** | Default: not used for training | Default: not used for training (API) | Depends on product tier | Not used for training | Not used for training | N/A (open-weight model) |
| **Model card / system card** | Published | Published | Published | Published | Published | Published (comprehensive) |
| **Art. 53 compliance claims** | In progress | In progress | In progress | In progress | Partial | Partial (open-weight specific) |
| **EU representative (Art. 54)** | Appointed | Appointed | EU entity exists | EU-headquartered | In progress | EU entity exists |
| **API terms AI Act compatible** | Evolving | Evolving | Evolving | Evolving | Evolving | Open-weight license + API terms vary |
| **Incident reporting support** | Status page + account support | Status page + account support | Status page + account support | Status page + support | Status page + support | Community + hosting provider |
| **Content provenance (C2PA)** | In development | Partial (DALL-E images) | Partial (some products) | Limited | Limited | Limited |
| **Transparency reporting** | Published | Published | Published | Published | Limited | Published |

**Last verified**: March 2026. Assume any cell could be outdated by the time you read this.

---

## Provider-by-Provider Notes

### Anthropic (Claude)

- Headquartered in the US. EU representative appointed.
- API data is not used for training by default. Safety-related retention (up to 30 days) with strict access controls.
- Usage policy is detailed and actively enforced. May restrict use cases that conflict with their Acceptable Use Policy.
- Strong on safety research transparency. Publishes model cards and system prompts.
- EU data residency available through direct API and cloud provider partnerships.
- Evolving AI Act compliance documentation — check their Trust & Safety pages for updates.

### OpenAI (GPT-4, GPT-4o, o-series)

- Headquartered in the US. EU representative appointed.
- API data not used for training by default since March 2023. Consumer products (ChatGPT) have different defaults.
- Enterprise tier offers enhanced data controls, SOC 2 compliance, and dedicated infrastructure.
- Extensive model cards published. Active engagement with EU regulatory process.
- EU data residency available through Azure OpenAI Service.
- Content provenance: C2PA metadata on DALL-E generated images. Text content provenance in development.

### Google (Gemini)

- EU entity exists (Google Ireland, Google Cloud EMEA).
- Data handling varies significantly between products (Gemini API, Vertex AI, consumer Gemini). Read the specific terms for your product.
- Vertex AI offers strong enterprise data controls and EU data residency.
- Publishes model cards and technical reports.
- Large investment in AI safety research. Participates in standards development.
- Content provenance: SynthID watermarking for some generated content.

### Mistral

- Headquartered in Paris, France. EU-native provider.
- Being EU-based simplifies several compliance dimensions (no Art. 54 representative needed, natural EU data residency).
- API data not used for training. Reasonable retention policies.
- Publishes model cards. Active in EU policy discussions.
- Open-weight models available alongside API, giving you more deployment flexibility.
- Smaller company — enterprise support infrastructure is maturing.

### Cohere

- Headquartered in Canada. EU representative appointment in progress.
- Enterprise-focused with strong data privacy positioning.
- Offers private deployments and configurable data retention.
- Model documentation available but less extensive than larger providers.
- Particularly strong in enterprise search and RAG use cases.
- AI Act compliance documentation is developing.

### Meta (Llama via API / Self-Hosted)

- Open-weight models (Llama series) with a permissive license.
- Self-hosting means you control data processing entirely — great for compliance, but you own all the operational burden.
- API access typically through hosting partners (AWS, Azure, Together AI, etc.) — compliance terms depend on the hosting provider, not Meta directly.
- Comprehensive model cards published with detailed training information.
- Art. 53 obligations apply to Meta as the GPAI model provider, but your compliance posture depends heavily on your deployment choice.
- No content provenance features built-in — you must implement your own.

---

## The Comparison Table You Actually Need

For quick decision-making, here's what matters most by use case:

### If You Handle EU Personal Data in Prompts

**Priority**: DPA quality, EU data residency, training opt-out, data retention.

**Best positioned**: Mistral (EU-native), Google Vertex AI (EU region), Anthropic (EU region), OpenAI via Azure (EU region).

### If You Build High-Risk AI

**Priority**: Model documentation, Art. 53 compliance, incident reporting, transparency.

**Best positioned**: Providers with published model cards and active AI Act engagement. Currently Anthropic, OpenAI, Google, and Mistral lead on documentation depth.

### If You Need Maximum Control

**Priority**: Self-hosting capability, data never leaves your infrastructure.

**Best positioned**: Meta Llama (self-hosted), Mistral (self-hosted open-weight models). You get full control but full responsibility.

### If You Generate Synthetic Content

**Priority**: Content provenance, C2PA support, watermarking.

**Best positioned**: OpenAI (DALL-E C2PA), Google (SynthID). This area is immature across all providers for text content.

---

## What to Check Before Signing Up

Due diligence checklist before committing to an AI API provider:

### Legal and Contractual

- [ ] DPA is available, GDPR-aligned, and covers your specific processing activities
- [ ] Terms of service do not grant the provider rights to use your data for training (or you can opt out)
- [ ] Data retention period is documented and acceptable for your use case
- [ ] Liability allocation is clear — who is responsible for model outputs?
- [ ] Terms are compatible with your AI Act obligations (can you get the documentation you need?)
- [ ] Sub-processor list is available and acceptable
- [ ] Data breach notification obligations are specified and timely

### Technical and Operational

- [ ] EU data residency is available and you can enforce it technically
- [ ] API uptime SLA meets your availability requirements
- [ ] Model versioning — will you be notified before model changes?
- [ ] Rate limiting and capacity guarantees are sufficient
- [ ] Logging and audit trail capabilities meet Art. 12 requirements
- [ ] Content filtering / safety features are configurable for your use case
- [ ] Model card or system card provides sufficient technical documentation

### AI Act Specific

- [ ] Provider has appointed an EU representative (if non-EU)
- [ ] Provider publishes Art. 53 compliance documentation (for GPAI)
- [ ] Provider supports downstream transparency obligations
- [ ] Provider's incident reporting process is documented
- [ ] Provider commits to notifying you of material model changes
- [ ] Provider's acceptable use policy is compatible with your intended use
- [ ] Provider will cooperate with market surveillance authorities if needed

### Ongoing Monitoring

- [ ] You have a process to review provider term changes
- [ ] You monitor the provider's status page and security advisories
- [ ] You re-evaluate compliance posture at least annually
- [ ] You have a migration plan if the provider becomes non-compliant

---

## A Note on "AI Act Compliant" Marketing Claims

Several providers now market themselves as "AI Act compliant" or "AI Act ready."
Treat these claims with professional skepticism.

The AI Act places obligations on **providers** and **deployers** — not on API
services in isolation. A provider being "compliant" doesn't make *your system*
compliant. It means they handle their part of the value chain. You still need to
handle yours.

What matters is not whether they claim compliance, but whether their terms,
documentation, and technical capabilities *enable* your compliance. An honest
provider will say "we support your compliance" rather than "we make you compliant."

---

## Disclaimer

This comparison is based on publicly available information as of March 2026.
We are not affiliated with any provider listed. Provider policies, terms, and
capabilities change frequently — often without prominent announcement.

Before making procurement decisions:
1. Verify current terms on the provider's website
2. Request the latest DPA and review it with legal counsel
3. Test technical capabilities (data residency, logging) in your specific configuration
4. Document your due diligence for your AI Act compliance records

This is a starting point for research, not a substitute for legal advice or
technical evaluation.
