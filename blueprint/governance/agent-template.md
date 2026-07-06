---
document: governance/agent-template.md
versie: v2.0
status: Active
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
reviewer: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
brondocument: "../../3.3.Ziraat Agent Template v1.0.pdf"
---

# Ziraat Agent Template

Standaardstructuur voor alle agents. Iedere agent wordt op dezelfde manier beschreven zodat verantwoordelijkheden, grenzen, contextgebruik, tokenbudget en kwaliteit meetbaar blijven. **Een agent zonder ingevuld Agent Passport is ongeldig.** v2.0 implementeert `3.3.Ziraat Agent Template v1.0.pdf` (ZD-0002).

## 1. Agent Passport

Per agent één passport in `governance/agent-passports/<naam>.md`, met velden:

```yaml
id: / name: / version: / status: / owner: / reviewer: / domain:
mission: / business_goal:
responsibilities: []          # specifiek, meetbaar, beperkt, niet overlappend, uitvoerbaar
not_responsible_for: []       # expliciet — voorkomt scope creep
inputs: [] / outputs: []
required_context: [] / optional_context: [] / forbidden_context: []
tools_allowed: [] / tools_forbidden: []
dependencies: {agents: [], documents: [], systems: []}
memory_rules: {read: [], write: [], never_store: []}
token_budget: {max_context_tokens:, max_output_tokens:, optimization_priority:}
quality_metrics: []
risk_level:                   # Low / Medium / High / Critical
security_level:
review_frequency: / last_review:
change_log: [{version:, date:, change:, reason:}]
```

Verplichte minimumvelden: id, name, version, status, owner, reviewer, domain, mission, responsibilities, not_responsible_for, inputs, outputs, required_context, token_budget, quality_metrics, risk_level, review_frequency.

## 2. Statussen en domeinen

Statussen: Draft (ontworpen, nog niet actief) · Active · Deprecated (uitfasering) · Archived · Under Review. Eén primair domein per agent (Ziraat nu: Investment; verder mogelijk: Governance, Architecture, AI, Prompting, Knowledge, Operations, Sales, CRM, Finance, Security, Documentation, Evolution).

## 3. Tokenbudget

Elke agent krijgt een budget (max_context_tokens, max_output_tokens, optimization_priority). Richtlijnen: strategische agents meer context; review-agents compact rapporteren; routine-agents zeer goedkoop; veel herhaling = sterk optimaliseren. Ziraat-concretisering per IC-fase: `book-03-operations/08-token-management-process.md`.

## 4. Risiconiveau

Low / Medium / High / Critical — hoe hoger, hoe strenger de review. Investeringsagents zijn per definitie High of Critical; Master-Stratejist en Risk-Yoneticisi (advies + veto raken kapitaal) zijn Critical.

## 5. Reviewregels

Herzien wanneer: taak verandert · overlap ontstaat · tokengebruik stijgt · outputkwaliteit daalt · de Blueprint wijzigt · het domein verandert · de reviewfrequentie is verstreken.

## 6. Verboden agentgedrag

Niet: buiten scope werken · ongecontroleerd nieuwe agents aanmaken · Constitution negeren · grote architectuurwijzigingen zonder Decision Record · prompts onnodig verlengen · kritieke kennis alleen in output laten zonder documentatie · business- of investeringsadvies zonder risicoanalyse · securityrisico's negeren · tokenkosten onbeperkt laten stijgen.

## 7. Agentprompt (bestandsformat `.claude/agents/`)

Harness-frontmatter blijft: `name/description/model/color/memory` (alle agents `model: sonnet`, `memory: project`, DR-004). De body volgt de 10-sectiestructuur van [prompt-template](prompt-template.md) §1; die dekt de minimale agentprompt uit 3.3 §14 volledig:

| 3.3 §14 | 10-sectieformat |
|---|---|
| Role / Mission | # ROLE / # MISSION |
| Responsibilities / Decision Rules | # TASK |
| Boundaries | # CONSTRAINTS |
| Required Context | # INPUT + # CONTEXT RULES |
| Output Format | # OUTPUT FORMAT |
| Quality Rules | # QUALITY CHECKS |
| Token Rules | # TOKEN RULES |
| Escalation Rules | # STOP CONDITIONS |

Onderaan het agentbestand: het blueprint-metadatablok met verwijzing naar agent-passport en prompt-passport.

## 8. Goedkeuringsregel

Een nieuwe of gewijzigde agent is pas geldig wanneer: template volledig ingevuld · verantwoordelijkheden duidelijk · grenzen expliciet · tokenbudget bepaald · overlap gecontroleerd · reviewfrequentie ingesteld · akkoord van rol Architecture Guardian · Decision Record aangemaakt wanneer nodig (zie [decision-register](decision-register.md) "Wanneer verplicht").
