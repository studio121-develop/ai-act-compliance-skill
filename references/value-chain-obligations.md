# Value Chain Responsibilities (Arts. 22-28)

The AI Act does not just regulate the entity that builds the AI system. It regulates
every actor in the value chain, from the foundation model provider all the way to the
organization deploying the system on real people. If you are building SaaS products that
use AI, you sit somewhere in this chain — and so do your customers.

This document maps the chain, explains each actor's obligations, and gives you practical
contract language and upstream demands.

---

## The AI Value Chain at a Glance

The AI Act defines five key roles (Art. 3). A single organization can occupy more than
one role simultaneously:

| Role | Definition | Typical Example |
|------|-----------|-----------------|
| **GPAI model provider** | Develops or commissions a general-purpose AI model and places it on the market (Art. 3(66)) | Anthropic, OpenAI, Meta (for Llama) |
| **AI system provider** | Develops or commissions an AI system and places it on the market or puts it into service under their own name (Art. 3(3)) | Your SaaS company wrapping an API into a product |
| **Deployer** | Uses an AI system under their authority in a professional capacity (Art. 3(4)) | Your B2B customer running your product |
| **Importer** | Places on the EU market an AI system from a non-EU provider (Art. 3(6)) | EU distributor reselling a US-built tool |
| **Distributor** | Makes an AI system available on the EU market without being provider or importer (Art. 3(7)) | Marketplace or VAR |

Recital 83 clarifies that these roles are functional, not corporate. The same legal
entity can be both a provider and a deployer for different systems.

---

## Art. 25: When a Downstream Actor Becomes a New Provider

This is the article that catches people off guard. You become a **new provider** — and
inherit all provider obligations — if you do any of the following:

1. **Put your name or trademark** on a high-risk AI system already on the market
   (Art. 25(1)(a))
2. **Make a substantial modification** to a high-risk AI system (Art. 25(1)(b))
3. **Modify the intended purpose** of an AI system so that it becomes high-risk
   (Art. 25(1)(c))

### What counts as a "substantial modification"?

Art. 3(23) defines it as a change not foreseen by the original provider that affects
compliance with the requirements of Chapter III, Section 2, or that modifies the
intended purpose for which the conformity assessment was performed.

Practical examples:
- Fine-tuning a model on domain-specific data that changes its risk profile: **likely substantial**
- Changing the output classification thresholds of a hiring-screening tool: **likely substantial**
- Adjusting UI copy or adding logging: **not substantial**
- Adding RAG with new data sources that shift the system's domain: **possibly substantial**, depends on intended-purpose scope

When you become a new provider under Art. 25, the original provider must give you the
information needed to comply (Art. 25(3)). Put this in your contracts.

---

## Art. 24: Obligations of Importers

If you bring a non-EU AI system into the EU market, you must (Art. 24(1)-(5)):

- Verify the provider has carried out the conformity assessment
- Verify technical documentation (Annex IV) exists
- Verify the system bears CE marking and is accompanied by the EU declaration of conformity
- Verify the provider has appointed an authorized representative (Art. 23)
- Not place the system on the market if you have reason to believe it does not comply
- Ensure storage/transport conditions do not jeopardize compliance
- Keep a copy of the EU declaration of conformity for 10 years (Art. 24(6))
- Provide information and documentation to authorities on request

Importers who discover non-compliance must take corrective action or withdraw the system
(Art. 24(7)).

---

## Art. 23: Authorized Representatives for Non-EU Providers

Non-EU providers placing high-risk AI systems on the EU market must appoint an
authorized representative established in the EU **before** placing the system on the
market (Art. 22(1)).

The authorized representative's mandate must include (Art. 23(2)):
- Verifying the conformity assessment and technical documentation exist
- Keeping documentation available for authorities for 10 years
- Cooperating with competent authorities
- Informing the provider immediately of any non-compliance
- Terminating the mandate if the provider acts contrary to the AI Act

This mirrors the GDPR representative requirement (Art. 27 GDPR) and the MDR authorized
representative model. If your GPAI model provider (e.g., a US company) does not have an
EU authorized representative, that is a red flag for your compliance story.

---

## Art. 26: Deployer Obligations (Critical for B2B SaaS)

Your B2B customers are deployers. Art. 26 imposes direct obligations on them, which
means they will demand things from you (the provider) to meet those obligations.

Deployers of high-risk AI systems must:

1. **Use the system in accordance with the instructions of use** (Art. 26(1))
2. **Assign human oversight** to natural persons with competence, training, and
   authority (Art. 26(2)) — see Art. 14 for the full human oversight requirements
3. **Ensure input data is relevant and sufficiently representative** for the intended
   purpose (Art. 26(4))
4. **Monitor the system's operation** based on the instructions of use (Art. 26(5))
5. **Inform the provider or distributor** when they identify a risk and **suspend use**
   if a serious incident occurs (Art. 26(5))
6. **Keep logs automatically generated** by the system for at least 6 months, unless
   other law requires longer (Art. 26(6))
7. **Carry out a Fundamental Rights Impact Assessment (FRIA)** before putting the
   system into use, if required under Art. 27 (Art. 26(9))
8. **Use the output information** from the system to comply with the transparency
   obligation under Art. 50 (Art. 26(11))

For detailed FRIA guidance, see [deployer-obligations.md](./deployer-obligations.md).

---

## Art. 28: Obligations Along the Value Chain

Art. 28 creates a web of mutual duties:

- Any distributor, importer, deployer, or other third party who **substantially modifies**
  a high-risk system or changes its intended purpose is considered a new provider
  (Art. 28(1)) — echoing Art. 25
- The original provider may specify in the contract that they should be notified of
  modifications (Art. 28(2))
- For high-risk systems that are safety components of products covered by Union
  harmonisation legislation (Annex I, Section A), the **product manufacturer** is
  considered the provider of the AI system (Art. 28(3))

Recital 84 emphasizes that these rules ensure "no regulatory gap" in the value chain.

---

## How Liability Flows Through the Chain

The AI Act itself is primarily a regulatory compliance framework, not a civil liability
statute. However, liability flows through two mechanisms:

### 1. The AI Liability Directive (Directive 2024/2853)
- Creates a presumption of causality when a provider or deployer fails to comply with
  the AI Act and harm occurs
- Non-compliance with your AI Act obligations directly strengthens a claimant's case

### 2. The Product Liability Directive (Directive 2024/2853)
- AI systems embedded in products are "products" under PLD
- The provider is treated as the manufacturer
- Strict liability applies — no need to prove fault

### Practical liability chain:
1. End user suffers harm from an AI-powered decision
2. End user claims against the **deployer** (your customer)
3. Deployer seeks indemnification from the **provider** (you)
4. Provider may seek contribution from the **GPAI model provider** (Anthropic, OpenAI)

This means your contracts need indemnification clauses flowing in both directions.

---

## Practical Section: What to Include in Your B2B Contracts

When your customers are deployers of your high-risk AI system, your deployer agreements
should include:

### Mandatory provider-to-deployer provisions:
- **Instructions of use** — comprehensive, meeting Art. 13 requirements
- **Intended purpose statement** — clearly scoped to match your conformity assessment
- **Human oversight requirements** — who needs to oversee, with what training
- **Input data specifications** — what data quality and relevance standards apply
- **Log retention** — what logs your system generates and how to access/retain them
- **Incident reporting obligations** — deployer must report serious incidents to you
  within [specify timeframe]
- **Prohibited uses** — explicitly list out-of-scope uses to avoid Art. 25 triggering
- **Modification restrictions** — any changes beyond [defined scope] may make the
  deployer a new provider under Art. 25

### Recommended additional clauses:
- **Cooperation on market surveillance** — mutual obligation to respond to authority
  requests (Art. 21)
- **FRIA support** — provider will supply information needed for the deployer's FRIA
  (Art. 27)
- **Update obligations** — provider will supply updates, deployer will install them
- **Indemnification** — mutual indemnification for breaches of respective obligations
- **Audit rights** — deployer's right to verify provider's compliance documentation
- **Data processing agreement** — if personal data is processed, GDPR Art. 28 DPA

---

## Practical Section: What to Demand from Your Upstream Provider

If you are building on top of a GPAI model (Anthropic Claude, OpenAI GPT, Google Gemini,
etc.), demand the following from your upstream provider:

### Under Art. 52 (GPAI obligations):
- [ ] Technical documentation as required by Art. 52(1)(a)
- [ ] Information and documentation for downstream providers integrating the model
- [ ] Policy on copyright compliance
- [ ] Sufficiently detailed summary of training data content (per Art. 52(1)(d))

### For your own compliance:
- [ ] Model cards or system cards with performance metrics and known limitations
- [ ] Clear acceptable use policies with version history
- [ ] API documentation sufficient to implement human oversight (Art. 14)
- [ ] Incident notification commitments — if the model exhibits unexpected behavior
- [ ] Contractual right to receive updates to technical documentation
- [ ] Warranty that the model has been evaluated for the risks relevant to your use case
- [ ] Transparency about training data sources (to support your Art. 10 data governance)

### Red flags in upstream provider relationships:
- Provider refuses to share any technical documentation
- No clear versioning or changelog for model updates
- Terms of service disclaim all responsibility for downstream compliance
- No EU authorized representative (for non-EU providers of high-risk system components)
- No incident notification mechanism

---

## Key Takeaways

1. **Know your role.** Map every AI system you build or use to a specific role in the
   value chain. You may hold multiple roles.
2. **Art. 25 is a trap.** Substantial modifications or rebranding can silently turn you
   into a provider with full provider obligations.
3. **Your customers need things from you.** As a provider, you must equip deployers to
   meet their Art. 26 obligations. Build this into your product, not just your contracts.
4. **Contracts are your safety net.** Liability flows through the chain. Your agreements
   with both upstream providers and downstream deployers should reflect AI Act obligations.
5. **10-year documentation retention** applies across the chain. Plan your storage accordingly.
