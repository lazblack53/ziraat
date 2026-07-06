---
document: book-02-architecture/03-ai-agent-architecture.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
reviewer: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# AI Agent Architecture

## Agentbestand-standaard

Locatie `.claude/agents/*.md`; frontmatter `name/description/model/color/memory`; alle agents `model: sonnet`, `memory: project` (DR-004). Nieuwe agents: eerst Decision Record, dan [agent-template](../governance/agent-template.md).

## Twee agentlagen

Sinds ZD-0003–0005 kent Ziraat naast het Investment Committee een governance-laag:

| Agent | Domein | Taak | Trigger |
|---|---|---|---|
| Architecture-Guardian | Governance/Architecture | Wijzigingsreview (GO/REVISE/NO-GO) tegen Constitution/Blueprint | vóór elke structurele wijziging |
| Agent-Reviewer | AI/Agents | Periodieke agent-audit: scores, overlap, KEEP/IMPROVE/MERGE/SPLIT/DEPRECATE | maandelijks (Book III §06) |
| Prompt-Architect | AI/Prompting | Promptontwerp en -optimalisatie tegen de 10-sectiestandaard | tweewekelijks (Book IV §03) en op aanvraag |
| Token-Optimizer | AI/Cost Optimization | Tokenreview: waste-patterns, compressie- en cachingstrategieën, gekwantificeerde besparing | tweewekelijks (Book III §08) |
| Documentation-Manager | Documentation/Knowledge | Documentatie-audit: ontbrekend/verouderd/dubbel, changelog-/registerconsistentie, glossary | maandelijks (Meta §10) |
| Risk-Manager | Risk/Governance | Risicobeoordeling van wijzigingen/voorstellen (10 categorieën) + risk register | vóór elke High/Critical-beslissing; register maandelijks |

Governance-agents adviseren; besluiten lopen via Decision Records en de gebruiker. Zij geven nooit investeringsadvies. **Afbakening riskrollen:** Risk-Yoneticisi = inhoudelijke portefeuille-/trade-stress-test binnen de IC-workflow; Risk-Manager = platform-/proces-/wijzigingsrisico (ZD-0008).

## Het Investment Committee

| Agent | Rol | Prioriteit | Kernvraag |
|---|---|---|---|
| Master-Stratejist | Orkestrator / Head of IC | — | Wat is het ene, consistente advies? |
| Macro-Stratejist | Top-down regime | 1–2 (hoogste) | Risk-on of risk-off; TCMB, enflasyon, CDS, FX |
| Hisse-Analist | Bottom-up fundamentals | 4 | Welke BIST-aandelen, welke sectoren |
| Teknik-Analist | Timing | 5 (laagste) | Entry/stop/target — alleen Methode B (DR-003) |
| Risk-Yoneticisi | Eindfilter | veto | Overleeft het plan een stress-test? |

Rapportmap-toewijzing per agent staat in CLAUDE.md (tabel "Specialists") en in elke agentprompt zelf; niet hier gedupliceerd.

## Orkestratieworkflow (vaste volgorde)

1. Macro-Stratejist → marktregime
2. Hisse-Analist → fundamentele top-picks binnen dat regime
3. Teknik-Analist → niveaus voor die picks
4. Risk-Yoneticisi → stress-test, positiegrootte, veto
5. Master-Stratejist → consolidatie tot één advies; conflicten expliciet opgelost via het [Decision Framework](../book-01-foundation/08-decision-framework.md)

## Harde regels

- Een Master-Stratejist-draft is geen IC-besluit (Constitution, investeringsprincipes: draft ≠ besluit; memory `feedback_master_stratejist_draft_betrouwbaarheid`).
- Specialisten spreken elkaar niet direct aan; alle synthese loopt via Master-Stratejist.
- Geen agent voert orders uit; uitvoering is aan de gebruiker, binnen de broker-realiteit (dagvervallende orders, zincir, <1000 TRY vanaf 10:45).
- Ticker buiten ZFG-coverage (bijv. GMSTR, ALTIN): alleen technische of procentuele stops, en dat expliciet melden.

## Wijzigingen

Elke agentwijziging volgt `book-03-operations/06-agent-management-process.md`; gedragswijzigingen krijgen een Decision Record en change-log-regel.
