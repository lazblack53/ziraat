---
document: governance/workflow-template.md
versie: v1.0
status: Active
strategic_owner: rol COO
reviewer: Architecture-Guardian
documentation_owner: Documentation-Manager
review_frequentie: maandelijks
laatste_review: 2026-07-04
---

# Workflow Template

Standaardstructuur voor elke nieuwe workflow onder `blueprint/workflows/`. (Verplicht centraal document per Meta §6; P2-actie uit de Full Governance Review 2026-07-03.) Een nieuwe workflow vereist een ZD-record ("nieuwe workflows" — registerregels).

## Verplichte secties (conform doc 8 §Required Review Workflows)

```markdown
---
document: workflows/<naam>.md
versie: / status: / strategic_owner: / reviewer: / documentation_owner:
review_frequentie: / laatste_review: / brondocument: (indien van toepassing)
---

# <Naam> Workflow

<Doel: één alinea — wat voorkomt of levert deze workflow; ZD-verwijzing.>

**Verplicht bij:** <scope: wanneer moet deze workflow draaien>

**Betrokken agents.** Primair: <wie voert uit>. Secundair: <wie levert deelstappen>. Optioneel: <rollen via constitution-rolmapping>.

**Input.** Minimaal: <bestanden>. Optioneel: <bestanden>.

## Stappenvolgorde
| Stap | Wie | Wat | Outputsectie |
|---|---|---|---|

## Beslisregels
<uitkomstcategorieën + wanneer welke geldt; welke uitkomsten een ZD-record vereisen>

## Rapport
<vast outputformat + opslaglocatie `reports/<map>/<naam>-YYYY-MM-DD.md`; changelog-/registerplicht>

## Stopcondities
<wanneer stoppen of REVISE>

## Tokenregels
<batchlimieten, max bevindingen, samenvattingsplicht>
```

## Kwaliteitseisen

Elke workflow heeft: één duidelijk doel · een eigenaar en reviewer · expliciete scope ("verplicht bij") · per stap één verantwoordelijke agent · een vast rapportformat met opslaglocatie · stopcondities · tokenregels. Workflows verwijzen naar elkaar in plaats van stappen te dupliceren (voorbeeld: full-governance-review verwijst naar de drie deelworkflows).
