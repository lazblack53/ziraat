---
document: governance/change-log.md
versie: v1.0
status: Approved
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: continu
laatste_review: 2026-07-03
---

# Change Log

Elke wijziging aan een Blueprint-document krijgt hier één regel: datum, document, versie, wat + waarom. Grote beslissingen krijgen daarnaast een Decision Record.

| Datum | Document | Versie | Wijziging |
|---|---|---|---|
| 2026-07-03 | (alle) | v1.0 | Initiële aanmaak Minimum Viable Blueprint (17 documenten) conform Meta-Architecture §14–15; zie DR-001. |
| 2026-07-03 | governance/prompt-template.md | v2.0 | Volledig herschreven naar de normatieve standaard uit `2.Ziraat Prompt Template v1.0.pdf` (passport, 10 secties, tokenregels, stopcondities); DR-005. |
| 2026-07-03 | governance/agent-template.md | v1.1 | Verplichte promptsecties vervangen door de 10-sectiestructuur; passport-verplichting toegevoegd; DR-005. |
| 2026-07-03 | .claude/agents/*.md (5 stuks) | v2.0 | Migratie naar 10-sectiestandaard + QUALITY CHECKS/TOKEN RULES/STOP CONDITIONS; passports aangemaakt onder governance/prompt-passports/; DR-006. |
| 2026-07-03 | governance/constitution.md | v2.0 | Herschreven naar officiële `3.1.Ziraat Constitution v1.0.pdf` (10 hoogste principes, beslisregels, agent-/prompt-/architectuur-/business-/investeringsprincipes); Ziraat-concretisering en rolmapping behouden; ZD-0002. |
| 2026-07-03 | governance/decision-register.md | v2.0 | Herschreven naar officiële `3.2.Ziraat Decision Register v1.0.pdf`: ZD-nummering, volledig veldensjabloon, uitgebreide triggers; ZD-0001 opgenomen (DR-001 → Superseded); DR-002–006 als legacy behouden; ZD-0002. |
| 2026-07-03 | governance/agent-template.md | v2.0 | Herschreven naar officiële `3.3.Ziraat Agent Template v1.0.pdf`: Agent Passport verplicht, statussen/domeinen/tokenbudget/risiconiveaus/verboden gedrag; mapping 3.3-§14 ↔ 10-sectieformat; ZD-0002. |
| 2026-07-03 | governance/agent-passports/*.md (5 stuks) | v2.0 | Agent Passports AP-001–005 aangemaakt voor de vijf IC-agents (per 3.3: agent zonder passport is ongeldig); ZD-0002. |
| 2026-07-03 | governance/prompt-template.md | v2.0 | `3.4.Ziraat Prompt Template v1.0.pdf` geverifieerd: tekstueel identiek aan reeds geïmplementeerd document 2 (diff) — geen inhoudelijke wijziging, bronverwijzing aangevuld; ZD-0002. |
| 2026-07-03 | book-02/03/04 (5 documenten) | — | Verwijzingen naar oude Constitution-principenummering ("principe 5", "1–6") vervangen door verwijzing naar investeringsprincipes/Ziraat-concretisering (nummering gewijzigd door 3.1-adoptie). |
| 2026-07-03 | .claude/agents/Architecture-Guardian.md | v1.0 | Nieuwe governance-agent uit `4.1.Architecture Guardian.pdf` (GO/REVISE/NO-GO-wijzigingsreview); passport AP-006; ZD-0003. |
| 2026-07-03 | .claude/agents/Agent-Reviewer.md | v1.0 | Nieuwe governance-agent uit `4.2.Agent Reviewer.pdf` (agent-audit, scores, overlapmatrix); passport AP-007; ZD-0004. |
| 2026-07-03 | .claude/agents/Prompt-Architect.md | v1.0 | Nieuwe governance-agent uit `4.3.Prompt Architect Guide.pdf` (promptontwerp/-optimalisatie); passport AP-008; ZD-0005. |
| 2026-07-03 | governance/constitution.md | v2.1 | Rolmapping bijgewerkt: Architecture Guardian, Agent Reviewer en Prompt Architect zijn nu eigen agents; Token Optimizer/CISO expliciet als nog onvervulde rollen. |
| 2026-07-03 | book-02-architecture/03-ai-agent-architecture.md | v1.1 | Sectie "Twee agentlagen" toegevoegd: governance-laag naast het Investment Committee. |
| 2026-07-03 | .claude/agents/Token-Optimizer.md | v1.0 | Nieuwe governance-agent uit `5.1.Token Optimizer.pdf` (tokenreview, waste-patterns, gekwantificeerde besparing); passport AP-009; ZD-0006. |
| 2026-07-03 | .claude/agents/Documentation-Manager.md | v1.0 | Nieuwe governance-agent uit `5.2.Documentation Manager.pdf` (documentatie-audit, changelog-/registerconsistentie, glossary); passport AP-010; ZD-0007. |
| 2026-07-03 | .claude/agents/Risk-Manager.md | v1.0 | Nieuwe governance-agent uit `5.3.Risk Manager.pdf` (risicobeoordeling wijzigingen, 10 categorieën); passport AP-011; afbakening met Risk-Yoneticisi; ZD-0008. |
| 2026-07-03 | governance/risk-register.md | v1.0 | Risk register aangemaakt (verplicht centraal document Meta §6) met initiële risico's RR-001–009; beheer bij Risk-Manager; ZD-0008. |
| 2026-07-03 | governance/constitution.md | v2.2 | Rolmapping: Token Optimizer, Documentation Manager en Risk Manager nu eigen agents; alleen CTO/Chief AI Officer/CISO nog bij hoofdsessie. |
| 2026-07-03 | book-02-architecture/03-ai-agent-architecture.md | v1.2 | Governance-tabel uitgebreid naar zes agents; afbakening riskrollen toegevoegd. |
| 2026-07-03 | workflows/agent-review-workflow.md | v1.0 | Workflow aangemaakt uit `6.1.Ziraat Agent Review Workflow v1.0.pdf` (9 stappen, KEEP/IMPROVE/MERGE/SPLIT/DEPRECATE, 15-sectierapport); ZD-0009. |
| 2026-07-03 | workflows/prompt-review-workflow.md | v1.0 | Workflow aangemaakt uit `6.2.Ziraat Prompt Review Workflow v1.0.pdf` (9 stappen, incl. COMPRESS-besluit en testcriteria); ZD-0009. |
| 2026-07-03 | workflows/architecture-review-workflow.md | v1.0 | Workflow aangemaakt uit `6.3.Ziraat Architecture Review Workflow v1.0.pdf` (10 stappen, Change Proposal-intake verplicht); ZD-0009. |
| 2026-07-03 | reports/ (agents/prompts/architecture/tokens) | — | Outputlocaties voor reviewrapporten aangemaakt met README; ZD-0009. |
| 2026-07-03 | book-03 §02/§06, book-04 §03 | — | Verwijzingen naar de drie workflows toegevoegd als operationele uitwerking (geen inhoudelijke wijziging). |
| 2026-07-03 | workflows/full-governance-review.md | v1.0 | Master-reviewworkflow (10 fases) aangemaakt uit `7.Ziraat Full Governance Review Workflow v1.0.pdf`; padconventie gedocumenteerd; ZD-0010. |
| 2026-07-03 | governance/glossary.md | v1.0 | Glossary aangemaakt (verplicht bestand doc 8/Meta §6): governance-, pad-, tool- en beleggingsterminologie; ZD-0010. |
| 2026-07-03 | reports/ +3, knowledge/ +8 mappen | — | `reports/governance|documentation|risk/` en `knowledge/`-domeinstructuur (met README, zonder kennisduplicatie) aangemaakt per doc 8; ZD-0010. |
| 2026-07-03 | reports/governance/full-governance-review-2026-07-03.md | — | Eerste Full Governance Review uitgevoerd: Overall GO, geen P0, 11/11 agents KEEP; P1: IC-validatie RR-001, git-besluit, eerste agent-review-run; ZD-0010. |
| 2026-07-03 | governance/glossary.md | v1.1 | Toolconventie toegevoegd (bevinding AG-1 uit de review): abstracte passport-toolnamen → harness-tools; verboden handelingen expliciet. |
| 2026-07-04 | governance/workflow-template.md | v1.0 | Aangemaakt (verplicht Meta §6; P2 uit Full Governance Review): verplichte secties + kwaliteitseisen voor nieuwe workflows. |
| 2026-07-04 | governance/architecture-decision-record-template.md | v1.0 | Aangemaakt (verplicht Meta §6; P2): ADR = ZD-record + architectuurvelden; gekoppeld aan architecture-review-workflow. |
| 2026-07-04 | book-02-architecture/05-context-architecture.md | v1.0 | Aangemaakt (P2; werd gerefereerd door 4.3/6.2): contextlagen per run, declaratieplicht, budgettering, bekende beperkingen. |
| 2026-07-04 | book-01-foundation/09-success-metrics.md | v0.1 Proposed | KPI-voorstel K1–K7 met maandelijks rapportageformat; wacht op gebruikersgoedkeuring (Foundation-regel). |
| 2026-07-04 | governance/risk-register.md | v1.1 | **RR-001 gesloten**: 1e volledige IC-run onder v2.0-prompts (alle 5 agents) gedroeg zich conform besluitlijn én ving een Methode-A-recidive (RR-005-notitie); RR-010 toegevoegd (brondivergentie rapportprijzen vs bevestigde close). |
