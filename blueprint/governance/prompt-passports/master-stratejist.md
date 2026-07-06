# Prompt Passport — Master-Stratejist

```yaml
id: PP-001
name: Master-Stratejist agentprompt
version: v2.0
status: Active
owner: rol COO/orkestratie (gebruiker = eindbeslisser)
reviewer: rol Architecture Guardian
domain: investment-committee / orkestratie
used_by_agents:
  - Master-Stratejist
purpose: Specialistenoutput synthetiseren tot één risico-gecontroleerd IC-advies
success_criteria:
  - Eindadvies volgt Decision Engine-volgorde (DR-002) en lost conflicten expliciet op
  - Geen advies zonder afgelopen data-gap-checklist; bij open R:R-gaten GEEN ACTIE
  - Elk niveau/cijfer met bron (rapport + datum)
input_requirements:
  - Output van de vier specialisten (workflow stap 1–4)
  - Actuele portefeuillestand (portföyüm/ PNG)
required_context:
  - Recente rapporten betrokken domeinen
  - Memory: reference_ic_data_gaps, portfolio_beslissingen
optional_context:
  - Fondsdata (10. Fonlar) bij TP2-afwegingen
forbidden_context:
  - Cijfers zonder bron; verouderde rapporten als actueel
output_format: 8 vaste secties (Market Regime … Final Committee Decision incl. Data Gaps)
constraints:
  - Draft ≠ IC-besluit (Constitution, investeringsprincipes)
  - Geen orderuitvoering; broker-realiteit respecteren
decision_rules:
  - Macro > technisch; risk > rendement; fundamentals > momentum; twijfel → exposure omlaag/wachten
token_rules:
  max_context_tokens: consolidatie-only; specialisten lezen de rapporten
  max_output_tokens: compact eindadvies, geen lange redeneringen
  compression_required: true
  avoid_repetition: true
quality_checks:
  - Review-checklist Book III §A (bronplicht, Methode B-sanity, R:R herrekend, data-gaps, versheid)
risk_level: hoog (eindadvies raakt kapitaal)
review_frequency: biweekly
last_review: 2026-07-03
change_log:
  - version: v2.0
    date: 2026-07-03
    change: Migratie naar 10-sectiestandaard; Data Gaps-sectie en draft≠besluit-regel in prompt zelf
    reason: DR-005/DR-006; agent-evolution-agenda
```
