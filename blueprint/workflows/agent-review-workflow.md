---
document: workflows/agent-review-workflow.md
versie: v1.0
status: Active
strategic_owner: rol Chief AI Officer (Claude Code)
reviewer: Architecture-Guardian
documentation_owner: Documentation-Manager
review_frequentie: maandelijks
laatste_review: 2026-07-03
brondocument: "../../6.1.Ziraat Agent Review Workflow v1.0.pdf"
---

# Agent Review Workflow

Hoe agents worden beoordeeld, verbeterd, samengevoegd, gesplitst of uitgefaseerd. Verplicht bij: nieuwe agent · aanpassing bestaande agent · verwijderen/uitfaseren · merge · split · maandelijkse audit · grote wijzigingen in `.claude/agents/`. Vastgelegd via ZD-0009.

**Betrokken agents.** Primair: Agent-Reviewer, Architecture-Guardian. Secundair: Prompt-Architect, Token-Optimizer, Documentation-Manager, Risk-Manager. Optioneel (rolmapping constitution): gebruiker (CEO) bij strategische agents; CISO-rol bij securitygevoelige agents.

**Input.** Minimaal: constitution.md, agent-template.md, prompt-template.md, decision-register.md, `.claude/agents/`. Optioneel: book-02 §03, book-04 §02, `reports/agents/`, `reports/tokens/`.

## Reviewvolgorde

| Stap | Wie | Wat | Outputsectie |
|---|---|---|---|
| 1. Inventarisatie | Agent-Reviewer | Alleen bestandsnamen, namen, missie, verantwoordelijkheden, I/O, dependencies — nog niet diep lezen | Agent Inventory (tabel) |
| 2. Classificatie | Agent-Reviewer | Core / Supporting / Specialized / Experimental / Deprecated Candidate / Unknown | classificatiekolom |
| 3. Template Check | Agent-Reviewer | Verplichte passportvelden aanwezig? (agent-template §1) | Template Compliance (tabel) |
| 4. Scope Review | Agent-Reviewer | Missie duidelijk? Te breed? Grenzen expliciet? Buiten domein? Werk van een ander? Stopcondities? | Scope Review (tabel) |
| 5. Overlapanalyse | Agent-Reviewer | Paarsgewijs op missie, verantwoordelijkheden, I/O, context, tools, domein, beslisregels; niveau None–Critical | Overlap Matrix |
| 6. Token Review | Token-Optimizer | Promptlengte, herhaalde instructies, onnodige context, outputlengte, Blueprint-overlap, compressie | Token Review (tabel) |
| 7. Prompt Review | Prompt-Architect | Voldoet de prompt aan de 10 secties? | Prompt Review (tabel) |
| 8. Risk Review | Risk-Manager | Technisch, security, financieel, AI-hallucinatie, operationeel, investment indien relevant | Risk Review (tabel) |
| 9. Eindreview | Architecture-Guardian | Toets voorgestelde wijzigingen aan Constitution/Blueprint/standaarden/tokens/onderhoud/schaal/risico/businesswaarde | GO / REVISE / NO-GO |

## Beslisregels per agent

- **KEEP** — duidelijk, waardevol, geen sterke overlap, voldoet grotendeels aan template, risico beheersbaar.
- **IMPROVE** — nuttig, maar missie/prompt onduidelijk, templatevelden ontbreken, tokens te hoog of outputformat beter kan.
- **MERGE** — twee agents doen grotendeels hetzelfde (overlap High/Critical); verlaagt kosten/onderhoud. *Decision Record verplicht.*
- **SPLIT** — te veel verantwoordelijkheden, meerdere domeinen, te hoog risico of tokengebruik door brede scope. *Decision Record verplicht.*
- **DEPRECATE** — geen waarde, vervangen, onveilig/onbetrouwbaar, of structurele overlapveroorzaker. *Decision Record verplicht.*

## Rapport

Vast format `# Agent Review Report` met 15 secties: Samenvatting · Inventarisatie · Scores (duidelijkheid/scope/tokens/onderhoud/risico/gemiddelde/advies) · Template Compliance · Overlapmatrix · Belangrijkste problemen · Quick Wins · Te verbeteren · Samen te voegen · Te splitsen · Uit te faseren · Ontbrekende agents · Decision Records nodig · Prioriteitenlijst (met eigenaar) · Eindadvies GO/REVISE/NO-GO.

**Opslag:** `reports/agents/agent-review-YYYY-MM-DD.md`. Goedgekeurde wijzigingen → `blueprint/governance/change-log.md`; structurele wijzigingen → ZD-record.

## Stopcondities

Stop wanneer: Constitution of agent-template ontbreekt · `.claude/agents/` bestaat niet · agentbestanden onleesbaar · securitygevoelige agent aangepast zonder Risk-Manager/security-review · merge/split/deprecate zonder Decision Record · reviewscope te groot voor één run (faseer).

## Tokenregels

Start met inventarisatie, lees pas daarna diep · max 10 agents per reviewbatch · compact rapporteren · geen volledige agentprompts kopiëren tenzij noodzakelijk · max 15 belangrijkste bevindingen per rapport · tabellen voor vergelijking.
