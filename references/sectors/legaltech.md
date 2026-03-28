<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Legaltech — AI That Reads the Law (About AI)

There is a certain poetry in building an AI system that helps lawyers understand the AI Act. A regulation about AI, interpreted by AI, applied to AI. We are through the looking glass.

But let us set the meta-irony aside. Legaltech AI occupies a genuinely interesting position under the AI Act because the line between "high-risk" and "perfectly fine" depends almost entirely on who is using your tool and for what. The same legal research system can be high-risk when used by a judge and completely unregulated when used by a corporate lawyer reviewing contracts. Context is everything.

## What the AI Act Says About Legal AI

### Annex III, Category 8 — Administration of Justice and Democratic Processes

Two entries:

1. **AI assisting judicial authorities** in researching and interpreting facts and law, and applying the law to facts
2. **AI for dispute resolution** with binding or quasi-binding outcomes

That is it. Two entries. But the implications are substantial.

## When Legaltech AI IS High-Risk

- **Used by courts or judges** for case research, legal analysis, or applying law to facts
- **Binding dispute resolution** — AI-mediated arbitration where the outcome has legal effect
- **Evidence analysis for legal proceedings** — AI assessing reliability or relevance of evidence in judicial contexts
- **Prosecutorial support** — AI helping decide whether to bring charges (also crosses into Category 6)
- **Draft judicial decisions** — AI producing judgments, sentencing recommendations, or case outcome predictions for judges

### The Critical Distinction: Who Is the User?

| System | Used by Judge/Court | Used by Law Firm | Classification |
|---|---|---|---|
| Legal research platform | High-risk (Cat. 8) | Likely not high-risk | Depends on deployer |
| Case outcome prediction | High-risk (Cat. 8) | Arguably not high-risk | Depends on deployer |
| Contract analysis | N/A (not judicial) | Not high-risk | Not in Annex III |
| Evidence analysis tool | High-risk (Cat. 8) | Possibly not high-risk | Depends on context |

This creates an unusual compliance challenge: you may need to implement high-risk requirements because some users are judicial authorities, even if most are private lawyers. You cannot control who buys your product.

## When Legaltech AI Is NOT High-Risk

- **Legal research for lawyers** — Searching case law, legislation, commentary for private practice
- **Contract review and analysis** — Identifying clauses, flagging risks, comparing terms
- **Due diligence automation** — Document review for M&A, compliance, or litigation hold
- **Legal chatbots** — General legal information with appropriate disclaimers
- **Legal document generation** — Drafting from templates with user inputs
- **Compliance monitoring** — Tracking regulatory changes, flagging relevant developments

### Art. 6(3) Derogation for Legal Research

Most lawyer-facing tools can plausibly qualify because they:
- Perform a **preparatory task** — AI retrieves and summarizes; the lawyer analyzes and applies law to facts
- **Improve previously completed human activity** — Refining research the lawyer started
- **Do not replace human judgment** — The lawyer forms their own legal opinion

**Two caveats:**
1. If the tool **profiles individuals** (analyzing opposing counsel patterns, predicting individual judge behavior), the derogation does not apply
2. If used by **judicial authorities**, the context shifts and the derogation argument weakens significantly

## Attorney-Client Privilege and AI

The issue that keeps legal AI builders up at night.

### Does Privilege Survive AI Processing?

- **Third-party access** — Most jurisdictions are moving toward treating AI tools like cloud storage (privilege maintained with reasonable security). But not settled everywhere.
- **Training data** — If your AI trains on user data, privileged communications in training data create extraordinary problems. Never train on client data.
- **Logging vs. privilege** — Art. 12 requires logging, but logging privileged content creates discoverable records. Log system behavior, not content.
- **Cross-border** — Privilege rules differ between common law and civil law jurisdictions. Same communication, different protection.

### Privilege-Aware Architecture

```python
@dataclass(frozen=True)
class PrivilegeAwareAuditEntry:
    """Audit log satisfying Art. 12 without compromising privilege."""
    audit_id: str
    timestamp: str
    user_id_hash: str
    action: str                    # "search", "analyze", "generate"
    document_count: int
    privilege_flagged_count: int
    system_version: str
    query_category: str            # Categorize type, never log actual query
    result_count: int
    processing_time_ms: int
    # No query text. No document content. No result content.
```

The principle: log enough to satisfy Art. 12 record-keeping, but never persist privileged content. Categorize queries by type ("contract_review", "case_research") without recording the actual query text.

## Citation Verification: Trust but Verify

Legal AI hallucinations are not just embarrassing — they are sanctionable. Courts have fined lawyers for citing AI-generated fake cases.

```python
@dataclass(frozen=True)
class VerifiedLegalResponse:
    """AI response with citation verification clearly indicated."""
    response_id: str
    content: str
    citations: tuple[LegalCitation, ...]
    all_citations_verified: bool
    unverified_count: int
    disclaimer: str  # Warns if any citations could not be verified
```

Every citation should have: `verified` status, `verification_method` ("database_lookup", "url_check", "unverified"), source URL, and confidence score. If any citation is unverified, the disclaimer must explicitly warn: "AI systems can generate plausible but non-existent legal references."

## Court Rules on AI-Generated Submissions

A rapidly evolving area as of early 2026:

- **England & Wales**: Practice Direction requires disclosure of AI use in court documents
- **Several US jurisdictions**: Standing orders requiring lawyers to certify AI content is verified
- **EU member states**: Varying approaches, trending toward mandatory disclosure
- **CJEU**: No specific AI rules yet, but general lawyer responsibility applies

For your product:
- Build **disclosure features** — make it easy to identify AI-assisted parts of documents
- Consider **metadata embedding** indicating AI involvement
- Enable **compliance report export** showing AI involvement for court disclosure

## The "AI-Generated Legal Advice" Problem

Your legaltech AI is not giving legal advice. It really is not. Make this extremely clear:

1. **Unauthorized practice** — Only licensed lawyers can give legal advice. AI advice is unauthorized practice, and liability falls on the provider.
2. **Professional liability** — A lawyer who blindly relies on AI is liable. But the provider may face product liability claims too.
3. **Disclaimers: necessary but not sufficient** — If your product is designed so users treat it as legal advice, courts may look past the disclaimer.

Implement context-specific disclaimers: general research gets "informational purposes only, consult a qualified professional"; court-facing output gets "must be independently verified before use in legal proceedings"; contract review gets "does not replace professional legal review."

## Cross-Border Considerations

Legal AI faces a unique challenge: law itself is jurisdiction-specific.

- **Different systems** — Common law (case-driven) vs. civil law (code-driven) need different approaches
- **Different courts** — Each member state has different procedural rules, evidence standards, technology adoption
- **Multilingual complexity** — Legal terms do not translate neatly ("consideration" in English law has no French equivalent)
- **Regulatory fragmentation** — National bar associations have different AI rules

If operating cross-border: implement jurisdiction-aware configurations, not one-size-fits-all.

## Compliance Checklist

- [ ] Determine if any users are judicial authorities — if yes, you provide a high-risk system
- [ ] If high-risk: implement full Art. 9-15 obligations
- [ ] If lawyer-only: document Art. 6(3) derogation analysis thoroughly
- [ ] Design audit logging that satisfies Art. 12 without compromising privilege
- [ ] Implement citation verification for all AI-generated legal references
- [ ] Build disclosure features for court compliance requirements
- [ ] Include clear, prominent disclaimers that output is not legal advice
- [ ] Ensure human supervision is built in, not bolted on
- [ ] Address privilege preservation in architecture documentation
- [ ] Monitor emerging court rules on AI across target jurisdictions
- [ ] If cross-border: implement jurisdiction-aware configurations
- [ ] Conduct FRIA focusing on right to fair trial and effective remedy
