---
document: workflows/prompt-review-workflow.md
versie: v1.0
status: Active
strategic_owner: Prompt-Architect (agent)
reviewer: rol Chief AI Officer (Claude Code)
documentation_owner: Documentation-Manager
review_frequentie: tweewekelijks
laatste_review: 2026-07-03
brondocument: "../../6.2.Ziraat Prompt Review Workflow v1.0.pdf"
---

# Prompt Review Workflow

Hoe prompts worden beoordeeld, verbeterd, verkort en gestandaardiseerd. Verplicht bij: nieuwe agentprompts · wijzigingen aan bestaande agentprompts · prompts met hoge tokenkosten, onvoorspelbare output, zonder outputformat of zonder stopcondities · prompts met financiële, klant-, security- of investeringsimpact. Vastgelegd via ZD-0009.

**Betrokken agents.** Primair: Prompt-Architect, Token-Optimizer. Secundair: Agent-Reviewer, Architecture-Guardian, Documentation-Manager, Risk-Manager. Optioneel: gebruiker/CISO-rol bij securitygevoelige prompts, CFO-rol bij hoge kostenimpact.

**Input.** Minimaal: constitution.md, prompt-template.md, agent-template.md. Afhankelijk van scope: `.claude/agents/`, `blueprint/workflows/`, book-02 §04, book-04 §03, `reports/tokens/`.

## Reviewvolgorde

| Stap | Wie | Wat | Outputsectie |
|---|---|---|---|
| 1. Prompt Inventory | Prompt-Architect | Alle relevante prompts in kaart (gebruikt door, doel, lengte) | Prompt Inventory (tabel) |
| 2. Purpose Check | Prompt-Architect | Eén doel? Rol expliciet? Taak concreet? Klaar- en stopcriterium duidelijk? | Purpose Check (tabel) |
| 3. Structure Check | Prompt-Architect | Alle 10 secties aanwezig (ROLE→STOP CONDITIONS)? | Structure Check (tabel) |
| 4. Context Review | Prompt-Architect | Verplicht/optioneel/verboden gedefinieerd? Te veel of dubbel geladen? Samenvatbaar? Verwijst i.p.v. kopieert? | Context Review (tabel) |
| 5. Output Review | Prompt-Architect | Format expliciet? Beslisbaar? Te lang? Tabellen juist ingezet? Lengte-/prioriteitslimiet? | Output Review (tabel) |
| 6. Token Review | Token-Optimizer | Lengte, herhaling, brede formuleringen, context-/outputduplicatie, compressie, verwachte besparing | Token Review (tabel) |
| 7. Risk Review | Risk-Manager | Extra streng bij: investeringen, klantcommunicatie, security, compliance, financiële/juridische analyse, productieacties, datawijzigingen | Risk Review (tabel) |
| 8. Rewrite | Prompt-Architect | Alleen herschrijven als doel, agentverantwoordelijkheid, risico, outputformat en tokenbudget duidelijk zijn; altijd in 10-sectieformat | Verbeterde prompts |
| 9. Eindreview | Architecture-Guardian | GO alleen bij: past in Constitution, duidelijke scope, outputformat, stopcondities, acceptabele tokenimpact, beoordeeld risico | GO / REVISE / NO-GO |

## Anti-patterns

Markeer: "doe alles", "analyseer volledig", "maak beter", "optimaliseer waar nodig", "neem alles mee", "gebruik alle bestanden", "gebruik je beste oordeel", "schrijf uitgebreid", "maak het professioneel", "denk breed". Vervang door: "analyseer maximaal X onderdelen", "rapporteer maximaal X bevindingen", "gebruik alleen relevante bestanden", "wijzig niets zonder review", "output in vast format", "stop wanneer verplichte context ontbreekt".

## Beslisregels per prompt

**KEEP** (duidelijk, compact, effectief) · **IMPROVE** (mist structuur, contextregels, outputformat of stopcondities) · **COMPRESS** (inhoudelijk goed, te lang of duplicatief) · **SPLIT** (meerdere taken) · **MERGE** (sterke overlap met andere prompt) · **DEPRECATE** (overbodig, vervangen of risicovol).

## Rapport en test

Vast format `# Prompt Review Report` met 12 secties: Samenvatting · Prompt Inventory · Structure Check · Contextproblemen · Outputproblemen · Tokenproblemen · Risico's · Verbeterde prompts · Verwachte tokenimpact · Testcriteria · Decision Records nodig · Eindadvies.

Testcriteria voor elke verbeterde prompt: consistente output · correcte begrenzing · lagere tokenkosten · minder herhaling · betere beslisbaarheid · correct stoppen bij ontbrekende context · geen scope creep · geen strijd met Constitution. (Ziraat-concretisering: valideer op een historische IC-casus, conform book-04 §03.)

**Opslag:** `reports/prompts/prompt-review-YYYY-MM-DD.md`. Wijzigingen → change-log; grote promptwijzigingen → ZD-record.

## Stopcondities

Stop wanneer: Constitution of prompt-template ontbreekt · doel van de prompt onbekend · gebruikende agent onbekend · security-/investeringsimpact zonder Risk-Manager · outputformat niet vaststelbaar · tokenbudget niet haalbaar · prompt buiten agentverantwoordelijkheid.

## Tokenregels

Eerst structuur, dan inhoud · geen volledige prompts herschrijven zonder noodzaak · max 10 promptproblemen per review · verwijzingen i.p.v. volledige context · compact rapport · tokenimpact per verbetering meten of schatten.
