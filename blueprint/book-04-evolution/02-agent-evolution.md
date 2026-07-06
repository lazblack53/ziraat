---
document: book-04-evolution/02-agent-evolution.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
reviewer: Claude Code (rol: Architecture Guardian, tevens Agent Reviewer)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: tweewekelijks
laatste_review: 2026-07-03
---

# Agent Evolution

Gerichte, bewijsgedreven verbetering van de vijf IC-agents.

## Wanneer evolueert een agent

- Een output-reviewpunt (Book III §A) faalt herhaaldelijk bij dezelfde agent.
- Een feedback-memory wijst op een structurele fout of blinde vlek.
- De rapportstructuur verandert (nieuwe categorie, nieuwe broker) en raakt de mapscope.
- Tokenverbruik van de agent overschrijdt structureel zijn budgetindicatie.

## Werkwijze

1. **Diagnose:** reproduceer de fout op een concrete casus (datum + rapporten); leg vast wat de agent deed vs. had moeten doen.
2. **Kleinste ingreep eerst:** één promptsectie wijzigen, niet de hele agent herschrijven.
3. **Voorstel** via het negen-velden-format ([evolution-engine](01-evolution-engine.md)); gedragswijziging = Decision Record.
4. **Valideer** op de oorspronkelijke casus én één onafhankelijke casus vóór de wijziging definitief is.
5. **Versiebump** in het blueprint-metadatablok van het agentbestand + change-log-regel.

## Per-agent aandachtspunten

De agenda van 2026-07-03 (draft≠besluit + data-gap-sectie bij Master-Stratejist; Methode B + target>trigger-sanity bij Teknik-Analist; CDS/yabancı payı-plicht bij Macro-Stratejist; ZFG-coverage-melding bij Hisse-Analist; broker-uitvoeringsrisico bij Risk-Yoneticisi) is **uitgevoerd** in de v2.0-migratie naar de 10-sectiestandaard (DR-006, Stap 5 voltooid). Nieuwe punten worden hier verzameld tot de volgende evolutieronde.

**Openstaand:** validatie van de v2.0-prompts op de eerstvolgende echte IC-run (verwachte consistentie met besluitlijn 30.06–02.07: GEEN ACTIE bij datagaten); DR-006-review gepland 2026-08-01.
