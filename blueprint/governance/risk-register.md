---
document: governance/risk-register.md
versie: v1.0
status: Active
strategic_owner: gebruiker (CEO-rol)
technical_owner: Risk-Manager (agent)
documentation_owner: Documentation-Manager (agent)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Risk Register

Structurele risico's van het Ziraat-platform. Beheerd door Risk-Manager; elke wijziging via change-log. Niveaus: Low / Medium / High / Critical. (Verplicht centraal document per Meta-Architecture §6; aangemaakt bij ZD-0008.)

| ID | Risico | Categorie | Niveau | Mitigatie | Status | Bron/datum |
|---|---|---|---|---|---|---|
| RR-001 | Gedragsdrift agentprompts na v2.0-migratie (10-sectieformat) | AI Quality | Medium | **GESLOTEN 04.07:** volledige IC-run onder v2.0 uitgevoerd; besluit (GEEN ACTIE bij gaten/R:R-falen) consistent met besluitlijn 30.06–02.07; quality checks aantoonbaar toegepast (data-gap-markering, netto-R:R-herrekening, Methode-B-sanity); bonus: prompts vingen een bestaande fout (zie RR-005) | Gesloten | DR-006; ic_rapport_04072026 |
| RR-002 | Blueprint veroudert als reviewfrequenties niet worden gevolgd | Operational | Medium | Reviewfrequenties per Meta §10; Documentation-Manager maandelijkse audit | Open | ZD-0001, 2026-07-03 |
| RR-003 | Scraper-pipeline faalt stil ("0 pdfs" ≠ geen publicatie); evergreen links | Operational | Medium | Hash-check vóór "nieuw"; datagat expliciet melden in IC-run | Gemitigeerd (proces) | memory feedback_pipeline_scraper_gaps |
| RR-004 | Geen realtime koersdata; besluiten op rapport-EOD-data | Investment | High | GEEN ACTIE-default bij datagaten; 2e realtime-bron op data-gap-checklist | Open | memory reference_ic_data_gaps |
| RR-005 | Foutieve technische targets (historisch: Methode A, target1<trigger) | Investment | High | Methode B-plicht + target>trigger-sanitycheck in Teknik-Analist en review-checklist. **Recidive aangetroffen 04.07** in sessies 01–03.07 (TradingView resistance_20d/50d als target gebruikt): door v2.0-QUALITY CHECKS zelf gedetecteerd en gecorrigeerd; TUPRS/THYAO-targets 03.07 retroactief ingetrokken. Mitigatie bewezen werkend; alert blijven bij elke nieuwe databron | Gemitigeerd (bewezen 04.07) | DR-003; feedback_teknik_methode_recidive |
| RR-010 | Brondivergentie prijzen: İş-rapport toont GARAN 138,60 waar bevestigde close 136,10 is (−1,8%, 03.07); rapporten kunnen intraday/verouderde prijzen bevatten | Investment / AI Quality | Medium | Bevestigde candle-close (Teknik-bron) is leidend boven rapportprijzen; divergentie >1% expliciet melden in IC-advies; toegevoegd aan data-gap-checklist | Open | ic_rapport_04072026 |
| RR-006 | Order-gat door dagelijks vervallende broker-orders (close → herinvoer 10:45) | Investment | Medium | Verplicht meegewogen in Risk-Yoneticisi-verdict | Gemitigeerd (proces) | memory feedback_stop_loss_workflow |
| RR-007 | Overlap governance-agents onderling en met hoofdsessierollen (9 agents) | Operational | Medium | Eerste Agent-Reviewer-run met overlapmatrix; afbakening Risk-Manager/Risk-Yoneticisi in ZD-0008 | Open | ZD-0003–0008 |
| RR-008 | CISO-rol onvervuld; security-reviews vallen terug op gebruiker | Security | Medium | Escalatiepad naar gebruiker vastgelegd in agents; kandidaat voor volgende agent-batch | Open | 2026-07-03 |
| RR-009 | Tokenkosten stijgen met aantal agents en documentatielaag | Token Cost | Medium | Budgetten per passport; tweewekelijkse Token-Optimizer-review | Open | ZD-0006 |
