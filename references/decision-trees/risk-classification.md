<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Risk Classification Decision Tree

An executable, step-by-step decision algorithm for classifying AI systems under the EU AI Act. Walk through this with your AI agent or use it as a structured self-assessment.

> **Disclaimer**: This decision tree provides general guidance. It does not constitute legal advice or guarantee a correct classification. Consult a qualified professional for definitive risk assessment.

## How to Use

For each AI feature in your product, walk through the questions below in order. Each question has a YES/NO path. Follow the path until you reach a classification result.

You can ask Claude: `Classify the AI Act risk level of [describe your feature]` and it will walk through this tree interactively.

## The Decision Tree

### Q1: Is the system banned? (Art. 5)

Does your AI system do ANY of the following?

- [ ] Subliminal manipulation to distort behavior in a way that causes harm
- [ ] Exploit vulnerabilities of specific groups (age, disability, social/economic situation)
- [ ] Social scoring by public or private actors
- [ ] Real-time remote biometric identification in public spaces (unless specific law enforcement exceptions)
- [ ] Untargeted facial image scraping from internet or CCTV
- [ ] Emotion recognition in workplace or education (unless medical/safety)
- [ ] Biometric categorization to infer race, political opinions, religion, sexual orientation
- [ ] Predictive policing based solely on profiling

**YES to any** → PROHIBITED. Stop here. This practice is banned since Feb 2, 2025. You cannot deploy this system in the EU. Redesign or remove the feature.

**NO to all** → Continue to Q2.

---

### Q2: Is it a safety component of a regulated product? (Art. 6(1) + Annex I)

Is your AI system:
- A safety component of a product covered by EU harmonization legislation listed in Annex I? (medical devices, machinery, toys, radio equipment, civil aviation, vehicles, rail, marine equipment, etc.)
- Or: is the AI system itself such a product?

**YES** → HIGH-RISK via Annex I pathway. Must comply with Arts. 9-17 AND the relevant product regulation. Third-party conformity assessment likely required.
See `references/high-risk-requirements.md` and relevant sector guide.

**NO** → Continue to Q3.

---

### Q3: Does it operate in an Annex III domain? (Art. 6(2))

Does your AI system make decisions or significantly influence decisions in ANY of these areas?

| # | Domain | Examples |
|---|--------|----------|
| 1 | Biometrics | Remote identification (not just verification), emotion recognition |
| 2 | Critical infrastructure | Managing electricity, gas, water, heating, road traffic |
| 3 | Education | Exam scoring, admission decisions, learning assessment, proctoring |
| 4 | Employment | Recruitment, CV screening, interview evaluation, performance review, promotion/termination |
| 5 | Essential services | Credit scoring, insurance pricing, emergency dispatch prioritization, social benefits eligibility |
| 6 | Law enforcement | Evidence evaluation, crime prediction, profiling |
| 7 | Migration | Visa/asylum assessment, border control |
| 8 | Justice & democracy | Assisting courts in legal research/interpretation, dispute resolution |

**NO to all** → Skip to Q5.

**YES to any** → Continue to Q4.

---

### Q4: Does the Art. 6(3) derogation apply?

First, the critical check:

**Does your system profile individuals?** (Automated processing of personal data to evaluate aspects of a person: work performance, economic situation, health, preferences, interests, reliability, behavior, location, movements)

**YES, it profiles** → HIGH-RISK. No derogation possible (Art. 6(3) last paragraph). Go to Result A.

**NO, it does not profile** → Check if ALL of the following are true:

- [ ] The system performs a narrow procedural task
- [ ] The system improves the result of a previously completed human activity
- [ ] The system detects decision-making patterns without replacing or influencing the human assessment
- [ ] The system performs a preparatory task to an assessment listed in Annex III

**ALL true** → NOT HIGH-RISK despite Annex III listing. But you MUST document this assessment before placing on market (Art. 6(4)). Continue to Q5.

**NOT all true** → HIGH-RISK. Go to Result A.

---

### Q5: Does it have transparency obligations? (Art. 50)

Does your AI system do ANY of the following?

- [ ] Interact directly with humans (chatbot, assistant, voice interface, conversational AI)
- [ ] Generate synthetic text that may be presented as human-written
- [ ] Generate synthetic images
- [ ] Generate synthetic audio
- [ ] Generate synthetic video
- [ ] Perform emotion recognition
- [ ] Perform biometric categorization
- [ ] Generate or manipulate deepfakes (images/audio/video resembling real people/events)

**YES to any** → Go to Result B (Limited Risk).

**NO to all** → Go to Result C (Minimal Risk).

---

## Results

### Result A: HIGH-RISK

Your AI system is classified as high-risk under the EU AI Act.

**What this means:**
- Full compliance with Arts. 9-17 required by Aug 2, 2026 (Annex III standalone) or Aug 2, 2027 (Annex I products)
- Risk management system (Art. 9)
- Data governance (Art. 10)
- Technical documentation per Annex IV (Art. 11)
- Automatic logging (Art. 12)
- Transparency to deployers (Art. 13)
- Human oversight measures (Art. 14)
- Accuracy, robustness, cybersecurity (Art. 15)
- Quality management system (Art. 17)
- Conformity assessment (Annex VI self-assessment or Annex VII third-party)
- CE marking and EU database registration

**Next steps:**
1. Read `references/high-risk-requirements.md`
2. Use `references/annex-iv-template.md` for documentation
3. Follow `references/conformity-assessment.md` for assessment walkthrough
4. Check your sector guide in `references/sectors/`
5. Consider engaging legal counsel

**Confidence level**: If you reached this result, the classification is relatively clear. The main ambiguity is in Art. 6(3) derogation cases — when in doubt, classify as high-risk.

### Result B: LIMITED RISK (Transparency Obligations)

Your AI system has transparency obligations under Art. 50. This is the most common result for SaaS products with AI features.

**What this means:**
- Art. 50(1): Inform users they're interacting with AI
- Art. 50(2): Mark AI-generated content in machine-readable format
- Art. 50(4): Special disclosure for deepfakes and public interest text
- Deadline: Aug 2, 2026

**Next steps:**
1. Implement disclosure UI — see `references/transparency-implementation.md`
2. Implement content marking — see code patterns in `references/patterns/`
3. Run the pre-deploy checklist in SKILL.md
4. Create `AI_ACT_COMPLIANCE.md` from the template

**Confidence level**: High. If your system generates content or talks to users, this is almost certainly your classification.

### Result C: MINIMAL RISK

Your AI system has no specific AI Act obligations beyond AI literacy (Art. 4).

**What this means:**
- No mandatory transparency requirements
- No documentation requirements beyond good practice
- AI literacy obligations still apply (in force since Feb 2, 2025)
- You may voluntarily adopt codes of conduct (Art. 95)

**Next steps:**
1. Document your AI literacy training
2. Consider voluntary transparency measures anyway — they build user trust
3. Monitor whether future feature additions change the classification

**Confidence level**: Make sure you're not underestimating your system's capabilities. If there's any user interaction or content generation, re-check Q5.

---

## Edge Cases and Common Questions

**"My chatbot just answers FAQs — is it really limited risk?"**
Yes. Any system that interacts with humans triggers Art. 50(1). Even if the chatbot is simple. Disclose that it's AI.

**"I use AI for internal tools only, not customer-facing."**
The AI Act applies to systems "placed on the market or put into service in the Union" (Art. 2). Internal tools may still be "put into service." If employees use it, consider at minimum AI literacy and good practices. If it's in an Annex III domain (e.g., AI-assisted HR decisions), it's high-risk regardless of whether it's internal.

**"My system just summarizes text — is that 'generating' content?"**
Yes. Summarization produces new text that didn't exist before. It triggers Art. 50(2) content marking obligations.

**"I let users edit AI outputs before publishing — does that change things?"**
It may qualify as "human editorial oversight" for the Art. 50(4) exception for public interest text. But Art. 50(2) machine-readable marking still applies to the original AI output. Mark it, even if humans edit it afterward.

**"My classification was minimal risk, but I'm adding a new feature."**
Re-run this decision tree for every new AI feature. A product can have features at different risk levels — the highest applicable level drives the obligations for that feature.

**"What if I'm not sure?"**
When in doubt, classify up. It's better to over-comply (limited risk measures when you might be minimal) than to under-comply (treating high-risk as limited). The penalties for getting it wrong are significant.
