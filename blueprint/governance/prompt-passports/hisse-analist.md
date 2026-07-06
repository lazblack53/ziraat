# Prompt Passport — Hisse-Analist

```yaml
id: PP-003
name: Hisse-Analist agentprompt
version: v2.0
status: Active
owner: rol Equity-specialist
reviewer: rol Architecture Guardian
domain: BIST-fundamentals / sectorrotatie
used_by_agents:
  - Hisse-Analist
purpose: Fundamenteel koopwaardige aandelen en sectorvoorkeuren identificeren binnen het macro-regime
success_criteria:
  - Elke pick met concreet cijfer + bron en relatieve waardering
  - Coverage-status per pick vermeld (ZFG-universum dekt niet alle tickers)
input_requirements:
  - Marktregime van Macro-Stratejist (via Master-Stratejist)
required_context:
  - Mapscope: ZFG 1/4/5/6/8/9/11, İş 3/7/8
optional_context:
  - Toplantı notları, yabancı oranları als verdieping
forbidden_context:
  - Technische niveaus als koopargument; macro-regimebepaling
output_format: 3 secties (Sectorvoorkeuren, Top picks gerangschikt, Coverage-melding)
constraints:
  - Fundamentals-only; teknik bülten-rotatie is geen signaal
decision_rules:
  - Sectorrotatie vóór stock selection (Priority 4, DR-002)
token_rules:
  max_context_tokens: ≤ 8 rapporten per run, gericht op kandidaten (Book III §08)
  max_output_tokens: compact; alleen relevante cijfers
  compression_required: true
  avoid_repetition: true
quality_checks:
  - Cijfer+bron per pick; relatieve waardering; coverage-check; consistentie met macro-regime
risk_level: middel
review_frequency: biweekly
last_review: 2026-07-03
change_log:
  - version: v2.0
    date: 2026-07-03
    change: Migratie naar 10-sectiestandaard; coverage-meldplicht toegevoegd
    reason: DR-005/DR-006; agent-evolution-agenda (GMSTR/ALTIN-les)
```
