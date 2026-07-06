---
document: governance/glossary.md
versie: v1.0
status: Active
strategic_owner: Documentation-Manager (agent)
reviewer: Architecture-Guardian
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Glossary

Consistente terminologie voor mensen en agents. Beheerd door Documentation-Manager. (Verplicht governance-document; aangemaakt bij ZD-0010.)

## Governance en structuur

| Term | Betekenis |
|---|---|
| Blueprint | Het besturingssysteem van Ziraat onder `blueprint/`: governance + vier boeken + workflows. Hoogste documentatielaag na de Constitution. |
| Constitution | Hoogste set ontwerpprincipes (`blueprint/governance/constitution.md`); wint bij elk conflict. |
| ZD-record | Decision Record in `blueprint/governance/decision-register.md` (ZD-xxxx; DR-002–006 zijn geldige legacy-ID's). |
| Agent Passport / Prompt Passport | Verplichte metadata per agent (`agent-passports/`, AP-xxx) en per belangrijke prompt (`prompt-passports/`, PP-xxx). Agent zonder passport is ongeldig. |
| 10-sectieformat | Verplichte promptstructuur: ROLE, MISSION, TASK, INPUT, CONTEXT RULES, OUTPUT FORMAT, CONSTRAINTS, QUALITY CHECKS, TOKEN RULES, STOP CONDITIONS. |
| Padconventie | Bronddocument-paden zonder prefix mappen zo: `governance/` → `blueprint/governance/` · `workflows/reviews/` → `blueprint/workflows/` · `reports/`, `knowledge/` → projectroot. |
| Toolconventie | Abstracte toolnamen in passports mappen op harness-tools: `file_read`/`file_search`/`grep`/`diff`/`markdown_lint`/`log_summary`/`static_analysis`/`risk_matrix` → Read, Grep, Glob en Bash; `production_deploy`, `financial_trade_execution` en `destructive_file_delete_without_approval` zijn categorisch verboden handelingen, geen tools. |
| IC | Investment Committee: Master-Stratejist + vier specialisten; besluit via de Decision Engine (DR-002). |
| Governance-laag | De zes reviewagents: Architecture-Guardian, Agent-Reviewer, Prompt-Architect, Token-Optimizer, Documentation-Manager, Risk-Manager. Adviseren alleen. |
| GEEN ACTIE | IC-default bij R:R-datagaten: kapitaal blijft in TP2. |
| GO / REVISE / NO-GO | Reviewuitkomsten governance-workflows. |
| KEEP / IMPROVE / MERGE / SPLIT / DEPRECATE (+ COMPRESS) | Besluitcategorieën agent-review (prompt-review kent ook COMPRESS). |
| P0–P4 | Prioriteitscategorieën: kritiek · hoge waarde/lage moeite · belangrijk niet urgent · later · niet doen. |

## Beleggingstermen (Turks → betekenis)

| Term | Betekenis |
|---|---|
| TP2 | Geldmarktfonds waarin niet-belegd kapitaal geparkeerd staat. |
| Methode A / Methode B | TradingView-targetmethoden; A (resistance-swing) is verboden (DR-003), alleen B toegestaan. |
| zincir order | Kettingorder bij de broker; vervalt dagelijks bij market close, handmatig herinvoeren; < 1000 TRY pas vanaf 10:45. |
| faiz / enflasyon (TÜFE) | Rente / inflatie (consumentenprijsindex). |
| yabancı oranları / yabancı payı | Buitenlandse posities / buitenlands aandeel in BIST. |
| CDS | Credit default swap-spread; risicoperceptie Turkije. |
| FAVÖK, F/K, PD/DD, FD/FAVÖK | EBITDA, P/E, P/B, EV/EBITDA. |
| 1Ç26 e.d. | Kwartaalaanduiding (1e kwartaal 2026) in rapportnamen. |

Nieuwe termen: toevoegen via Documentation-Manager met change-log-regel.
