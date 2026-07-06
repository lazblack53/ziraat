---
document: governance/prompt-template.md
versie: v2.0
status: Active
strategic_owner: Claude Code (rol: Prompt Architect / Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
reviewer: Claude Code (rol: Chief AI Officer)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: tweewekelijks
laatste_review: 2026-07-03
brondocument: "../../2.Ziraat Prompt Template v1.0.pdf (identiek aan 3.4.Ziraat Prompt Template v1.0.pdf, geverifieerd via diff 2026-07-03)"
---

# Ziraat Prompt Template

Normatieve standaard voor alle prompts (agentdefinities én taakprompten). v2.0 vervangt de eerdere minimale template en implementeert `2.Ziraat Prompt Template v1.0.pdf` integraal (DR-005). Een prompt zonder doel, grenzen en outputformat is ongeldig.

## 1. Verplichte structuur (10 secties, exact deze koppen en volgorde)

```
# ROLE            wie de agent is
# MISSION         waarom de agent bestaat (doel)
# TASK            exact wat er moet gebeuren
# INPUT           welke input/bronnen, met exacte paden of scope
# CONTEXT RULES   verplichte / optionele / verboden context
# OUTPUT FORMAT   exacte outputstructuur
# CONSTRAINTS     grenzen, regels, verboden gedrag
# QUALITY CHECKS  waarop de agent eigen output controleert
# TOKEN RULES     hoe tokengebruik beperkt wordt
# STOP CONDITIONS wanneer stoppen of escaleren
```

## 2. Prompt Passport

Iedere belangrijke prompt (alle agentdefinities; herbruikbare taakprompten) krijgt een passport in `governance/prompt-passports/<naam>.md` met velden: id, name, version, status, owner, reviewer, domain, used_by_agents, purpose, success_criteria, input_requirements, required/optional/forbidden_context, output_format, constraints, decision_rules, token_rules (max_context_tokens, max_output_tokens, compression_required, avoid_repetition), quality_checks, risk_level, review_frequency, last_review, change_log.

## 3. Tokenregels (verplicht in elke prompt)

- Geen lange context waar een samenvatting volstaat; verwijs naar documenten i.p.v. inhoud te kopiëren.
- Herhaal geen Blueprint-informatie; geen brede opdrachten zonder scope.
- Compacte outputformats; details alleen op noodzaak; grote taken in fases; eerst inventariseren, dan diep analyseren; geen lange redeneringen in output; tabellen alleen met echte meerwaarde.
- Ziraat-specifiek: `--recent N` vóór `--lijst`; scoped mappen; één keer lezen; budgetten per IC-fase in `book-03-operations/08-token-management-process.md`.

## 4. Patronen

**Verboden (te breed):** "doe/bekijk alles", "optimaliseer waar nodig", "maak het beter", "gebruik je beste oordeel", "neem alles mee", "wees volledig", "schrijf uitgebreid".

**Goed (begrensd):** "analyseer alleen …", "rapporteer maximaal N punten", "wijzig niets zonder eerst een plan te tonen", "maximaal N woorden", "geef per wijziging reden/impact/risico", "markeer ontbrekende context expliciet".

## 5. Standaard-outputformats

Algemeen: `## Samenvatting / ## Bevindingen / ## Risico's / ## Aanbevolen wijzigingen / ## Tokenimpact / ## Volgende stap`.
Review: tabel `| Onderdeel | Probleem | Impact | Prioriteit | Aanbevolen actie |`.
Besluit: `## Context / ## Opties / ## Aanbeveling / ## Risico / ## Kostenimpact / ## Besluit nodig`.

## 6. Stop Conditions (minimaal, altijd)

Stoppen of escaleren wanneer: verplichte context ontbreekt · risico hoger dan toegestaan · taak buiten scope · wijziging schendt de Constitution · tokenbudget overschreden · output zou speculatief worden · wijziging raakt meerdere domeinen zonder review · security-/investeringsrisico niet beoordeelbaar.

## 7. Reviewchecklist

Eén doel? · rol expliciet? · taak afgebakend? · inputvereisten duidelijk? · contextregels duidelijk? · outputformat vastgelegd? · beperkingen duidelijk? · quality checks aanwezig? · tokenregels aanwezig? · stopcondities aanwezig? · overlap met andere prompts gecontroleerd? · consistent met de [Constitution](constitution.md)?

## 8. Goedkeuringsregel

Een prompt is pas bruikbaar wanneer: één duidelijk doel · voldoet aan de 10-sectiestructuur · tokenregels opgenomen · outputformat expliciet · stopcondities aanwezig · overlap gecontroleerd · eigenaar en reviewer benoemd (passport) · versie vastgelegd. Wijzigingen: change-log-regel; gedragswijzigingen bovendien Decision Record (`book-04-evolution/03-prompt-evolution.md`).
