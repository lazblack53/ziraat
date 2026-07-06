---
document: book-02-architecture/04-prompt-architecture.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Prompt Architecture

## Twee promptlagen

1. **Agentdefinities** (`.claude/agents/*.md`) — persistent gedrag: rol, rapporttoegang, mapscope, werkwijze, outputformat, grenzen. Format: [agent-template](../governance/agent-template.md).
2. **Taakprompten** (per IC-run of ad-hocvraag) — doel, context, input-scope, opdracht, outputformat, constraints. Format: [prompt-template](../governance/prompt-template.md).

## Conventies

- **Taal:** Nederlands als draagtaal, Turkse vaktermen (faiz, enflasyon, yabancı oranları) onvertaald; consistent met bestaande agents.
- **Paden:** altijd absoluut (`/home/developer/projects/ziraat/…`).
- **Datatoegang in de prompt:** de drie standaard `lees_pdf.py`-aanroepen, met `--recent` als eerste keus; `--lijst` alleen indien nodig (±750 paden).
- **Outputcontract:** vaste kopjes per agent zodat consolidatie mechanisch kan; trade-voorstellen altijd met entry/stop/target/R:R/bron.
- **Scope-discipline:** een prompt noemt alleen de mappen die de agent nodig heeft; "lees alles" is verboden (tokenprincipe, zie `book-03-operations/08-token-management-process.md`).

## Anti-patterns (uit geleden schade)

- Targets zonder methode-vermelding → Methode A-fouten glippen door (DR-003).
- Draft-output presenteren als besluit → Constitution, investeringsprincipes: draft ≠ besluit.
- Prompt die memory-inhoud integraal herhaalt → tokenverspilling; verwijs naar de memory-naam.
- Aannemen dat "0 pdfs" = geen publicatie → pipeline-les `feedback_pipeline_scraper_gaps`.

## Wijzigingsproces

Kleine verduidelijkingen: direct + change-log-regel. Gedragsveranderende wijzigingen: Decision Record + review volgens `book-03-operations/02-review-process.md`. Optimalisatie-cyclus: `book-04-evolution/03-prompt-evolution.md`.
