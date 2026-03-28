# 🇪🇺 AI Act Compliance Skill for Claude Code

> La prima skill per Claude Code (e agenti AI compatibili) che guida la compliance al Regolamento EU 2024/1689 (AI Act) per chi costruisce SaaS con AI integrata.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Agent Skills Standard](https://img.shields.io/badge/Agent_Skills-SKILL.md-purple.svg)](https://agentskills.io)
[![AI Act](https://img.shields.io/badge/EU_AI_Act-2024%2F1689-yellow.svg)](https://artificialintelligenceact.eu/)

---

## Perché questa skill

Se costruisci SaaS con Claude API, OpenAI, o qualsiasi modello AI via API, l'AI Act ti classifica come **Provider** — non deployer. Questo comporta obblighi specifici di trasparenza, documentazione e governance che entrano in piena applicazione il **2 agosto 2026**.

Questa skill integra la compliance direttamente nel tuo workflow di sviluppo: classificazione del rischio, checklist operative, template di documentazione, pattern di codice pronti all'uso, e contesto normativo italiano.

## Cosa include

| File | Contenuto |
|------|-----------|
| `SKILL.md` | Workflow di classificazione rischio, checklist pre-deploy, template documentazione, code patterns |
| `references/checklist-completa.md` | **219 punti di verifica** articolo per articolo, organizzati per fase |
| `references/high-risk-requirements.md` | Obblighi completi per sistemi ad alto rischio (Art. 9-17) |
| `references/transparency-implementation.md` | Guida tecnica Art. 50 con codice pronto (React, Python, SQL, API) |
| `references/italian-context.md` | Contesto Italia: autorità, normative collegate, template in italiano |
| `references/auto-update.md` | Workflow di aggiornamento normativo con fonti e changelog |

## Installazione

### Claude Code (terminale)

```bash
# Opzione 1: Clone nella directory skills del progetto
git clone https://github.com/studio121-develop/ai-act-compliance-skill.git .claude/skills/ai-act-compliance

# Opzione 2: Installazione globale (disponibile in tutti i progetti)
git clone https://github.com/studio121-develop/ai-act-compliance-skill.git ~/.claude/skills/ai-act-compliance
```

### Claude.ai (web/app)

1. [Scarica il file ZIP](https://github.com/studio121-develop/ai-act-compliance-skill/archive/refs/heads/main.zip)
2. Vai su **Customize > Skills**
3. Carica il file ZIP

### Altri agenti compatibili (Codex, Cursor, Gemini CLI)

```bash
# OpenAI Codex CLI
cp -r ai-act-compliance ~/.codex/skills/

# Cursor / altri agenti SKILL.md-compatibili
cp -r ai-act-compliance .skills/
```

## Utilizzo

La skill si attiva automaticamente quando lavori su progetti AI. Puoi anche invocarla esplicitamente:

```
Classifica il rischio AI Act del mio progetto
```

```
Genera la documentazione AI Act compliance per il mio SaaS
```

```
Checklist pre-deploy AI Act
```

```
Aggiorna la skill AI Act compliance con le ultime novità normative
```

### Esempi di trigger automatici

- Stai costruendo un chatbot → la skill suggerisce gli obblighi Art. 50
- Integri Claude API in un prodotto → la skill ti classifica come Provider
- Aggiungi feature AI a un e-commerce → la skill valuta il rischio
- Prepari il deploy di un SaaS con AI → la skill lancia la checklist pre-deploy

## Per chi è

- **SaaS builder** che integrano AI via API (Claude, OpenAI, Mistral, etc.)
- **Agenzie digitali** che costruiscono prodotti AI per clienti
- **Indie hacker** e **vibe coder** che usano AI nei loro progetti
- **PMI italiane** ed europee che devono adeguarsi all'AI Act
- **Consulenti** che assistono clienti nella compliance AI

## Compatibilità

| Piattaforma | Supporto |
|-------------|----------|
| Claude Code | ✅ Nativo |
| Claude.ai (Pro/Max/Team/Enterprise) | ✅ Via upload |
| Claude API (code execution) | ✅ Via Skills API |
| OpenAI Codex CLI | ✅ Formato SKILL.md compatibile |
| Cursor | ✅ Formato SKILL.md compatibile |
| Gemini CLI | ✅ Formato SKILL.md compatibile |

## Aggiornamento normativo

La skill non si auto-aggiorna, ma include un workflow strutturato. Chiedi a Claude:

```
Aggiorna la skill AI Act compliance con le ultime novità normative
```

Claude cercherà aggiornamenti da fonti primarie EU e italiane, aggiornerà i file e terrà traccia nel changelog.

**Frequenza raccomandata**: mensile fino ad agosto 2026, trimestrale dopo.

## Timeline AI Act

| Data | Cosa | Stato |
|------|------|-------|
| Feb 2025 | Pratiche proibite + AI literacy | ✅ In vigore |
| Ago 2025 | Obblighi GPAI + governance | ✅ In vigore |
| **Ago 2026** | **Trasparenza Art. 50 + high-risk standalone** | ⚠️ Prossima |
| Ago 2027 | High-risk in prodotti regolamentati | 🔜 |

## Contribuire

Le Pull Request sono benvenute. In particolare:

- 🐛 Segnalazione errori normativi
- 📝 Aggiornamenti normativi (nuove linee guida, standard, sentenze)
- 🌍 Traduzioni (tedesco, francese, spagnolo)
- 💻 Nuovi code pattern per framework specifici
- 📋 Espansione checklist per settori verticali

## Licenza

Apache License 2.0 — vedi [LICENSE](LICENSE).

## Autore

**Studio121 Srls** — Web design, digital communications & AI-powered products.
Ragusa, Sicilia 🇮🇹

- Web: [studio121.it](https://studio121.it)
- GitHub: [@studio121-develop](https://github.com/studio121-develop)

---

> ⚠️ **Disclaimer**: Questa skill fornisce indicazioni operative per la compliance all'AI Act ma non costituisce consulenza legale. Per casi specifici, consultare un professionista specializzato in diritto digitale europeo.
