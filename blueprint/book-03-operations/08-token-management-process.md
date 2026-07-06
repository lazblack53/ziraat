---
document: book-03-operations/08-token-management-process.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer, tevens Token Optimizer)
technical_owner: Claude Code (rol: CTO)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Token Management Process

Tokens zijn de grootste variabele kostenpost van Ziraat. Dit proces houdt het verbruik per IC-run beheersbaar.

## Leesregels (grootste hefboom)

1. **`--recent N` vóór `--lijst`.** `--lijst` dumpt ±750 paden; alleen gebruiken als `--recent` niet volstaat.
2. **Scoped mappen.** Elke agent leest uitsluitend zijn toegewezen categorieën; `--recent` bij voorkeur op een submap (`--recent 5 "raporlar/2. Günlük Teknik Bülten/"`) i.p.v. de hele boom.
3. **Eén keer lezen.** Een rapport dat al in de sessie is geëxtraheerd wordt niet opnieuw gelezen; kerncijfers gaan naar de agent-output of memory.
4. **Image-based PDF's vroeg herkennen.** <500 tekens → stoppen, niet blijven proberen.
5. **Excel gericht lezen.** Fondsbestanden zijn groot; alleen de relevante sheet/kolommen citeren.

## Schrijfregels

6. Memory-items compact: feit + waarom + hoe toepassen; geen rapportteksten kopiëren, wel bestandspaden.
7. Prompts verwijzen naar memory-namen en Blueprint-documenten in plaats van inhoud te herhalen.
8. Blueprint-documenten blijven compact genoeg om efficiënt door AI gelezen te worden (Quality Standard §11); dubbele informatie is een defect.

## Budgetindicatie per IC-run

| Fase | Richtlijn |
|---|---|
| Macro-Stratejist | ≤ 5 rapporten (sabah + FX + evt. özel) |
| Hisse-Analist | ≤ 8 rapporten, gericht op kandidatenlijst |
| Teknik-Analist | ≤ 4 rapporten (alleen voor de picks) |
| Risk-Yoneticisi | ≤ 3 rapporten + portfolioscreenshot |

Overschrijding is toegestaan mits gemotiveerd in de output ("waarom extra bron nodig was").

## Bewaking

Maandelijks (samen met de agent-review): steekproef van één IC-run nalopen op onnodige reads; structurele lekken → voorstel in `book-04-evolution/` (token-optimization is daar een vast thema).
