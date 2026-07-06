---
document: governance/decision-register.md
versie: v2.0
status: Active
strategic_owner: Gebruiker
technical_owner: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: continu
laatste_review: 2026-07-03
brondocument: "../../3.2.Ziraat Decision Register v1.0.pdf"
---

# Decision Register

Bewaart alle belangrijke architectuur-, agent-, prompt-, business-, security- en operationele beslissingen, zodat altijd te achterhalen is: wat besloten is, waarom, welke alternatieven zijn overwogen, welke risico's bekend waren, welke impact verwacht werd en wanneer herbeoordeling volgt. v2.0 implementeert `3.2.Ziraat Decision Register v1.0.pdf` (ZD-0002).

## Wanneer verplicht

Bij: nieuwe agent · verwijderde agent · gewijzigde agentverantwoordelijkheden · nieuwe workflow · wijziging hoofdarchitectuur · nieuw businessdomein · grote promptwijzigingen · duidelijke tokenimpact · kostenimpact · security-impact · investerings- of risicogevolgen · wijzigingen die meerdere systeemlagen raken.

## Statussen

Proposed (ingediend, nog niet goedgekeurd) · Approved (goedgekeurd en actief) · Rejected (afgewezen) · Deprecated (wordt uitgefaseerd) · Superseded (vervangen door nieuwere beslissing) · Under Review (wordt herbeoordeeld).

## Template nieuwe records (ZD-xxxx)

Verplichte velden per record: Decision ID · Titel · Datum · Status · Eigenaar · Betrokken rollen · Context · Besluit · Waarom nu? · Alternatieven (minimaal twee, incl. niets doen) · Voordelen · Nadelen · Risico's · Impact op architectuur / agents / prompts / tokengebruik / kosten / onderhoud · Rollback-plan · Succescriteria · Reviewdatum · Links.

## Nummering

Nieuwe beslissingen: `ZD-xxxx` (vanaf ZD-0011). Records DR-002 t/m DR-006 (aangemaakt vóór deze standaard) behouden hun ID en geldigheid; hernummeren zou verwijzingen in agents, passports en boeken breken (Constitution: eenvoud boven complexiteit). DR-001 is Superseded door ZD-0001.

---

## ZD-0001 — Introduceer Ziraat Blueprint als centrale bron van waarheid

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Architecture Guardian
- **Betrokken rollen:** Gebruiker (CEO), Architecture Guardian, Chief AI Officer, Documentation Manager
- **Context:** Ziraat groeit richting een platform met meerdere agents, prompts, workflows en investeringslogica. Zonder centrale structuur: duplicatie, inconsistente beslissingen, stijgend tokengebruik, moeilijk onderhoud.
- **Besluit:** De Ziraat Blueprint is de centrale bron van waarheid voor architectuur, agents, prompts, workflows, governance, businessstrategie en evolution. Geïmplementeerd onder `blueprint/` (MVB, Meta §14–15).
- **Waarom nu:** De gebruiker leverde de Meta-Architecture aan; het agentsysteem draaide al zonder governance-laag.
- **Alternatieven:** (1) geen centrale Blueprint; (2) alleen losse README's; (3) alleen agentprompts als bron van waarheid — alle afgewezen wegens duplicatie- en driftrisico.
- **Voordelen:** consistentie, minder chaos, schaalbaarheid, overdraagbaarheid, controle over agents/prompts.
- **Nadelen:** meer documentatie, opstartkost, vergt discipline.
- **Risico's:** veroudering zonder onderhoud; agents die documenten negeren; te veel documentatie verhoogt tokenkosten.
- **Impact:** governance-laag boven bestaande structuur; agents raadplegen Blueprint bij structurele wijzigingen; prompts verwijzen naar Constitution/templates; tokens korte termijn licht omhoog, lange termijn omlaag; onderhoud eenvoudiger.
- **Rollback:** Blueprint deactiveren als governance-laag; documenten blijven als referentie.
- **Succescriteria:** nieuwe agents via agent-template · nieuwe prompts via prompt-template · grote beslissingen vastgelegd · minder agentoverlap · tokengebruik beter meetbaar.
- **Reviewdatum:** 2026-10-01 · **Links:** `Ziraat Blueprint Meta-Architecture v1.0.pdf`, `blueprint/README.md`. Vervangt DR-001.

## ZD-0002 — Adoptie officiële governance-set 3.1–3.4

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Architecture Guardian
- **Betrokken rollen:** Gebruiker (aanleverend/CEO), Architecture Guardian, Chief AI Officer, Documentation Manager
- **Context:** De gebruiker leverde de officiële versies van de vier Stap 1-governancedocumenten: `3.1 Constitution`, `3.2 Decision Register`, `3.3 Agent Template`, `3.4 Prompt Template`. De eerdere `governance/`-documenten waren eigen invullingen op basis van de Meta-Architecture.
- **Besluit:** De PDF's zijn normatief. `constitution.md` → v2.0 (PDF integraal + Ziraat-specifieke investeringsconcretisering + rolmapping), `decision-register.md` → v2.0 (dit document, ZD-nummering), `agent-template.md` → conform 3.3, `prompt-template.md` → gecontroleerd tegen 3.4.
- **Waarom nu:** Voorkomen dat eigen interpretaties en officiële standaard uiteenlopen (verboden duplicatie/conflict).
- **Alternatieven:** (1) niets doen (PDF's naast eigen versies) — afgewezen: direct conflict met Quality Standard; (2) PDF's letterlijk kopiëren zonder projectcontext — afgewezen: verliest bindende Ziraat-regels (Methode B, TP2-default, broker-realiteit).
- **Voordelen:** één standaard; officiële templates; projectregels behouden. **Nadelen:** migratie-inspanning; dubbele ID-reeks (DR/ZD) in register.
- **Risico's:** verwijzingen naar oude DR-nummers raken verweesd — gemitigeerd door legacy-records te behouden.
- **Impact:** governance-documenten geactualiseerd; agents/prompts onaangetast (10-sectieformat blijft geldig onder 3.4); tokens neutraal; onderhoud eenvoudiger.
- **Rollback:** vorige versies reconstrueerbaar uit sessie 2026-07-03 + change-log.
- **Succescriteria:** geen inhoudelijk conflict meer tussen `governance/` en de 3.x-PDF's; nieuwe records in ZD-format.
- **Reviewdatum:** 2026-10-01 · **Links:** de vier 3.x-PDF's in de projectroot; change-log 2026-07-03.

## ZD-0003 — Nieuwe agent: Architecture-Guardian

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol CTO; reviewer: gebruiker (CEO-rol)
- **Betrokken rollen:** Gebruiker (aanleverend), CTO, Chief AI Officer, Architecture Guardian
- **Context:** De Blueprint verwijst overal naar de rol Architecture Guardian, tot nu ingevuld door de Claude Code-hoofdsessie. Gebruiker leverde `4.1.Architecture Guardian.pdf` met compleet agent-ontwerp (passport + prompt).
- **Besluit:** Agent aangemaakt als `.claude/agents/Architecture-Guardian.md` (10-sectieformat, sonnet, project-memory per DR-004) met passport `governance/agent-passports/architecture-guardian.md`. Reviewt wijzigingen met GO/REVISE/NO-GO; outputformat uit de PDF.
- **Waarom nu:** Governance-reviews worden zo een gescheiden, onafhankelijke rol i.p.v. zelfbeoordeling door de hoofdsessie.
- **Alternatieven:** (1) niets doen (rol bij hoofdsessie laten) — afgewezen: reviewer en uitvoerder vallen dan samen; (2) alleen als procesdocument opnemen — afgewezen: PDF is expliciet een agent.
- **Risico's:** overlap met hoofdsessierol — gemitigeerd door rolmapping-update in constitution; tokenimpact laag (budget 8000/1800, alleen bij reviews).
- **Rollback:** bestand naar `.claude/agents/_deprecated/`, record op Deprecated.
- **Succescriteria:** architectuur-/agent-/promptwijzigingen krijgen aantoonbaar een Guardian-review vóór doorvoering.
- **Reviewdatum:** 2026-08-01 · **Links:** 4.1-PDF, AP-006.

## ZD-0004 — Nieuwe agent: Agent-Reviewer

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Chief AI Officer; reviewer: Architecture-Guardian
- **Context:** Gebruiker leverde `4.2.Agent Reviewer.pdf`. Maandelijkse agent-review (Book III §06) had nog geen uitvoerende agent.
- **Besluit:** Agent aangemaakt als `.claude/agents/Agent-Reviewer.md` + passport AP-007. Scoort agents 1–10 op acht dimensies; adviseert KEEP/IMPROVE/MERGE/SPLIT/DEPRECATE; MERGE/DEPRECATE-uitvoering vereist altijd ZD-record.
- **Waarom nu:** Agentbestand groeit (nu 8 agents); overlapbewaking wordt anders onhoudbaar.
- **Alternatieven:** (1) niets doen (checklist handmatig) — afgewezen: niet schaalbaar; (2) samenvoegen met Architecture-Guardian — afgewezen: PDF scheidt de rollen bewust (Guardian = wijzigingsreview, Reviewer = periodieke agent-audit).
- **Risico's:** advies-overlap met Guardian bij agentwijzigingen — afbakening: Reviewer audit + advies, Guardian besluit-review.
- **Rollback:** naar `_deprecated/`, record op Deprecated.
- **Succescriteria:** eerste Agent Review Report over alle 8 agents; overlapmatrix zonder onopgeloste High-overlaps.
- **Reviewdatum:** 2026-08-01 · **Links:** 4.2-PDF, AP-007.

## ZD-0005 — Nieuwe agent: Prompt-Architect

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Chief AI Officer; reviewer: Architecture-Guardian
- **Context:** Gebruiker leverde `4.3.Prompt Architect Guide.pdf` — ondanks de naam een compleet agent-ontwerp. De promptstandaard (DR-005) had nog geen uitvoerende rol voor ontwerp/optimalisatie.
- **Besluit:** Agent aangemaakt als `.claude/agents/Prompt-Architect.md` + passport AP-008. Ontwerpt/reviewt prompts tegen de 10-sectiestandaard; optimalisatiestrategie in 10 stappen; GO/REVISE/NO-GO-advies.
- **Waarom nu:** Tweewekelijkse promptronde (book-04 §03) krijgt hiermee een uitvoerende agent.
- **Alternatieven:** (1) niets doen — afgewezen: promptonderhoud bleef bij hoofdsessie; (2) samenvoegen met Agent-Reviewer — afgewezen: prompting is een eigen domein met eigen reviewfrequentie (biweekly vs monthly).
- **Risico's:** gedragsdrift bij promptherschrijvingen — gemitigeerd: herschrijvingen zijn voorstellen, doorvoeren vereist ZD + before/after-validatie.
- **Rollback:** naar `_deprecated/`, record op Deprecated.
- **Succescriteria:** promptreviews leveren aantoonbaar kortere of robuustere prompts met beschreven tokenimpact.
- **Reviewdatum:** 2026-08-01 · **Links:** 4.3-PDF, AP-008.

## ZD-0006 — Nieuwe agent: Token-Optimizer

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol CFO; reviewer: rol Chief AI Officer
- **Context:** Gebruiker leverde `5.1.Token Optimizer.pdf`; de rol stond sinds ZD-0003–0005 als onvervuld in de rolmapping en was dependency van drie governance-agents.
- **Besluit:** Agent aangemaakt als `.claude/agents/Token-Optimizer.md` + passport AP-009. Tweewekelijkse tokenreview (GO/REVISE/NO-GO); waste-patterndetectie; besparing altijd gekwantificeerd; nooit kwaliteit opofferen voor tokens.
- **Alternatieven:** (1) tokenbewaking in Book III §08-proces laten (handmatig) — afgewezen: geen eigenaar; (2) samenvoegen met Prompt-Architect — afgewezen: kosten-analyse is breder dan prompts (workflows, context, output).
- **Risico's:** over-optimalisatie ten koste van IC-bronplicht — gemitigeerd via stopconditie "context nodig voor veiligheid/nauwkeurigheid".
- **Rollback:** naar `_deprecated/`, record Deprecated. **Succescriteria:** eerste review met gekwantificeerde besparingsvoorstellen zonder kwaliteitsverlies.
- **Reviewdatum:** 2026-08-01 · **Links:** 5.1-PDF, AP-009.

## ZD-0007 — Nieuwe agent: Documentation-Manager

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol COO; reviewer: Architecture-Guardian
- **Context:** Gebruiker leverde `5.2.Documentation Manager.pdf`; documentatie-eigenaarschap lag bij de hoofdsessie; de Blueprint groeit (20+ documenten) en veroudering is een geregistreerd risico (RR-002).
- **Besluit:** Agent aangemaakt als `.claude/agents/Documentation-Manager.md` + passport AP-010. Maandelijkse documentatie-audit (ontbrekend/verouderd/dubbel), changelog-/register-consistentie, glossary-bewaking. Delete altijd als voorstel.
- **Alternatieven:** (1) hoofdsessie blijft documentation owner — afgewezen: geen onafhankelijke audit; (2) samenvoegen met Agent-Reviewer — afgewezen: ander domein en andere frequentie.
- **Risico's:** audit-rapporten zelf worden tokenlast — gemitigeerd: max 10 bevindingen, compact format.
- **Rollback:** naar `_deprecated/`, record Deprecated. **Succescriteria:** eerste audit identificeert de ontbrekende verplichte governance-documenten (glossary, workflow-template, ADR-template) met prioriteit.
- **Reviewdatum:** 2026-08-01 · **Links:** 5.2-PDF, AP-010.

## ZD-0008 — Nieuwe agent: Risk-Manager + aanmaak risk-register.md

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** gebruiker (CEO-rol); reviewer: Architecture-Guardian
- **Context:** Gebruiker leverde `5.3.Risk Manager.pdf`. Risicobeoordeling bestond alleen inhoudelijk-financieel (Risk-Yoneticisi, IC); platform-/proces-/AI-risico had geen eigenaar. Het risk register (verplicht centraal document, Meta §6) ontbrak.
- **Besluit:** Agent aangemaakt als `.claude/agents/Risk-Manager.md` + passport AP-011; `governance/risk-register.md` aangemaakt met negen initiële risico's (RR-001–009). **Afbakening:** Risk-Yoneticisi = inhoudelijke portefeuille-/trade-stress-test binnen de IC-workflow; Risk-Manager = risicobeoordeling van wijzigingen en voorstellen (technisch, operationeel, security, compliance, AI, token, business) plus procestoets op investeringsvoorstellen (downside beschreven? rollback? data?). Geen van beide neemt eindbeslissingen.
- **Alternatieven:** (1) Risk-Yoneticisi uitbreiden met platformrisico — afgewezen: schendt "één verantwoordelijkheid per agent" en vervuilt de IC-rol; (2) niets doen — afgewezen: wijzigingsrisico bleef onbeoordeeld.
- **Risico's:** rolverwarring met Risk-Yoneticisi — gemitigeerd via expliciete afbakening in beide passports en RR-007 (Agent-Reviewer bewaakt).
- **Rollback:** naar `_deprecated/`, record Deprecated; risk-register blijft (is los waardevol).
- **Succescriteria:** elke volgende ZD-beslissing met High/Critical-impact heeft een Risk-Manager-review vóór goedkeuring.
- **Reviewdatum:** 2026-08-01 · **Links:** 5.3-PDF, AP-011, governance/risk-register.md.

## ZD-0009 — Adoptie drie reviewworkflows (agent, prompt, architectuur) + reports/-structuur

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Chief AI Officer / rol CTO; reviewer: Architecture-Guardian
- **Betrokken rollen:** Gebruiker (aanleverend), Chief AI Officer, CTO, alle zes governance-agents
- **Context:** Gebruiker leverde `6.1/6.2/6.3` (Agent/Prompt/Architecture Review Workflow v1.0). De governance-agents bestonden (ZD-0003–0008) maar hun samenwerking per reviewtype was niet als proces vastgelegd; "nieuwe workflows" vereisen per registerregels een Decision Record.
- **Besluit:** Drie workflowdocumenten aangemaakt onder `blueprint/workflows/` (agent-review, prompt-review, architecture-review), inhoudelijk conform de PDF's: stappenvolgorde met verantwoordelijke agent per stap, beslisregels (KEEP/IMPROVE/MERGE/SPLIT/DEPRECATE; KEEP…DEPRECATE + COMPRESS voor prompts; GO/REVISE/NO-GO eindadvies), verplichte rapportformats, stopcondities en tokenregels. Outputlocaties aangemaakt: `reports/agents|prompts|architecture|tokens/`. Bestaande procesdocumenten (book-03 §02/§06, book-04 §03) verwijzen naar de workflows als operationele uitwerking.
- **Waarom nu:** Eerste geplande runs (agent-audit over 11 agents, RR-007-mitigatie) hebben een vastgelegd proces nodig vóór uitvoering.
- **Alternatieven:** (1) workflows in de book-03-documenten integreren — afgewezen: maakt die documenten lang en dupliceert de PDF-structuur; (2) niets doen (agents improviseren per run) — afgewezen: niet reproduceerbaar, geen vaste rapportformats.
- **Voordelen:** reproduceerbare reviews, vaste rapportlocaties, duidelijke rolverdeling per stap. **Nadelen:** meer documenten; workflowdiscipline vereist.
- **Risico's:** workflow-overhead bij kleine wijzigingen — mitigatie: scopebepalingen ("verplicht bij") begrenzen wanneer de volledige workflow nodig is.
- **Impact:** architectuur +1 documentlaag (`blueprint/workflows/`, was al voorzien in Meta/boekstructuur); agents ongewijzigd (workflows gebruiken bestaande agents); tokens: reviews zijn gebudgetteerd (max bevindingen, batchlimieten); onderhoud eenvoudiger.
- **Rollback:** workflowdocumenten markeren als Deprecated; agents blijven zelfstandig bruikbaar.
- **Succescriteria:** eerste agent-review-rapport in `reports/agents/` volgens het 15-sectieformat; architectuurwijzigingen gaan via Change Proposal-intake.
- **Reviewdatum:** 2026-08-01 · **Links:** 6.1/6.2/6.3-PDF's, `blueprint/workflows/`, `reports/README.md`.

## ZD-0010 — Full Governance Review Workflow + bootstrap-afronding + eerste review uitgevoerd

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** Architecture-Guardian (rol); reviewer: gebruiker (CEO-rol)
- **Betrokken rollen:** Gebruiker (aanleverend), alle zes governance-agents, hoofdsessierollen CTO/Chief AI Officer
- **Context:** Gebruiker leverde `7.Ziraat Full Governance Review Workflow v1.0.pdf` (centrale 10-fasenreview) en `8.Ziraat Governance Bootstrap Prompt v1.0.pdf` (opstartdraaiboek). Vrijwel de hele door doc 8 vereiste basis bestond al (ZD-0001–0009); ontbrekend waren glossary, de master-workflow, reports-submappen (governance/documentation/risk) en de knowledge/-structuur.
- **Besluit:** (1) `workflows/full-governance-review.md` aangemaakt conform doc 7, incl. padconventie-mapping; (2) `governance/glossary.md` aangemaakt (verplicht bestand doc 8/Meta §6) met pad- en toolconventie; (3) `reports/governance|documentation|risk/` en `knowledge/` (8 domeinmappen + README, zonder duplicatie van bestaande kennisbronnen) aangemaakt; (4) de eerste Full Governance Review uitgevoerd → `reports/governance/full-governance-review-2026-07-03.md`, Overall Status GO, geen P0-bevindingen, 11/11 agents KEEP.
- **Waarom nu:** Doc 8 schrijft expliciet voor te eindigen met een uitgevoerde review + eindrapport; de bootstrap is daarmee afgerond en het systeem operationeel.
- **Alternatieven:** (1) alleen documenten aanmaken zonder review te draaien — afgewezen: doc 8's slotinstructie vereist de review; (2) bestaande structuur verplaatsen naar de letterlijke doc 8-paden (root-`governance/` etc.) — afgewezen: churn zonder waarde, mapping gedocumenteerd in glossary.
- **Risico's:** review deels zelfbeoordeling (bouwer = reviewer) — gemitigeerd: bevindingen zijn concreet en falsifieerbaar (AG-1, ontbrekende templates, git-advies), en de P1-acties leggen externe validatie vast (IC-run, gebruikersbesluit git).
- **Impact:** documentatie +3 bestanden, +11 mappen; agents ongewijzigd; tokens neutraal; onderhoud beter (glossary + vaste reviewprocedure).
- **Rollback:** workflow/glossary markeren als Deprecated; rapport blijft als momentopname.
- **Succescriteria:** maandelijkse herhaling van de review; P1-acties (IC-validatie RR-001, git-besluit, eerste agent-review-run) binnen 30 dagen opgepakt.
- **Reviewdatum:** 2026-08-01 · **Links:** 7/8-PDF's, `blueprint/workflows/full-governance-review.md`, `reports/governance/full-governance-review-2026-07-03.md`.

---

## Legacy-records (vóór ZD-standaard; geldig tenzij anders vermeld)

## DR-001 — Adoptie Ziraat Blueprint Meta-Architecture v1.0

- **Status:** Superseded door ZD-0001 (inhoud daar opgenomen en uitgebreid).
- **Datum:** 2026-07-03 · **Eigenaar:** Gebruiker
- **Kern:** MVB (17 documenten) aangemaakt onder `blueprint/` conform Meta §14–15.

## DR-002 — Beslisvolgorde signalen (Decision Engine)

- **Datum:** 2026-07-03 (formalisering bestaande praktijk) · **Status:** Approved · **Eigenaar:** Master-Stratejist / Gebruiker
- **Besluit:** Prioriteit: macro-regime → liquiditeit (TCMB) → buitenlandse stromen → sectorrotatie → technische timing. Bij conflict: macro > technisch; risk > rendement.
- **Reviewdatum:** 2026-10-01

## DR-003 — Verbod TradingView Methode A voor targets

- **Datum:** 2026-07-03 (fout ontdekt juni 2026) · **Status:** Approved · **Eigenaar:** Teknik-Analist / Risk-Yoneticisi
- **Besluit:** Methode A (resistance-swing) structureel ongeldig (target1 < trigger). Alleen Methode B; elke target/trigger-set op consistentie gecontroleerd vóór IC-gebruik.
- **Reviewdatum:** 2026-10-01

## DR-004 — Agent-runtime: sonnet + project-scoped memory

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Chief AI Officer
- **Besluit:** Alle agents `model: sonnet`, `memory: project`; absolute paden naar `lees_pdf.py`. Afwijking vereist nieuw record.
- **Reviewdatum:** 2026-10-01

## DR-005 — Adoptie Ziraat Prompt Template als promptstandaard

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Prompt Architect
- **Besluit:** Prompt Passport + verplichte 10-sectiestructuur (ROLE→STOP CONDITIONS) + tokenregels + goedkeuringsregel, per `2.Ziraat Prompt Template v1.0.pdf` (identiek aan 3.4). `prompt-template.md` v2.0.
- **Reviewdatum:** 2026-10-01

## DR-006 — Migratie vijf agentprompts naar 10-sectiestandaard (Stap 5)

- **Datum:** 2026-07-03 · **Status:** Approved · **Eigenaar:** rol Prompt Architect; reviewer rol Architecture Guardian
- **Besluit:** Alle vijf agents herschreven naar 10-sectieformat (v2.0); inhoud behouden; nieuw alleen QUALITY CHECKS / TOKEN RULES / STOP CONDITIONS op basis van al goedgekeurde regels; passports in `governance/prompt-passports/`.
- **Risico/rollback:** gedragsdrift; oude teksten in sessie 2026-07-03; validatie op eerstvolgende IC-run (verwacht consistent: GEEN ACTIE bij datagaten).
- **Reviewdatum:** 2026-08-01
