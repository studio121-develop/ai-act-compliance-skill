# Checklist Compliance AI Act — Versione Esaustiva

Checklist articolo per articolo per provider SaaS che integrano AI via API. Organizzata per fase: pre-sviluppo, sviluppo, pre-deploy, post-deploy.

---

## FASE 0 — GOVERNANCE E ORGANIZZAZIONE

### 0.1 Ruoli e Responsabilità
- [ ] Identificare il responsabile compliance AI Act nell'organizzazione
- [ ] Definire se l'azienda è Provider o Deployer per ciascun sistema AI
- [ ] Se si opera come Provider: documentare che si è il soggetto che "immette sul mercato" il sistema AI
- [ ] Se si modifica sostanzialmente un sistema AI di terzi: documentare che si assumono obblighi da Provider (Art. 25)
- [ ] Definire la catena di responsabilità: provider modello (es. Anthropic) → provider sistema (tu) → deployer (cliente)
- [ ] Nominare un rappresentante autorizzato se l'azienda è extra-UE (Art. 22)

### 0.2 AI Literacy (Art. 4) — IN VIGORE DAL 2 FEB 2025
- [ ] Valutare il livello di competenza AI del team
- [ ] Pianificare e documentare formazione AI per tutti i dipendenti coinvolti
- [ ] Formazione deve coprire: funzionamento dei modelli AI, limitazioni, rischi, obblighi normativi
- [ ] Conservare registri della formazione (date, partecipanti, contenuti)
- [ ] Aggiornare la formazione almeno annualmente o al cambio significativo di tecnologia
- [ ] Estendere requisito literacy anche a freelancer e collaboratori esterni coinvolti nell'AI

### 0.3 Inventario Sistemi AI
- [ ] Creare un registro completo di tutti i sistemi AI utilizzati/forniti
- [ ] Per ogni sistema documentare: nome, descrizione, modello AI sottostante, scopo previsto
- [ ] Per ogni sistema documentare: dati trattati, utenti target, data deployment
- [ ] Per ogni sistema documentare: ruolo aziendale (Provider/Deployer), classificazione rischio
- [ ] Aggiornare il registro ad ogni nuova feature AI o modifica sostanziale
- [ ] Conservare versioni storiche del registro (version control)

---

## FASE 1 — CLASSIFICAZIONE DEL RISCHIO

### 1.1 Verifica Pratiche Proibite (Art. 5) — IN VIGORE DAL 2 FEB 2025
- [ ] Verificare che il sistema NON usa tecniche subliminali per manipolare il comportamento
- [ ] Verificare che il sistema NON sfrutta vulnerabilità di gruppi specifici (età, disabilità, situazione sociale)
- [ ] Verificare che il sistema NON effettua social scoring (valutazione della persona basata su comportamento sociale)
- [ ] Verificare che il sistema NON usa identificazione biometrica remota in tempo reale in spazi pubblici (salvo eccezioni tassative)
- [ ] Verificare che il sistema NON effettua scraping non mirato di immagini facciali da internet o CCTV
- [ ] Verificare che il sistema NON inferisce emozioni in contesti lavorativi o educativi (salvo motivi medici/sicurezza)
- [ ] Verificare che il sistema NON categorizza biometricamente le persone per dedurre razza, opinioni politiche, orientamento sessuale, etc.
- [ ] Verificare che il sistema NON usa AI predittiva per valutare il rischio di commissione reati basandosi su profiling
- [ ] Documentare l'esito della verifica con data e responsabile

### 1.2 Verifica Alto Rischio (Annex III)
- [ ] Controllare CIASCUNA delle 8 categorie Annex III per ogni sistema AI:
  - [ ] 1. Biometria: il sistema identifica/categorizza persone tramite dati biometrici?
  - [ ] 2. Infrastrutture critiche: il sistema gestisce energia, trasporti, acqua, gas, riscaldamento?
  - [ ] 3. Istruzione: il sistema influenza ammissioni, valutazioni, esami, percorsi formativi?
  - [ ] 4. Impiego: il sistema influenza assunzioni, screening CV, valutazioni performance, promozioni, licenziamenti?
  - [ ] 5. Servizi essenziali: il sistema influenza affidabilità creditizia, assicurazioni, accesso a servizi pubblici, priorità emergenze?
  - [ ] 6. Forze dell'ordine: il sistema valuta prove, predice crimini, effettua profiling?
  - [ ] 7. Migrazione: il sistema valuta richieste di visto/asilo, sorveglia frontiere?
  - [ ] 8. Giustizia/Democrazia: il sistema assiste in ricerche giuridiche, risoluzione controversie, processi elettorali?
- [ ] Se sistema rientra in Annex III → verificare se si applica deroga Art. 6(3):
  - [ ] Il sistema svolge un compito procedurale ristretto?
  - [ ] Il sistema migliora il risultato di un'attività umana già completata?
  - [ ] Il sistema rileva pattern decisionali senza sostituire/influenzare la valutazione umana?
  - [ ] Il sistema svolge un compito preparatorio a una valutazione Annex III?
- [ ] Se il sistema profila individui (trattamento automatizzato dati personali per valutare aspetti della persona) → la deroga Art. 6(3) NON si applica → è SEMPRE alto rischio
- [ ] Documentare la classificazione con motivazione dettagliata
- [ ] Se si dichiara "non alto rischio" per sistema Annex III: documentare prima dell'immissione sul mercato (Art. 6(3))

### 1.3 Verifica Rischio Trasparenza (Art. 50)
- [ ] Il sistema interagisce direttamente con esseri umani? → Obbligo disclosure
- [ ] Il sistema genera testo sintetico? → Obbligo marcatura
- [ ] Il sistema genera immagini sintetiche? → Obbligo marcatura
- [ ] Il sistema genera audio sintetico? → Obbligo marcatura
- [ ] Il sistema genera video sintetico? → Obbligo marcatura
- [ ] Il sistema riconosce emozioni? → Obbligo informativa
- [ ] Il sistema categorizza biometricamente? → Obbligo informativa
- [ ] Il sistema genera/manipola deepfake? → Obbligo disclosure specifico
- [ ] Il sistema genera testo per informare il pubblico su temi di interesse pubblico? → Obbligo disclosure specifico
- [ ] Documentare tutti gli obblighi applicabili con piano di implementazione

---

## FASE 2 — SVILUPPO (Design & Build)

### 2.1 Trasparenza — Disclosure Interazione AI (Art. 50.1)
- [ ] Implementare banner/modal visibile PRIMA della prima interazione AI
- [ ] Il messaggio di disclosure deve essere "chiaro e distinguibile" — NON nascosto nei ToS
- [ ] Utilizzare linguaggio comprensibile per l'utente target (italiano per mercato IT)
- [ ] Includere: che è un sistema AI, cosa fa, quali sono i suoi limiti
- [ ] Implementare reminder periodico nelle conversazioni lunghe
- [ ] Testare che la disclosure sia visibile su tutti i device (mobile, desktop, tablet)
- [ ] Testare con screen reader per accessibilità (WCAG 2.1)
- [ ] Documentare l'implementazione tecnica della disclosure

### 2.2 Trasparenza — Marcatura Contenuti AI (Art. 50.2)
- [ ] Implementare marcatura machine-readable su TUTTI i contenuti generati dall'AI
- [ ] Scegliere e implementare standard di marcatura (C2PA / IPTC / metadata custom)
- [ ] Includere nei metadati: flag ai_generated, provider modello, nome sistema, timestamp
- [ ] Implementare marcatura visibile per l'utente finale (label, badge, footer)
- [ ] Verificare che la marcatura sia robusta (non facilmente rimovibile dall'utente)
- [ ] Implementare meccanismo di rilevamento downstream (per chi riceve il contenuto)
- [ ] Se il contenuto è "assistive function" per editing standard → documentare perché l'esenzione si applica
- [ ] Testare la marcatura end-to-end: generazione → storage → display → export

### 2.3 Trasparenza — Deepfake e Testo di Interesse Pubblico (Art. 50.4)
- [ ] Se si generano immagini/audio/video che somigliano a persone reali: implementare disclosure visibile
- [ ] Se si genera testo per informare il pubblico: implementare disclosure
- [ ] Per contenuti artistici/satirici: la disclosure deve esistere ma non ostacolare la fruizione
- [ ] Se contenuto ha supervisione editoriale umana + responsabilità editoriale: documentare l'esenzione

### 2.4 Informativa Privacy AI (GDPR + AI Act)
- [ ] Aggiornare privacy policy con sezione dedicata all'uso dell'AI
- [ ] Specificare quali dati vengono inviati al modello AI
- [ ] Specificare la base giuridica GDPR per il trattamento AI (consenso/legittimo interesse/contratto)
- [ ] Specificare il provider del modello AI e la sua policy di data retention
- [ ] Specificare se i dati vengono usati per training del modello (tipicamente NO con API commerciali)
- [ ] Informare sull'esistenza di processi decisionali automatizzati (Art. 22 GDPR)
- [ ] Garantire il diritto di opt-out da decisioni puramente automatizzate (Art. 22 GDPR)
- [ ] Se si trattano dati particolari (Art. 9 GDPR): valutare DPIA
- [ ] Implementare data minimization: inviare al modello solo i dati strettamente necessari
- [ ] Implementare pseudonimizzazione/anonimizzazione dove possibile prima dell'invio al modello

### 2.5 Termini di Servizio
- [ ] Aggiornare ToS con clausola sull'uso dell'AI
- [ ] Specificare: descrizione funzionalità AI, limitazioni, esclusione responsabilità per imprecisioni
- [ ] Specificare: che i contenuti AI non sostituiscono consulenza professionale
- [ ] Specificare: responsabilità dell'utente nella verifica dei contenuti AI
- [ ] Specificare: conformità all'AI Act (Reg. UE 2024/1689)
- [ ] Far revisionare le clausole da un legale

### 2.6 Data Governance (buona pratica per tutti, obbligatorio per high-risk)
- [ ] Documentare quali dati vengono inviati al modello AI per ogni funzionalità
- [ ] Implementare filtri di input: rimuovere dati sensibili non necessari prima dell'invio
- [ ] Implementare filtri di output: controllare le risposte AI prima di mostrarle all'utente
- [ ] Implementare rate limiting per prevenire abusi
- [ ] Implementare content moderation sugli output AI
- [ ] Documentare la catena di trattamento dati: utente → tuo sistema → API provider → risposta → utente

### 2.7 Human Oversight
- [ ] Implementare meccanismo per disabilitare funzionalità AI ("kill switch")
- [ ] Implementare meccanismo per l'utente di segnalare risposte inappropriate (feedback/flag)
- [ ] Definire processo di escalation: quando e come un operatore umano interviene
- [ ] Per decisioni consequenziali: implementare step di revisione umana obbligatorio
- [ ] Testare il kill switch end-to-end
- [ ] Documentare il processo di oversight

### 2.8 Logging e Audit Trail
- [ ] Implementare logging di tutte le interazioni AI (pseudonimizzate)
- [ ] Log deve includere: timestamp, tipo interazione, disclosure mostrata, contenuto marcato
- [ ] Log deve includere: modello utilizzato, versione sistema, eventuali errori
- [ ] Definire retention period per i log (almeno 6 mesi raccomandato, verificare con GDPR)
- [ ] Proteggere i log da manomissione (integrità)
- [ ] Implementare meccanismo di export log per audit

### 2.9 Accuratezza e Robustezza (Art. 15 - buona pratica per tutti)
- [ ] Documentare le limitazioni note del sistema AI
- [ ] Implementare gestione degli errori per fallimenti API (timeout, rate limit, errori modello)
- [ ] Implementare fallback graceful quando l'AI non è disponibile
- [ ] Testare il comportamento del sistema con input adversariali (prompt injection)
- [ ] Implementare protezioni base contro prompt injection
- [ ] Monitorare la qualità delle risposte AI nel tempo

### 2.10 Cybersecurity (Art. 15 - buona pratica per tutti)
- [ ] Proteggere le API key del modello AI (variabili ambiente, secrets manager)
- [ ] Implementare HTTPS per tutte le comunicazioni con l'API AI
- [ ] Implementare autenticazione utente prima dell'accesso alle funzionalità AI
- [ ] Rate limiting per endpoint AI
- [ ] Monitoraggio per utilizzo anomalo (attacchi, abusi)
- [ ] Data Processing Agreement (DPA) firmato con il provider AI

---

## FASE 3 — PRE-DEPLOYMENT

### 3.1 Documentazione Tecnica
- [ ] Creare/aggiornare file `AI_ACT_COMPLIANCE.md` nella root del progetto
- [ ] Compilare tutte le sezioni: descrizione sistema, classificazione, modello AI, trasparenza, dati, oversight, rischi
- [ ] Far revisionare la documentazione internamente
- [ ] Conservare la documentazione in version control

### 3.2 Verifica Contrattuale
- [ ] Verificare che il contratto con il provider AI (es. Anthropic Terms of Service) sia compatibile con gli obblighi AI Act
- [ ] Verificare la Data Processing Agreement con il provider AI
- [ ] Se si hanno clienti B2B che usano il sistema come deployer: fornire loro le istruzioni d'uso necessarie per la loro compliance

### 3.3 Test di Compliance
- [ ] Test disclosure: verificare che l'informativa AI sia visibile in tutti i percorsi utente
- [ ] Test marcatura: verificare che i metadata AI siano presenti su tutti i contenuti generati
- [ ] Test kill switch: verificare che le funzionalità AI possano essere disabilitate
- [ ] Test human oversight: verificare che il processo di escalation funzioni
- [ ] Test logging: verificare che tutte le interazioni siano correttamente loggate
- [ ] Test accessibilità: verificare che disclosure e label siano accessibili (screen reader, contrasto)
- [ ] Test mobile: verificare la compliance su tutti i dispositivi target
- [ ] Test privacy: verificare che la privacy policy sia aggiornata e accessibile
- [ ] Test ToS: verificare che i termini di servizio siano aggiornati

### 3.4 Review Finale
- [ ] Checklist Art. 5 (pratiche proibite): confermata
- [ ] Classificazione rischio: documentata e confermata
- [ ] Art. 50 obblighi: tutti implementati e testati
- [ ] Privacy policy: aggiornata
- [ ] ToS: aggiornati
- [ ] Documentazione tecnica: completa e aggiornata
- [ ] Team formato su AI literacy: confermato
- [ ] DPA con provider AI: in essere

---

## FASE 4 — POST-DEPLOYMENT

### 4.1 Monitoraggio Continuo
- [ ] Revisione trimestrale della classificazione rischio (nuove feature → nuova classificazione)
- [ ] Monitoraggio segnalazioni utente su risposte AI inappropriate
- [ ] Analisi log per identificare pattern problematici
- [ ] Verifica periodica che disclosure e marcatura funzionino correttamente
- [ ] Aggiornamento documentazione ad ogni release con feature AI
- [ ] Monitoraggio aggiornamenti normativi (vedi references/auto-update.md)

### 4.2 Gestione Incidenti
- [ ] Definire cosa costituisce un "incidente AI" per il tuo sistema
- [ ] Esempi: risposta AI che causa danno all'utente, leak di dati tramite AI, discriminazione sistematica
- [ ] Procedura di risposta: identificazione → contenimento → analisi → risoluzione → report
- [ ] Per sistemi high-risk: obbligo di segnalazione alle autorità di sorveglianza entro 15 giorni (Art. 73)
- [ ] Conservare registro incidenti con azioni correttive

### 4.3 Aggiornamenti e Modifiche
- [ ] Ogni modifica sostanziale al sistema AI → ri-classificazione rischio
- [ ] Cambio modello AI (es. da Claude Sonnet a Claude Opus) → aggiornare documentazione
- [ ] Cambio system prompt significativo → verificare che la classificazione sia ancora corretta
- [ ] Nuova funzionalità AI → percorrere tutta la checklist per la nuova feature
- [ ] Aggiornamento delle condizioni del provider AI → verificare compatibilità

### 4.4 Cooperazione con Autorità (Art. 21)
- [ ] Essere preparati a fornire documentazione alle autorità su richiesta
- [ ] Conservare registri di compliance accessibili e organizzati
- [ ] Designare punto di contatto per le autorità competenti
- [ ] Per sistemi registrati nel database EU: mantenere aggiornate le informazioni

---

## REQUISITI AGGIUNTIVI PER SISTEMI HIGH-RISK

Se il tuo sistema è classificato come alto rischio, aggiungi questi requisiti (vedi anche references/high-risk-requirements.md):

### HR.1 Risk Management System (Art. 9)
- [ ] Stabilire un sistema di gestione del rischio continuo per l'intero ciclo di vita
- [ ] Identificare e analizzare rischi noti e ragionevolmente prevedibili
- [ ] Stimare e valutare rischi da uso previsto E da uso improprio ragionevolmente prevedibile
- [ ] Adottare misure di gestione del rischio appropriate
- [ ] Testare il sistema per identificare le misure più appropriate
- [ ] Documentare tutto il processo di risk management

### HR.2 Data Governance (Art. 10)
- [ ] Dataset di training/validazione/test pertinenti e sufficientemente rappresentativi
- [ ] Implementare pratiche di data governance: scelte di design, raccolta, preparazione, etichettatura
- [ ] Esaminare i dati per bias
- [ ] Identificare lacune nei dati

### HR.3 Technical Documentation (Art. 11 + Annex IV)
- [ ] Descrizione generale del sistema AI
- [ ] Descrizione dettagliata degli elementi e del processo di sviluppo
- [ ] Informazioni su monitoraggio, funzionamento e controllo
- [ ] Descrizione del sistema di gestione del rischio
- [ ] Descrizione delle modifiche durante il ciclo di vita
- [ ] Lista degli standard armonizzati applicati
- [ ] Descrizione della valutazione di conformità effettuata
- [ ] Dichiarazione di conformità UE

### HR.4 Record-Keeping / Logging (Art. 12)
- [ ] Logging automatico degli eventi durante tutto il ciclo di vita
- [ ] Log devono consentire la tracciabilità del funzionamento
- [ ] Logging proporzionato allo scopo previsto
- [ ] Conformità a standard riconosciuti o specifiche comuni

### HR.5 Transparency to Deployers (Art. 13)
- [ ] Istruzioni d'uso per i deployer includenti:
  - [ ] Identità e contatti del provider
  - [ ] Caratteristiche, capacità, limitazioni del sistema
  - [ ] Scopo previsto e usi impropri prevedibili
  - [ ] Modifiche apportate dal provider nel tempo
  - [ ] Misure di supervisione umana
  - [ ] Durata di vita attesa, manutenzione
  - [ ] Risorse computazionali e hardware necessarie

### HR.6 Human Oversight (Art. 14)
- [ ] Sistema progettato per consentire supervisione umana effettiva
- [ ] Le persone che supervisionano devono poter:
  - [ ] Comprendere pienamente capacità/limitazioni
  - [ ] Monitorare il funzionamento
  - [ ] Decidere di non usare il sistema o ignorare/sovrascrivere l'output
  - [ ] Intervenire o interrompere il funzionamento ("pulsante di stop")

### HR.7 Accuracy, Robustness, Cybersecurity (Art. 15)
- [ ] Livelli di accuratezza appropriati per lo scopo previsto (dichiarati nelle istruzioni)
- [ ] Resilienza a errori, guasti, inconsistenze
- [ ] Resilienza a tentativi non autorizzati di alterare uso o performance
- [ ] Soluzioni di ridondanza tecnica dove appropriato

### HR.8 Quality Management System (Art. 17)
- [ ] Strategia per la conformità normativa
- [ ] Tecniche e procedure per design, sviluppo, test
- [ ] Procedure di esame, test e validazione
- [ ] Specifiche tecniche e standard applicati
- [ ] Sistemi e procedure per la gestione dei dati
- [ ] Sistema di gestione del rischio
- [ ] Sistema di monitoraggio post-market
- [ ] Procedure per segnalazione incidenti
- [ ] Comunicazione con autorità, enti competenti, deployer, utenti

### HR.9 Conformity Assessment
- [ ] Self-assessment (Annex VI) per la maggior parte dei sistemi SaaS
- [ ] Notified body assessment (Annex VII) per sistemi di identificazione biometrica
- [ ] Dichiarazione di conformità UE rilasciata
- [ ] Marcatura CE apposta

### HR.10 Registration
- [ ] Registrazione nel database EU PRIMA dell'immissione sul mercato
- [ ] Aggiornamento entro 14 giorni da modifiche significative

---

## MATRICE TEMPISTICA

| Requisito | Scadenza | Stato |
|-----------|----------|-------|
| Pratiche proibite (Art. 5) | 2 Feb 2025 ✅ | IN VIGORE |
| AI Literacy (Art. 4) | 2 Feb 2025 ✅ | IN VIGORE |
| Obblighi GPAI model provider | 2 Ago 2025 ✅ | IN VIGORE |
| Governance e penalty regime | 2 Ago 2025 ✅ | IN VIGORE |
| **Trasparenza Art. 50** | **2 Ago 2026 ⚠️** | **PROSSIMA SCADENZA** |
| **High-risk Annex III standalone** | **2 Ago 2026 ⚠️** | **PROSSIMA SCADENZA** |
| High-risk in prodotti regolamentati | 2 Ago 2027 | Prossima |
| GPAI modelli pre-esistenti | 2 Ago 2027 | Prossima |
| Sistemi IT su larga scala (Annex X) | 31 Dic 2030 | Futura |
