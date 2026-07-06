---
document: book-03-operations/02-review-process.md
versie: v1.0
status: Approved
strategic_owner: Master-Stratejist (rol: COO)
technical_owner: Risk-Yoneticisi
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Review Process

Twee reviewsoorten: (A) review van analyse-output vóór IC-gebruik, (B) review van Blueprint-/agent-/promptwijzigingen.

## A. Output-review (elke IC-run)

Checklist, af te lopen door Master-Stratejist vóór consolidatie en door Risk-Yoneticisi als eindfilter:

1. **Bronplicht** — elk niveau (entry/stop/target) en elk macro-cijfer heeft rapport + datum. Geen bron = verwijderen of als aanname markeren.
2. **Methodecheck** — targets via Methode B; sanity: target1 > trigger bij long (DR-003-fout was target1 < trigger).
3. **Consistentie** — R:R netto (na kosten) herrekend, niet overgenomen; positiegrootte past bij portefeuille (huidige basis: TP2-saldo).
4. **Data-gap-checklist** — memory `reference_ic_data_gaps` afgelopen; elk open gat expliciet benoemd in het advies.
5. **Versheid** — rapportdatums vermeld; verouderde rapporten gemarkeerd.
6. **Draft ≠ besluit** — auto-gegenereerde drafts worden nooit doorgestuurd zonder deze checklist.

Faalt een punt → advies degradeert naar GEEN ACTIE of terug naar de betreffende specialist.

## B. Wijzigingsreview (Blueprint, agents, prompts)

| Wijziging | Reviewer(s) | Extra vereist |
|---|---|---|
| Typo/verduidelijking | Documentation Manager | change-log-regel |
| Procesdocument (Book III) | COO-rol + betrokken agent-eigenaar | change-log-regel |
| Architectuur (Book II) | Architecture Guardian | Decision Record; volledige [Architecture Review Workflow](../workflows/architecture-review-workflow.md) incl. Change Proposal-intake (ZD-0009) |
| Foundation (Book I) / Constitution | Gebruiker | Decision Record; alleen gebruiker keurt goed |
| Agent nieuw/verwijderd/gedrag | Architecture Guardian + Risk-Yoneticisi bij risico-impact | Decision Record |

## Cadans

Maandelijks één onderhoudsronde over Book II/III-documenten; bevindingen als change-log-regels, structurele punten naar Book IV (innovation backlog t.z.t.).
