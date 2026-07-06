---
document: workflows/full-governance-review.md
versie: v1.0
status: Active
strategic_owner: Architecture-Guardian (agent)
reviewer: gebruiker (CEO-rol)
documentation_owner: Documentation-Manager
review_frequentie: maandelijks of bij grote wijzigingen
laatste_review: 2026-07-03
brondocument: "../../7.Ziraat Full Governance Review Workflow v1.0.pdf"
---

# Full Governance Review Workflow

Centrale reviewprocedure voor het hele platform: projectstructuur, Blueprint, governance, agents, prompts, workflows, documentatie, tokens, risico, businesswaarde en evolution readiness. **Hoogste regel: eerst begrijpen → dan beoordelen → dan prioriteren → dan pas wijzigen.** Geen structurele wijziging vóór minimaal de prioriteitenlijst (fase 10) is afgerond. Vastgelegd via ZD-0010.

**Verplicht bij:** eerste volledige analyse · grote wijzigingen aan `.claude/agents/` · nieuwe governance-structuur · nieuwe Blueprint-versie · grote promptwijzigingen · wijziging mappenstructuur · nieuwe businessdomeinen · nieuwe AI-workflows · maandelijkse governance-review.

**Padconventie (Ziraat):** de brondocumenten gebruiken paden zonder prefix (`governance/…`, `workflows/reviews/…`). In dit project geldt de mapping: `governance/` → `blueprint/governance/`, `workflows/reviews/` → `blueprint/workflows/`, `knowledge/` → `knowledge/` (projectroot), `reports/` → `reports/` (projectroot). Vastgelegd in [glossary](../governance/glossary.md).

**Betrokken agents.** Primair: Architecture-Guardian, Agent-Reviewer, Prompt-Architect, Token-Optimizer, Documentation-Manager, Risk-Manager. Secundair (rolmapping): gebruiker (CEO), hoofdsessierollen CTO/Chief AI Officer; CISO-rol onvervuld. Minimale bestanden: de zeven governance-documenten + de drie deelworkflows; ontbreekt er één, dan meldt de workflow dat en stelt eerst aanmaak voor.

## De 10 fases

| Fase | Naam | Wie (primair) | Kern |
|---|---|---|---|
| 0 | Safety & Scope Check | Architecture-Guardian | Bestaat de basis? Scope duidelijk? Toestemming? Alleen rapporteren of ook patches? Gevoelige data uitgesloten? Stop bij destructieve opdracht zonder toestemming. |
| 1 | Project Inventory | Documentation-Manager | Alleen structuur, bestandsnamen, README's — geen diepe inhoud; max 3 directoryniveaus; caches/`.git`/grote outputmappen overslaan. |
| 2 | Blueprint & Governance Review | Documentation-Manager | Completeness-check (constitution, register, templates, changelog, risk register, glossary, Meta), conflicten, eigenaarschap, versiebeheer. |
| 3 | Architecture Review | Architecture-Guardian | Volgt [architecture-review-workflow](architecture-review-workflow.md): structuur, domeinen, lagen, technische schuld, schaalbaarheid. |
| 4 | Agent Review | Agent-Reviewer | Volgt [agent-review-workflow](agent-review-workflow.md); max 10 agents per batch — bij meer: eerst inventariseren, groeperen per domein, Core → Supporting → Specialized. |
| 5 | Prompt Review | Prompt-Architect | Volgt [prompt-review-workflow](prompt-review-workflow.md): 10 secties, anti-patterns, duplicatie. |
| 6 | Token Review | Token-Optimizer | Grootste verspilling: lange prompts, dubbele instructies, brede contextloads, output zonder limiet, ontbrekende samenvattingen/caching. |
| 7 | Documentation Review | Documentation-Manager | Ontbrekend/dubbel/verouderd, eigenaar/versie/reviewdatum, changelog, register, glossary, Blueprint↔werkelijkheid. |
| 8 | Risk Review | Risk-Manager | Tien risicocategorieën; algemene rating Low–Critical; mitigaties; escalatie. |
| 9 | Business & Evolution Review | Architecture-Guardian + rol CEO | Businesswaarde, kostenbesparing, schaalbaarheid naar nieuwe domeinen, self-improvement/evolution readiness, KPI's, automatiseringskansen, risk/reward investeringsmodules. |
| 10 | Prioriteitenlijst & Implementatieplan | Architecture-Guardian | P0 kritiek · P1 hoge waarde/lage moeite · P2 belangrijk niet urgent · P3 later · P4 niet doen. Plus vereiste ZD's, documentatie-, agent- en promptwijzigingen, token- en businessimpact. |

Elke fase eindigt met een eigen outputsectie (tabelformats per bronworkflow) en een GO/REVISE/NO-GO-tussenadvies.

## Wijzigingsregels na de review

Wijzigingen alleen uitvoeren wanneer: prioriteit P0/P1 · risico Low/Medium · Architecture-Guardian minimaal GO of REVISE-met-voorwaarden · ZD-record aangemaakt indien verplicht · rollback-plan bij structurele wijzigingen · documentatie-impact bekend. High/Critical-wijzigingen vereisen extra review.

## Eindrapport

`# Full Governance Review — Final Report` met: Executive Summary · Overall Status (GO/REVISE/NO-GO) · Belangrijkste bevindingen · Grootste risico's · Grootste kansen · Quick Wins · Prioriteiten · Vereiste Decision Records · Vereiste documentatie-updates · Vereiste agentwijzigingen · Vereiste promptwijzigingen · Verwachte tokenimpact · Verwachte businessimpact · Concrete volgende stap.

**Opslag:** `reports/governance/full-governance-review-YYYY-MM-DD.md`. Goedgekeurde wijzigingen → change-log; structurele beslissingen → decision-register.

## Stopcondities

Stop of REVISE wanneer: governancebasis of Constitution ontbreekt · projectstructuur onleesbaar · scope te groot zonder batchplan · secrets/gevoelige data aangetroffen · destructieve opdracht zonder expliciete toestemming · security- of investeringsrisico niet beoordeelbaar · rollback-plan ontbreekt bij structurele wijziging.

## Tokenregels

Begin met inventarisatie; eerst bestandsnamen, dan inhoud · max 10 agents en 10 prompts per batch · max 15 hoofdbevindingen, max 10 quick wins · geen volledige bestanden kopiëren; samenvattingen en tabellen · stop en maak een batchplan wanneer de scope te groot wordt · optimaliseer voor beslissingen, niet voor volledigheid om de volledigheid.
