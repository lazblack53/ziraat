---
document: book-04-evolution/03-prompt-evolution.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer, tevens Prompt Reviewer)
technical_owner: Claude Code (rol: CTO)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: tweewekelijks
laatste_review: 2026-07-03
---

# Prompt Evolution

Verbetering van taakprompten en promptsecties, los van agent-gedragswijzigingen (daarvoor: [agent-evolution](02-agent-evolution.md)).

## Optimalisatiedoelen, in volgorde

1. **Correctheid** — de prompt kan niet tot Constitution-strijdige output leiden.
2. **Consolideerbaarheid** — output past mechanisch in het IC-format van Master-Stratejist.
3. **Tokenefficiëntie** — kleinere input-scope, verwijzingen i.p.v. herhaling.
4. **Herbruikbaarheid** — terugkerende taakprompten worden sjablonen conform [prompt-template](../governance/prompt-template.md).

## Werkwijze (before/after-plicht)

1. Bewaar de oude promptversie (in de change-log-regel of als citaat in het Decision Record).
2. Formuleer de wijziging als hypothese: "door X verwachten we Y minder fouten/tokens".
3. Draai de nieuwe prompt op een historische casus waarvan de juiste uitkomst bekend is (bijv. IC-datums 20-06 of 01-07, uitkomst GEEN ACTIE) en vergelijk.
4. Alleen bij aantoonbare verbetering doorvoeren; anders terug naar de oude versie (rollback is triviaal omdat de oude versie bewaard is).

## Tweewekelijkse promptronde (Meta §10: prompt-documentatie tweewekelijks)

De uitvoering volgt de [Prompt Review Workflow](../workflows/prompt-review-workflow.md) (ZD-0009): 9 stappen, primair Prompt-Architect + Token-Optimizer, eindadvies Architecture-Guardian; rapport naar `reports/prompts/`. Aanvullend op die workflow:

- Loop feedback-memories sinds de vorige ronde na op promptoorzaken.
- Controleer of de standaard `lees_pdf.py`-blokken in alle agents nog identiek en correct zijn.
- Controleer of nieuwe kennisvallen (knowledge-architecture) een promptregel verdienen.
- Leg de ronde vast met één change-log-regel, ook als er niets wijzigde ("geen bevindingen").

## Verboden

- Stilzwijgend prompts wijzigen zonder change-log-regel.
- Twee gedragswijzigingen in één prompt-iteratie (maakt effectmeting onmogelijk).
- Promptregels toevoegen die informatie uit de Blueprint dupliceren i.p.v. ernaar te verwijzen.
