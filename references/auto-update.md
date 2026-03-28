# Auto-Aggiornamento Normativo

Questa skill non si aggiorna automaticamente, ma contiene un workflow strutturato per aggiornarsi manualmente con l'aiuto di Claude.

## Come Aggiornare la Skill

Quando vuoi verificare se ci sono novità normative, chiedi a Claude:

```
Aggiorna la skill AI Act compliance con le ultime novità normative.
```

Claude eseguirà questo workflow:

### Step 1: Ricerca Novità
Cercare sul web le ultime novità su:
- Aggiornamenti all'AI Act e linee guida della Commissione EU
- Nuovi standard armonizzati CEN/CENELEC JTC 21
- Linee guida dell'AI Office
- Code of Practice (GPAI e Transparency)
- Decisioni e comunicazioni del Garante Privacy italiano
- Aggiornamenti AgID e ACN sull'AI
- Sentenze rilevanti delle corti europee sull'AI

### Step 2: Fonti da Monitorare
Verificare queste fonti per aggiornamenti:

**Fonti primarie EU:**
- https://artificialintelligenceact.eu — Aggiornamenti e analisi AI Act
- https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai — Commissione EU
- https://ai-act-service-desk.ec.europa.eu — Service Desk ufficiale
- https://eur-lex.europa.eu — Testo ufficiale e emendamenti

**Fonti italiane:**
- https://www.garanteprivacy.it — Garante Privacy
- https://www.agid.gov.it — AgID
- https://www.acn.gov.it — Agenzia Cybersicurezza

**Standard e compliance:**
- CEN/CENELEC JTC 21 harmonized standards
- ISO/IEC 42001 (AI Management System)
- NIST AI RMF updates

### Step 3: Aggiornamento Files
Dopo la ricerca, aggiornare i file della skill:

1. **SKILL.md** — Aggiornare date, scadenze, nuovi articoli applicabili
2. **references/high-risk-requirements.md** — Nuovi standard, linee guida
3. **references/transparency-implementation.md** — Nuovi standard tecnici (C2PA, etc.)
4. **references/italian-context.md** — Novità autorità italiane, nuove leggi nazionali
5. **references/checklist-completa.md** — Aggiungere nuovi requisiti emersi

### Step 4: Changelog
Aggiungere una entry al changelog in fondo a questo file.

## Frequenza Raccomandata

| Periodo | Motivazione |
|---------|-------------|
| **Mensile** fino ad Ago 2026 | Fase pre-applicazione, molte linee guida in uscita |
| **Trimestrale** dopo Ago 2026 | Regime di applicazione stabile |
| **Immediatamente** su eventi critici | Nuovi standard armonizzati, sentenze, sanzioni rilevanti |

## Date Chiave da Monitorare

- **Ago 2026**: Applicazione completa Art. 50 + high-risk Annex III standalone
- **Fine 2026**: Prevista finalizzazione Code of Practice on Transparency
- **Ago 2027**: Applicazione high-risk in prodotti regolamentati
- **2027-2030**: Varie scadenze per sistemi IT su larga scala

## Changelog

### v1.0 — Marzo 2026
- Creazione iniziale della skill
- Copertura completa: classificazione rischio, Art. 50, Annex III, sanzioni
- Template documentazione in italiano
- Checklist pre-deployment
- Contesto normativo italiano (Garante, AgID, ACN)
