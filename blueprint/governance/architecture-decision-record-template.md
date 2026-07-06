---
document: governance/architecture-decision-record-template.md
versie: v1.0
status: Active
strategic_owner: rol CTO
reviewer: Architecture-Guardian
documentation_owner: Documentation-Manager
review_frequentie: maandelijks
laatste_review: 2026-07-04
---

# Architecture Decision Record (ADR) Template

Sjabloon voor ZD-records met architectuurimpact. (Verplicht centraal document per Meta §6; P2-actie uit de Full Governance Review 2026-07-03.) ADR's zijn gewone ZD-records in `decision-register.md` — dit sjabloon vult het algemene ZD-veldenformat (decision-register §Template) aan met de architectuurspecifieke velden uit de Architecture Review Workflow.

## Gebruik

1. Doorloop eerst de [architecture-review-workflow](../workflows/architecture-review-workflow.md) (Change Proposal-intake is verplicht).
2. Leg het besluit vast als `ZD-xxxx` met alle standaardvelden, plus onderstaande architectuurvelden.
3. Rapport van de review → `reports/architecture/`; het ZD-record verwijst ernaar onder Links.

## Aanvullende architectuurvelden

```markdown
## ZD-xxxx — <titel>
<alle standaard ZD-velden, plus:>

- **Architectuurcontext:** huidige situatie (welke laag/component, huidig gedrag).
- **Gekozen architectuur:** wat verandert structureel (lagen, componenten, dataflow).
- **Constitution-check:** uitkomst per geraakt principe (of verwijzing naar reviewrapport).
- **Domain Impact:** geraakte domeinen + eigenaren (tabel uit workflow stap 3).
- **Consequenties:** wat wordt hierdoor makkelijker én moeilijker (beide verplicht).
- **Alternatieven-architectuur:** per verworpen alternatief de structurele reden.
- **Migratiepad:** hoe bestaande componenten overgaan (of "n.v.t. — additief").
- **Guardian-advies:** GO / REVISE / NO-GO + datum + rapportlink.
```

## Wanneer een ADR (i.p.v. een gewoon ZD-record)

Bij: wijziging mappenstructuur · nieuwe domeinen of lagen (memory/context/integraties) · wijziging data- of securitystructuur · wijzigingen die meerdere domeinen raken (scope architecture-review-workflow). Nieuwe agents of prompts zonder structuurimpact: gewoon ZD-record volstaat.
