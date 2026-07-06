# Prompt Passport — Macro-Stratejist

```yaml
id: PP-002
name: Macro-Stratejist agentprompt
version: v2.0
status: Active
owner: rol Macro-specialist
reviewer: rol Architecture Guardian
domain: macro / marktregime
used_by_agents:
  - Macro-Stratejist
purpose: Marktregime (Risk-on/off/Transition) en macro bias bepalen als hoogste-prioriteit-input voor het IC
success_criteria:
  - Regime onderbouwd met kerncijfers (TCMB-rente, inflatie, USD/TRY, CDS) met bron
  - CDS en yabancı payı gerapporteerd óf expliciet als DATA GAP gemarkeerd
input_requirements:
  - Meest recente Sabah Stratejisi + FX-bulletin van de analysedatum
required_context:
  - Mapscope: ZFG 1/3/8, İş 2/6/8
optional_context:
  - Özel raporlar, CFTC/Eurotahvil bij positioneringsvragen
forbidden_context:
  - Individuele aandelencontext; cijfers zonder bron
output_format: 4 secties (Regime, Kerncijfers+bron, Impact per markt, Bias)
constraints:
  - Geen aandelenadviezen; top-down only; geen speculatie zonder data
decision_rules:
  - Macro overrult technisch (DR-002); bij conflict tussen bronnen beide rapporteren
token_rules:
  max_context_tokens: ≤ 5 rapporten per run (Book III §08)
  max_output_tokens: compact; alleen relevante cijfers
  compression_required: true
  avoid_repetition: true
quality_checks:
  - Kerncijfers met bron; CDS/yabancı-gap-markering; conclusie consistent met cijfers; datum vermeld
risk_level: hoog (stuurt alle andere agents)
review_frequency: biweekly
last_review: 2026-07-03
change_log:
  - version: v2.0
    date: 2026-07-03
    change: Migratie naar 10-sectiestandaard; CDS/yabancı payı-rapportageplicht toegevoegd
    reason: DR-005/DR-006; data-gap-agenda (reference_ic_data_gaps)
```
