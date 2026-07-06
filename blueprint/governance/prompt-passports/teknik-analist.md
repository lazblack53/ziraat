# Prompt Passport — Teknik-Analist

```yaml
id: PP-004
name: Teknik-Analist agentprompt
version: v2.0
status: Active
owner: rol Timing-specialist
reviewer: rol Architecture Guardian
domain: technische analyse / timing
used_by_agents:
  - Teknik-Analist
purpose: Entry/stop/target en invalidatie leveren voor door het IC aangedragen picks
success_criteria:
  - Elke setup: entry-zone, stop, 1–2 targets (Methode B), R:R ≥ 1:2, invalidatie, horizon
  - Sanity target1 > trigger bij long gehaald (DR-003-fout uitgesloten)
input_requirements:
  - Picks van Master-Stratejist/Hisse-Analist
required_context:
  - Mapscope: ZFG 2/7, İş 1/6; recentste bulletin dat de ticker dekt
optional_context:
  - FX-technisch rapport bij FX-vragen
forbidden_context:
  - Macro/fundamentals als argument; richting kiezen zonder aangeleverde picks
output_format: 6 vaste onderdelen per asset + coverage-melding
constraints:
  - Geen entry zonder stop; geen R:R < 1:2; twijfel → wait; Methode A verboden (DR-003)
decision_rules:
  - Priority 5, execution only; macro en fundamentals overrulen volledig (DR-002)
token_rules:
  max_context_tokens: ≤ 4 rapporten, alleen voor gevraagde picks (Book III §08)
  max_output_tokens: compact per asset, geen indicatoruitleg
  compression_required: true
  avoid_repetition: true
quality_checks:
  - target>trigger-sanity; bron per niveau; R:R herrekend; Methode B benoemd
risk_level: middel (niveaus sturen orders)
review_frequency: biweekly
last_review: 2026-07-03
change_log:
  - version: v2.0
    date: 2026-07-03
    change: Migratie naar 10-sectiestandaard; Methode B-plicht + target>trigger-sanity in prompt
    reason: DR-005/DR-006; DR-003 (Methode A-fout)
```
