---
document: book-03-operations/06-agent-management-process.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Agent Management Process

Lifecycle van agents in `.claude/agents/`.

## Aanmaken

1. Decision Record (Proposed) met: welk gat de agent vult, waarom geen bestaande agent volstaat, mapscope, tokenimpact.
2. Bouwen volgens [agent-template](../governance/agent-template.md); blueprint-metadatablok invullen.
3. Review: Architecture Guardian (+ Risk-Yoneticisi bij risicorol).
4. Decision Record → Approved; change-log-regel; testrun op een historische casus (bijv. een afgesloten IC-datum) vóór productiegebruik.

## Wijzigen

- **Cosmetisch** (typo's, padcorrectie, mapnaam): direct, change-log-regel.
- **Gedrag** (rol, werkwijze, outputformat, scope-uitbreiding): Decision Record + review; oude versie in het metadatablok bumpen zodat een rollback triviaal is (git ontbreekt — het metadatablok is de enige versiehistorie).

## Verwijderen / deactiveren

Decision Record (status Deprecated); bestand verplaatsen naar `.claude/agents/_deprecated/` in plaats van deleten, zodat prompthistorie behouden blijft.

## Maandelijkse agent-review (per Meta §10)

De volledige uitvoering volgt de [Agent Review Workflow](../workflows/agent-review-workflow.md) (ZD-0009): 9 stappen over Agent-Reviewer, Token-Optimizer, Prompt-Architect, Risk-Manager en Architecture-Guardian; rapport naar `reports/agents/`. De kernvragen per agent blijven:
1. Kloppen mapverwijzingen nog met `raporlar/`-realiteit?
2. Zijn de Constitution-investeringsprincipes en Ziraat-concretisering nog onverkort aanwezig/onweersproken?
3. Bevat de prompt inmiddels achterhaalde aannames (check tegen recente feedback-memories)?
4. Outputformat nog consolideerbaar door Master-Stratejist?
5. Tokenscope nog passend (geen sluipende map-uitbreiding)?

Bevindingen: kleine fixes direct, gedragspunten via Decision Record.

## Stap 5 uit de Meta-Architecture

De systematische aanpassing van de vijf bestaande agents aan deze Blueprint is een apart traject: per agent één review-pass volgens bovenstaande checklist, elk met eigen Decision Record. Nog niet uitgevoerd; gepland als eerstvolgende Blueprint-activiteit na goedkeuring van v1.0 door de gebruiker.
