<!-- Verification status: see LAST_VERIFIED.md -->

# Contesto Italiano per l'AI Act

Riferimenti specifici per l'implementazione dell'AI Act in Italia, incluse le autorità competenti, le normative collegate e le considerazioni pratiche per le PMI italiane.

## Legge nazionale sull'IA — Legge 23 settembre 2025, n. 132

L'Italia è stato tra i primi Stati membri ad approvare una legge nazionale di accompagnamento all'AI Act.

- **Legge n. 132/2025** — "Disposizioni e deleghe al Governo in materia di intelligenza artificiale"
- Pubblicata in **GU Serie Generale n. 223 del 25 settembre 2025**; **in vigore dal 10 ottobre 2025** (vacatio di 15 giorni)
- Testo: https://www.gazzettaufficiale.it/eli/id/2025/09/25/25G00143/sg
- Contenuti chiave: principi nazionali sull'uso dell'IA, deleghe al Governo per l'adeguamento all'AI Act, disposizioni penali (incluse aggravanti per reati commessi mediante sistemi di IA), sanzioni amministrative, e designazione delle autorità nazionali
- **Autorità nazionali designate**: **AgID** (autorità di notifica) e **ACN** (autorità di sorveglianza del mercato), fatte salve le competenze del **Garante** in materia di dati personali
- Sanzioni pecuniarie previste dalla legge nazionale fino a circa **774.685 €**, oltre a misure interdittive ex D.Lgs. 231/2001 in taluni casi

> **Nota (luglio 2026)**: A livello UE il **Digital Omnibus on AI** (adottato giugno 2026) ha posticipato gli obblighi high-risk — Annex III standalone al **2 dicembre 2027**, prodotti regolati (Annex I) al **2 agosto 2028**. Gli obblighi di trasparenza dell'Art. 50 restano al **2 agosto 2026**. Verificare il riferimento finale in GUUE su EUR-Lex.

## Autorità Competenti in Italia

### AgID — Agenzia per l'Italia Digitale
- Ruolo nell'ecosistema AI: coordinamento delle iniziative AI nella PA
- Riferimento per linee guida sull'uso dell'AI nella pubblica amministrazione
- Sito: https://www.agid.gov.it

### Garante per la Protezione dei Dati Personali
- Autorità di supervisione per aspetti GDPR collegati all'AI Act
- Ha già preso posizioni forti sull'AI (es. caso ChatGPT 2023)
- Sito: https://www.garanteprivacy.it

### ACN — Agenzia per la Cybersicurezza Nazionale
- Competenze su aspetti di cybersecurity dei sistemi AI
- Standard di sicurezza per sistemi AI ad alto rischio
- Sito: https://www.acn.gov.it

### Autorità Nazionali Competenti (designate dalla Legge 132/2025)
- **ACN** — Agenzia per la Cybersicurezza Nazionale: autorità di sorveglianza del mercato
- **AgID** — Agenzia per l'Italia Digitale: autorità di notifica
- **Garante Privacy**: mantiene le competenze sui profili di protezione dei dati personali
- Per gli aggiornamenti sulle modalità operative, monitorare le comunicazioni ufficiali di AgID e ACN

## Normative Collegate

### GDPR (Reg. UE 2016/679) — Interconnessione con l'AI Act
L'AI Act non sostituisce il GDPR ma lo integra. Punti di contatto chiave:

- **Art. 22 GDPR** — Diritto di non essere sottoposto a decisioni automatizzate: si applica in aggiunta all'AI Act per decisioni con effetti giuridici o significativi
- **Basi giuridiche per il trattamento**: il trattamento di dati personali tramite AI richiede comunque una base giuridica GDPR valida
- **DPIA**: la Valutazione d'Impatto sulla Protezione dei Dati è spesso necessaria per sistemi AI che trattano dati personali
- **Privacy by design**: si allinea con i requisiti di risk management dell'AI Act

### Codice del Consumo (D.Lgs. 206/2005)
- Pratiche commerciali scorrette: un sistema AI che inganna i consumatori può violare sia l'AI Act che il Codice del Consumo
- Obblighi informativi precontrattuali: si sommano agli obblighi di trasparenza AI Act

### D.Lgs. 196/2003 (Codice Privacy) come modificato dal D.Lgs. 101/2018
- Norme nazionali di adeguamento al GDPR
- Sanzioni amministrative e penali specifiche italiane

## Considerazioni per PMI Italiane

### Agevolazioni AI Act per PMI
L'AI Act prevede alcune misure specifiche per le PMI (Art. 62):
- Sanzioni proporzionate (il minore tra importo fisso e percentuale del fatturato)
- Accesso a sandbox regolamentari per testare sistemi AI in ambiente controllato
- Supporto e guida specifici dalle autorità nazionali
- Modelli semplificati di documentazione tecnica per i sistemi ad alto rischio (attesi)

### Struttura di Costi Tipica per la Compliance
Per una PMI che sviluppa SaaS con AI integrata (rischio limitato):

**Costi una tantum:**
- Classificazione del rischio e documentazione: 2-5 giorni lavoro interni
- Aggiornamento privacy policy e ToS: consulenza legale 500-2.000€
- Implementazione tecnica (disclosure, marking): 3-10 giorni sviluppo

**Costi ricorrenti:**
- Review trimestrale compliance: 1 giorno/trimestre
- Aggiornamento documentazione: al rilascio di ogni nuova feature AI
- Monitoraggio normativo: integrato nelle attività ordinarie

### Template Documentazione in Italiano

#### Informativa AI per Utenti (Banner/Modal)
```
AVVISO: UTILIZZO DI INTELLIGENZA ARTIFICIALE

Questo servizio utilizza un sistema di intelligenza artificiale per
[DESCRIZIONE FUNZIONALITÀ]. 

Stai interagendo con un assistente automatizzato, non con un operatore umano.
Le risposte vengono generate automaticamente e potrebbero contenere 
imprecisioni.

[NOME AZIENDA] - [INDIRIZZO] - P.IVA [NUMERO]
Per informazioni: [EMAIL CONTATTO]

Informativa completa: [LINK PRIVACY POLICY]
```

#### Clausola per Termini di Servizio
```
UTILIZZO DELL'INTELLIGENZA ARTIFICIALE

[X]. Descrizione del Servizio AI
Il Servizio include funzionalità basate su intelligenza artificiale,
specificamente [DESCRIZIONE]. Tali funzionalità sono alimentate da
modelli di linguaggio di terze parti (Anthropic Claude) integrati
tramite API nel nostro sistema.

[X+1]. Limitazioni e Responsabilità
a) I contenuti generati dall'intelligenza artificiale sono forniti
   "così come sono" e potrebbero contenere errori o imprecisioni.
b) Il Servizio non sostituisce la consulenza professionale di
   [TIPO PROFESSIONISTA].
c) L'Utente è responsabile della verifica delle informazioni
   ricevute prima di assumere decisioni sulla base delle stesse.
d) [NOME AZIENDA] non garantisce l'accuratezza, la completezza
   o l'adeguatezza dei contenuti generati dall'AI.

[X+2]. Trasparenza
a) I contenuti generati dall'AI sono contrassegnati come tali
   sia in modo visibile che in formato leggibile dalle macchine.
b) L'Utente viene informato quando interagisce con un sistema
   automatizzato.
c) In conformità al Regolamento UE 2024/1689 (AI Act), Art. 50.

[X+3]. Trattamento dei Dati
I dati forniti dall'Utente durante l'interazione con il sistema AI
sono trattati in conformità al GDPR (Reg. UE 2016/679) e alla nostra
Informativa Privacy disponibile al link [URL].
```

#### Registro Sistemi AI (Template)
```markdown
# Registro Sistemi AI — [NOME AZIENDA]
## Ultimo aggiornamento: [DATA]

### Sistema 1: [NOME]
- **Descrizione**: [cosa fa]
- **Modello AI**: [es. Claude Sonnet via API]
- **Ruolo aziendale**: Provider
- **Classificazione rischio**: Limitato (Art. 50)
- **Categorie Annex III**: Nessuna applicabile
- **Utenti target**: [chi lo usa]
- **Dati trattati**: [quali dati personali]
- **Base giuridica GDPR**: [consenso/legittimo interesse/etc.]
- **Disclosure implementata**: Sì/No — [dettaglio]
- **Marcatura contenuti**: Sì/No — [dettaglio tecnico]
- **Data primo deployment**: [DATA]
- **Ultima review compliance**: [DATA]
- **Prossima review prevista**: [DATA]
- **Responsabile compliance**: [NOME]
```

## Fatturazione e Aspetti Fiscali

Se offri servizi di compliance AI Act come consulenza:
- Codice ATECO: 62.02.00 (Consulenza nel settore delle tecnologie dell'informatica) o 62.09.09
- IVA: 22% standard
- Fatturazione elettronica: obbligatoria via SDI come per tutti i servizi B2B

## Risorse Utili

- **Testo ufficiale AI Act in italiano**: https://eur-lex.europa.eu/legal-content/IT/TXT/?uri=CELEX:32024R1689
- **AI Act Explorer**: https://artificialintelligenceact.eu/ai-act-explorer/
- **Compliance Checker**: https://artificialintelligenceact.eu/compliance-checker/
- **Linee guida pratiche proibite**: Commissione EU, 4 febbraio 2025
- **GPAI Code of Practice**: Pubblicato 10 luglio 2025

## Calendario Azioni Raccomandate

| Quando | Azione |
|--------|--------|
| Subito | Inventario sistemi AI + classificazione rischio |
| Subito | Documentare la formazione AI literacy del team |
| Entro H1 2026 | Implementare disclosure Art. 50 in tutti i prodotti |
| Entro H1 2026 | Aggiornare privacy policy e ToS |
| Entro H1 2026 | Implementare marcatura contenuti AI in formato machine-readable |
| **2 ago 2026** | Compliance completa Art. 50 (trasparenza) — invariata |
| 2 dic 2026 | Fine grace period marcatura Art. 50(2) per sistemi già sul mercato |
| **2 dic 2027** | High-risk Annex III standalone (posticipato dall'Omnibus) |
| 2 ago 2028 | High-risk in prodotti regolati (Annex I) |
| Trimestrale | Review documentazione e compliance |
