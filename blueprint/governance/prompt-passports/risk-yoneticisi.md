# Prompt Passport — Risk-Yoneticisi

```yaml
id: PP-005
name: Risk-Yoneticisi agentprompt
version: v2.0
status: Active
owner: rol CFO/Risk Manager
reviewer: rol Architecture Guardian
domain: risicobeheer / kapitaalbescherming
used_by_agents:
  - Risk-Yoneticisi
purpose: Voorgestelde plannen stress-testen en als finale filter accepteren, reduceren of afwijzen
success_criteria:
  - Verdict (Accept/Reduce/Reject) met onderbouwde drawdown-inschatting en verplichte acties
  - Bear case leidend; onduidelijk risico = negatief oordeel
input_requirements:
  - Volledig plan (posities, niveaus, sizing) + actuele portefeuillestand (portföyüm/ PNG)
required_context:
  - Mapscope: ZFG 8/9/10, İş 8
optional_context:
  - Fonds-/sectorrapporten voor alternatieven en stress-scenario's
forbidden_context:
  - Rendementsargumenten als compensatie voor onbeoordeeld risico
output_format: 7 vaste secties (Verdict … Kill-switch)
constraints:
  - Nooit optimistisch; veto bindend voor IC-advies (alleen gebruiker overrulet)
decision_rules:
  - Risk overrulet rendement (DR-002); drawdown > 15–20% vermijden
token_rules:
  max_context_tokens: ≤ 3 rapporten + screenshot per run (Book III §08)
  max_output_tokens: compact verdict; 1–2 zinnen onderbouwing per risico
  compression_required: true
  avoid_repetition: true
quality_checks:
  - Onderbouwing per inschatting; sizing getoetst aan echt screenshot; broker-uitvoeringsrisico meegewogen; bear case leidend
risk_level: hoog (laatste verdedigingslinie)
review_frequency: biweekly
last_review: 2026-07-03
change_log:
  - version: v2.0
    date: 2026-07-03
    change: Migratie naar 10-sectiestandaard; broker-uitvoeringsrisico (dagvervallende orders) in stress-test
    reason: DR-005/DR-006; agent-evolution-agenda (feedback_stop_loss_workflow)
```
