---
document: book-02-architecture/00-architecture-overview.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: CTO)
technical_owner: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Architecture Overview

## Lagen

```
Gebruiker (chat, @Agent-Naam)
   │
Master-Stratejist (orkestratie, IC-consolidatie)
   │
Specialisten: Macro-Stratejist · Hisse-Analist · Teknik-Analist · Risk-Yoneticisi
   │
Toolinglaag: lees_pdf.py (PyMuPDF + openpyxl) · Read (portfolioscreenshots)
   │
Datalaag: raporlar/ (ZFG + İş Yatırım) · portföyüm/ · project-memory
```

## Componenten

- **`lees_pdf.py`** — enige extractietool. PDF via `fitz`, Excel via `openpyxl` (`data_only=True`). Modi: bestand lezen, `--lijst`, `--recent N` (voorkeursingang voor verse rapporten). Nederlandse naamgeving in code.
- **`raporlar/`** — ±750 bestanden, twee brokersubtrees, genummerde categorieën, maand-/jaarsubmappen. Volledige structuur en naamgevingsstandaard: zie [07-knowledge-architecture](07-knowledge-architecture.md) en CLAUDE.md.
- **Agents** — vijf definities in `.claude/agents/`, allemaal sonnet + project-memory (DR-004). Detail: [03-ai-agent-architecture](03-ai-agent-architecture.md).
- **Memory** — persistente projectmemory (index `MEMORY.md`) voor IC-besluiten, feedback, marktsignalen en pipeline-lessen.
- **Blueprint (`blueprint/`)** — deze documentatielaag; besturingssysteem per Meta-Architecture §16.

## Ontwerpprincipes

1. **Eén extractiepad.** Alle rapportinhoud loopt via `lees_pdf.py`; geen ad-hoc PDF-parsing per agent.
2. **Scoped datatoegang.** Elke agent leest alleen zijn toegewezen mappen (tokenbeheersing + focus).
3. **Stateless agents, stateful memory.** Agents dragen geen sessiestaat; alles wat runs overleeft staat in project-memory of de Blueprint.
4. **Absolute paden.** Agentprompts gebruiken hardcoded `/home/developer/projects/ziraat/…` zodat Bash-aanroepen omgevingsonafhankelijk zijn.

## Bekende beperkingen

- Sommige PDF's zijn image-based (m.n. `7. Haftalık Teknik Hisse Önerileri`): <500 tekens output = waarschijnlijk image-based.
- Scraper-pipeline kan stil falen ("0 pdfs" ≠ geen publicatie); evergreen links vereisen hash-check.
- Geen realtime koersdata; tweede realtime-bron staat op de data-gap-checklist.
