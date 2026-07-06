---
document: workflows/architecture-review-workflow.md
versie: v1.0
status: Active
strategic_owner: rol CTO (Claude Code)
reviewer: Architecture-Guardian
documentation_owner: Documentation-Manager
review_frequentie: maandelijks
laatste_review: 2026-07-03
brondocument: "../../6.3.Ziraat Architecture Review Workflow v1.0.pdf"
---

# Architecture Review Workflow

Hoe architectuurwijzigingen worden beoordeeld vóór uitvoering — tegen groei door losse lokale oplossingen (technische schuld, tokenkosten, agent-overlap, securityrisico, slechtere schaalbaarheid). Verplicht bij: wijziging mappenstructuur · nieuwe domeinen · nieuwe agents met platformimpact · nieuwe workflows · nieuwe memory-/contextlaag · nieuwe integraties · wijzigingen aan data- of securitystructuur · kosten-/tokenimpact · wijzigingen die meer dan één domein raken. Vastgelegd via ZD-0009.

**Betrokken agents.** Primair: Architecture-Guardian, rol CTO. Secundair: Agent-Reviewer, Prompt-Architect, Token-Optimizer, Documentation-Manager, Risk-Manager. Optioneel: gebruiker (CEO) bij strategische impact; CISO-/CFO-/COO-rollen per rolmapping.

**Input.** Minimaal: constitution.md, decision-register.md, agent-template.md, prompt-template.md. Afhankelijk van wijziging: book-02/03/04, `.claude/agents/`, `blueprint/workflows/`, `reports/`.

## Reviewvolgorde

| Stap | Wie | Wat | Outputsectie |
|---|---|---|---|
| 1. Change Intake | indiener | Verplicht Change Proposal: Titel · Probleem · Voorgestelde wijziging · Waarom nu? · Geraakte domeinen · Geraakte bestanden · Verwachte voordelen · Verwachte risico's · Rollback-plan. **Zonder deze velden gaat het voorstel niet door.** | Change Proposal |
| 2. Constitution Check | Architecture-Guardian | Toets tegen alle 10 hoogste principes (tabel per principe) | Constitution Check |
| 3. Domain Impact | Architecture-Guardian | Welke domeinen geraakt (Governance/Architecture/AI/Prompting/Knowledge/Operations/Finance/Investment/Security/Documentation/Evolution); eigenaar + review nodig? | Domain Impact (tabel) |
| 4. Agent Impact | Agent-Reviewer | Geraakte agents, veranderende verantwoordelijkheden, nieuwe overlap, template-updates, nieuwe agents nodig? | Agent Impact (tabel) |
| 5. Prompt Impact | Prompt-Architect | Geraakte prompts, contextregels, outputformats, stopcondities, duplicatie, tokenimpact | Prompt Impact (tabel) |
| 6. Token Impact | Token-Optimizer | Extra context-/outputkosten, besparing, caching, samenvattingen, workflowvolgorde, kosten bij schaal; zonder cijfers: Low/Medium/High/Unknown | Token Impact (tabel huidig/nieuw/verschil) |
| 7. Risk Review | Risk-Manager | Technisch, operationeel, security, compliance, financieel, AI-kwaliteit, business, rollback-risico | Risk Review (tabel met eigenaar) |
| 8. Documentation Review | Documentation-Manager | Bij te werken documenten, Decision Record/changelog/glossary nodig, conflicterende documentatie | Documentation Impact (tabel) |
| 9. Decision Record | indiener/Guardian | Verplicht bij: architectuurverandering, agents toevoegen/verwijderen/mergen/splitsen, workflowwijziging, security, significante kosten/tokens, meerdere domeinen, businessstrategie → `governance/decision-register.md` | Decision Record-status |
| 10. Final Review | Architecture-Guardian | Definitief GO / REVISE / NO-GO | Advies |

## Beslisregels

- **GO** — alles waar: past in Constitution · probleem duidelijk · businesswaarde duidelijk · risico beheersbaar · tokenimpact acceptabel · documentatie-impact bekend · rollback-plan bestaat · ZD-record aangemaakt indien nodig.
- **REVISE** — potentie, maar context/risicobeoordeling/rollback/tokenimpact/documentatie-impact ontbreekt of scope te breed.
- **NO-GO** — schendt Constitution · complexiteit zonder waarde · High/Critical-risico zonder mitigatie · rollback onmogelijk · securityimpact onacceptabel · tokenkosten zonder businesswaarde · verzwakt bestaande architectuur.

## Rapport

Vast format `# Architecture Review Report` met 13 secties: Samenvatting · Change Proposal · Constitution Check · Domain Impact · Agent Impact · Prompt Impact · Token Impact · Risk Review · Documentation Impact · Decision Record (nodig ja/nee + status) · Ontbrekende context · Advies · Concrete vervolgstappen.

**Opslag:** `reports/architecture/architecture-review-YYYY-MM-DD.md`. Goedgekeurde wijzigingen → change-log; wanneer relevant → decision-register.

## Stopcondities

Stop wanneer: Change Proposal ontbreekt · Constitution ontbreekt · rollback-plan ontbreekt bij High impact · securityimpact onbekend · meerdere domeinen zonder Decision Record · tokenimpact onbekend bij schaalgevoelige wijziging · bestaande documentatie conflicteert · verantwoordelijke eigenaar ontbreekt.

## Tokenregels

Analyseer eerst het proposal, niet de volledige codebase · laad alleen geraakte domeinen · samenvattingen voor grote documenten · max 10 belangrijkste risico's · geen volledige Blueprint-secties kopiëren · tabellen voor impactanalyse.
