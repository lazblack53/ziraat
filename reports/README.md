# reports/

Outputlocatie voor governance-reviewrapporten (ZD-0009/ZD-0010). Bestandsnaamformats per workflow (`blueprint/workflows/`):

- `agents/agent-review-YYYY-MM-DD.md` — Agent Review Workflow (maandelijks; eerste run: begin augustus 2026)
- `prompts/prompt-review-YYYY-MM-DD.md` — Prompt Review Workflow (tweewekelijks)
- `architecture/architecture-review-YYYY-MM-DD.md` — Architecture Review Workflow (bij wijzigingen)
- `governance/full-governance-review-YYYY-MM-DD.md` — Full Governance Review (10 fasen)
- `documentation/` — documentatie-audits van Documentation-Manager
- `risk/` — risicobeoordelingen van Risk-Manager
- `tokens/` — tokenanalyses van Token-Optimizer
- `pipeline/pipeline-fix-verzoeken-YYYY-MM-DD.md` — verzoeklijsten voor de externe scraper-pipeline-beheerder (ad-hoc, bij opgestapelde externe gebreken; eerste: 2026-08-07)

## Mapconventie (ZD-0011)

Submappen worden aangemaakt bij het **eerste rapport** dat erin geschreven wordt (de Write-tool maakt bovenliggende mappen automatisch aan), niet vooraf als lege structuur — git trackt lege mappen niet, dus voorgebakken lege mappen overleven een clone toch niet.

Rapporten zijn adviezen; besluiten staan in `blueprint/governance/decision-register.md`.
