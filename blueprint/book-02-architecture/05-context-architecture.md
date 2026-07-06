---
document: book-02-architecture/05-context-architecture.md
versie: v1.0
status: Active
strategic_owner: rol CTO (Claude Code)
technical_owner: rol Chief AI Officer (Claude Code)
reviewer: Architecture-Guardian
documentation_owner: Documentation-Manager
review_frequentie: maandelijks
laatste_review: 2026-07-04
---

# Context Architecture

Hoe context per agent-run wordt samengesteld, begrensd en betaald. (P2-actie uit de Full Governance Review 2026-07-03; werd al gerefereerd door 4.3/6.2.)

## Contextlagen per run (van goedkoop naar duur)

| Laag | Bron | Wanneer geladen |
|---|---|---|
| 1. Agentdefinitie | `.claude/agents/<naam>.md` | altijd (harness) |
| 2. Taakprompt | opdrachtgever (gebruiker of Master-Stratejist) | altijd; volgt prompt-template |
| 3. Memory-verwijzingen | memory-namen in de prompt | alleen genoemde items |
| 4. Blueprint-secties | `blueprint/…` | alleen bij governance-taken; verwijzen boven laden |
| 5. Rapportdata | `lees_pdf.py` op `raporlar/` | duurste laag; scoped per agent, `--recent` eerst |
| 6. Screenshots | `portföyüm/` via Read | alleen Master-Stratejist/Risk-Yoneticisi |

## Regels

1. **Elke prompt declareert zijn context** als verplicht / optioneel / verboden (CONTEXT RULES-sectie); niet-gedeclareerde context wordt niet geladen.
2. **Passports en boeken zijn ontwerpdata, geen runtime-context.** Agents laden hun eigen passport niet; de agentdefinitie is de runtime-waarheid (bewuste keuze, zie token review fase 6, 2026-07-03).
3. **Laag 5 is gebudgetteerd** per IC-fase (Book III §08); overschrijding alleen met motivering in de output.
4. **Samenvatting vóór diepte:** eerst inventariseren (`--recent`, bestandsnamen), dan gericht lezen; nooit dezelfde bron twee keer in één run.
5. **Contextoverdracht tussen agents** loopt via gestructureerde output (vaste kopjes), nooit via "lees alles wat ik las" — de ontvanger krijgt conclusies + bronverwijzingen, geen ruwe data.
6. **Versheid is onderdeel van context:** elke rapportgebaseerde bewering draagt rapportdatum; de ontvanger weegt de leeftijd (knowledge-architecture §Bronwaarheid).

## Bekende beperkingen

- Geen mechanische afdwinging van tokenbudgetten per agent (harness meet niet per subagent-run); bewaking is procesmatig via Token-Optimizer-reviews en `reports/tokens/`.
- CLAUDE.md wordt in elke hoofdsessie volledig geladen (harness-gedrag); compact houden is daarom een blijvende eis.
