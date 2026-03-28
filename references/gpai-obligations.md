# GPAI Model Provider Obligations (Arts. 51-56)

General-Purpose AI (GPAI) models are the foundation models that power most modern AI
applications — think Claude, GPT-4, Gemini, Llama, Mistral. The AI Act creates a
separate regulatory tier for these models under Chapter V (Arts. 51-56), recognizing
that their providers sit at the top of the value chain and have outsized influence on
downstream safety.

If you are building SaaS on top of these models, you are almost certainly **not** a GPAI
model provider. But understanding these obligations is essential because (a) they
determine what your upstream provider owes you, and (b) certain activities like
fine-tuning can blur the line.

---

## Art. 51: Classification of GPAI Models

GPAI models fall into two tiers:

### Tier 1: All GPAI Models
Any AI model that:
- Is trained with a large amount of data using self-supervision at scale
- Displays significant generality
- Is capable of competently performing a wide range of distinct tasks
- Can be integrated into a variety of downstream systems or applications

(Art. 3(63))

### Tier 2: GPAI Models with Systemic Risk
A GPAI model is classified as having **systemic risk** if (Art. 51(2)):
- It has **high-impact capabilities**, meaning capabilities that match or exceed those of
  the most advanced models, OR
- It is designated by the Commission based on specific criteria

The presumption trigger: a GPAI model is presumed to have systemic risk when the
cumulative amount of compute used for its training, measured in FLOPs, is **greater than
10^25** (Art. 51(2)). The Commission can update this threshold.

Recital 110 explains that high-impact capabilities include the ability to perform tasks
that pose significant risks to health, safety, fundamental rights, the environment,
democracy, or the rule of law.

As of the date of this document, models presumed to have systemic risk include GPT-4
class and above. The threshold is designed to capture only the frontier.

---

## Art. 52: Obligations of All GPAI Model Providers

Every GPAI model provider must (Art. 52(1)):

### (a) Technical Documentation
Draw up and keep up to date technical documentation of the model, including its training
and testing process and the results of its evaluation. This documentation must contain
at minimum the information set out in **Annex XI**.

Annex XI requires:
- Description of the model including version, date of release, architecture
- Description of the elements of the model and of the process for building it
- Description of the compute resources used (type, quantity, country of hosting)
- Description of training data: provenance, scope, curation methods, data characteristics
- Description of data processing choices (cleaning, labeling, enrichment)
- Model training details: methodology, techniques, hyperparameters
- Evaluation results, including benchmark performance

### (b) Information for Downstream Providers
Draw up, keep up to date, and make available information and documentation to providers
of AI systems who intend to integrate the GPAI model into their systems. This must
enable them to understand the model's capabilities and limitations and comply with their
own obligations.

In practice, this means: model cards, system cards, API documentation, capability
descriptions, known limitations, and risk information.

### (c) Copyright Compliance Policy
Put in place a policy to comply with Union copyright law, in particular to identify and
comply with reservations of rights expressed pursuant to Art. 4(3) of the DSM Directive
(Directive (EU) 2019/790) — the opt-out mechanism for text and data mining.

### (d) Training Data Summary
Draw up and make publicly available a sufficiently detailed summary about the content used
for training the GPAI model, according to a template provided by the AI Office
(Art. 52(1)(d)).

This summary is not the full training dataset description — it is a public-facing summary
designed to help rights holders understand whether their content may have been used.

---

## Art. 53: Additional Obligations for GPAI with Systemic Risk

On top of Art. 52 obligations, providers of GPAI models with systemic risk must
(Art. 53(1)):

### (a) Model Evaluation
Perform **model evaluation** in accordance with standardized protocols and tools,
including adversarial testing, to identify and mitigate systemic risks.

### (b) Systemic Risk Assessment and Mitigation
Assess and mitigate possible systemic risks at Union level, including their sources.

### (c) Serious Incident Tracking and Reporting
Track, document, and report to the AI Office and relevant national authorities any
**serious incidents** and possible corrective measures without undue delay.

### (d) Adequate Cybersecurity
Ensure an adequate level of cybersecurity protection for the model and its physical
infrastructure.

Recital 115 makes clear that systemic risks can include large-scale accidents, misuse
for cyberattacks, the spread of biases across many downstream applications, or severe
effects on democratic processes.

---

## Art. 54: Authorized Representatives

Non-EU GPAI model providers must appoint an authorized representative established in the
EU **before** making the model available on the Union market (Art. 54(1)).

This parallels Art. 22-23 for high-risk AI systems. The authorized representative must
have a written mandate specifying their tasks, which must include at least:

- Verifying that technical documentation (Annex XI) has been drawn up
- Keeping documentation available for the AI Office for 10 years
- Cooperating with the AI Office on any action it takes regarding the model
- Informing the provider if there is reason to believe the model no longer complies

---

## Art. 55: Codes of Practice

The AI Office facilitates the drawing up of **codes of practice** to contribute to the
proper application of the GPAI obligations (Art. 55(1)).

GPAI model providers can rely on adherence to a code of practice to demonstrate compliance
with Arts. 52 and 53, until a harmonized standard is published (Art. 55(2)).

### The GPAI Code of Practice (Published July 2025)

The first General-Purpose AI Code of Practice was finalized in July 2025 after an
extensive multi-stakeholder drafting process involving GPAI providers, downstream
providers, civil society, and Member State representatives.

Key requirements of the Code:

**For all GPAI models:**
- Structured technical documentation following a standardized template
- Transparency report on training data (going beyond the minimum Art. 52(1)(d) summary)
- Copyright policy with complaint mechanism for rights holders
- Downstream provider information package with capability and limitation descriptions

**For GPAI with systemic risk (additional):**
- Red-teaming framework with standardized adversarial testing protocols
- Systemic risk assessment methodology
- Incident response and reporting procedures
- Cybersecurity baseline requirements
- Regular external evaluation cadence

Adherence to the Code of Practice is **voluntary but strongly incentivized** — it creates
a compliance presumption. Non-adherent providers must demonstrate equivalent compliance
through other means.

---

## The Critical Question: When Does Fine-Tuning (or RAG, or Prompting) Make You a GPAI Model Provider?

This is the question every SaaS builder asks. Here is the framework.

### Fine-tuning

**Full fine-tuning (updating all or most weights):**
If you take an open-weight GPAI model (e.g., Llama, Mistral) and perform full
fine-tuning, you are creating a **new model** that you are placing on the market. You are
likely a GPAI model provider under Art. 3(66), especially if the resulting model retains
general-purpose capabilities.

**LoRA / adapter-based fine-tuning:**
This is a grey area. Recital 97 clarifies that modifying a GPAI model through fine-tuning
does not make the modified model a new GPAI model if the modification does not
substantially change the model's general-purpose capabilities. However, if you fine-tune
and then distribute the modified model (even via API), you may be considered a new
provider if the result has materially different capabilities.

**Fine-tuning via API (e.g., OpenAI fine-tuning endpoint):**
You are almost certainly **not** a GPAI model provider. The model remains hosted and
controlled by the original provider. You are creating a customized version within their
infrastructure. However, you may be a provider of an **AI system** built on top of that
model.

### RAG (Retrieval-Augmented Generation)

RAG does **not** make you a GPAI model provider. You are not modifying the model itself —
you are providing context at inference time. RAG is an AI system architecture choice, not
a model modification.

However, RAG significantly influences system behavior and outputs. As a provider of the
**AI system** that uses RAG, you are responsible for:
- The quality and accuracy of retrieved content
- Ensuring retrieved data does not introduce bias or discriminatory patterns
- Documenting the RAG architecture in your technical documentation

### Prompt Engineering / System Prompts

Prompt engineering does **not** make you a GPAI model provider. You are operating at the
application layer. No weights are modified, no training occurs.

But (and this is important): if your system prompt is so extensive that it effectively
creates a specialized agent with a narrow, domain-specific behavior, you are building an
**AI system** — and if that system is high-risk, you have provider obligations for the
system, even though you are not a GPAI model provider.

### Summary Table

| Activity | GPAI Model Provider? | AI System Provider? |
|----------|---------------------|-------------------|
| Full fine-tune of open model, redistribute | Likely yes | Also yes, if you build a system |
| LoRA fine-tune, redistribute | Possibly, depends on capability change | Yes, if you build a system |
| API fine-tuning (model stays with provider) | No | Yes |
| RAG | No | Yes |
| Prompt engineering / system prompts | No | Yes, if you build a product |
| Using API as-is, no customization | No | Yes, if you build a product |

---

## Most SaaS Builders Are NOT GPAI Model Providers

If you are:
- Calling Claude, GPT, or Gemini via API
- Fine-tuning via a provider's API
- Using RAG to add context
- Building an application layer with system prompts

Then you are an **AI system provider**, not a GPAI model provider. Your obligations come
from Chapter III (if high-risk) or Art. 50 (transparency), not from Chapter V.

### When you MIGHT be a GPAI model provider:
- You train a foundation model from scratch
- You take an open-weight model, substantially fine-tune it, and make it available for
  others to build on (either via API or by distributing weights)
- You merge or distill multiple models into a new general-purpose model

The distinguishing factor: are you providing a **model** that others integrate, or a
**system** that end-users or deployers use? If you are providing a model → Chapter V.
If a system → Chapter III (or lower-risk categories).

---

## What This Means for Your Upstream Due Diligence

Since your GPAI model provider has obligations under Art. 52, you should verify they
are meeting them. See [value-chain-obligations.md](./value-chain-obligations.md) for
detailed guidance on what to demand from upstream providers.

At a minimum, confirm your GPAI model provider:
- Has published technical documentation or committed to a Code of Practice
- Has appointed an EU authorized representative (if non-EU)
- Provides downstream provider information sufficient for your compliance
- Has a copyright compliance policy
- Has published a training data summary

If your provider is not meeting these obligations, that is not just their problem — it
weakens your own compliance posture and may expose you to regulatory scrutiny.

---

## Key Takeaways

1. **GPAI obligations are separate from AI system obligations.** Chapter V applies to
   model providers; Chapter III applies to system providers. Know which you are.
2. **The 10^25 FLOP threshold** triggers systemic risk classification. Most SaaS
   builders are nowhere near this.
3. **Fine-tuning via API does not make you a GPAI provider.** But fine-tuning open
   weights and redistributing might.
4. **The Code of Practice is the compliance benchmark.** Demand that your upstream
   providers adhere to it.
5. **RAG and prompting are system-level, not model-level.** They trigger AI system
   provider obligations, not GPAI model provider obligations.
