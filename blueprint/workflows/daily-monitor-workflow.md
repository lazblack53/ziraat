# Daily Monitor Workflow

- **Versie:** v1.0 · **Datum:** 2026-08-07 · **Eigenaar:** Master-Stratejist (rol COO/orkestratie)
- **Decision record:** ZD-0012 · **Cadans:** dagelijks (handelsdagen), default-modus voor de dagelijkse check
- **Vervangt:** niets — dit is een lichte voorloper vóór de volledige IC-workflow, die ongewijzigd blijft voor escalatiegevallen

## Doel

De dagelijkse marktcheck uitvoeren tegen ~20% van de kosten van een volledige IC-run. Aanleiding (traject-analyse 07.08.2026): 20+ opeenvolgende volledige IC-runs (~150k tokens, ~35 min elk) eindigden in GEEN ACTIE omdat de uitkomst al door dezelfde gesloten gates werd bepaald. De beslislogica is gate-gedreven; een dagelijkse check hoeft dus alleen de gate-standen en triggers te verifiëren — de volledige vierspecialisten-workflow is pas nodig als er iets verandert.

## Stappenvolgorde

Uitgevoerd door Master-Stratejist **zonder** de vier specialisten aan te roepen:

1. **Pre-flight datakwaliteit** — de 5 verplichte checks uit de eigen prompt (T+1, TV-versheid, Methode-A, WebSearch-marge, netto-R:R waar van toepassing).
2. **Rapport-refresh** — nieuwste dagbundel-bronnen voor gate-cijfers: ZFG Sabah Stratejisi + Teknik Bülten (BIST100/XBANK T+1-close, destek/direnç), ZFG FX Bülteni (Brent/USD-TRY broker-bevestigd), Halk Finansal Radar (CDS 5Y, TCMB, TÜFE).
3. **Gate-standen bijwerken** (uitsluitend op T+1-bevestigde cijfers): BIST100 vs 14.000-kill-switch en 14.300-oliebucket-poort · Brent vs 85/82-hysterese · XBANK-groendagenteller · lopende bank-printvoorwaarde (3Ç26).
4. **Trigger-check watchlist** — candle-close van gisteren vergelijken met de opgeslagen entry-triggers en stops uit het laatste ic_rapport; alleen vergelijken, geen nieuwe niveaus construeren.
5. **Portefeuille-check** — nieuwste screenshot: totaalstand, GLDTR-K/Z en allocatie vs 5–10%-band, TP2-stand.
6. **Escalatiebeslissing** — beslisregels hieronder langslopen; bij géén escalatie: monitor-rapport schrijven en stoppen.

## Beslisregels (escalatie naar volledige IC-workflow)

Eén of meer waar → volledige IC-run (stappen 1–5 van de vaste workflow, alle vier specialisten):

- **E1. Gate-statuswijziging** op T+1-bevestigde basis: BIST100 kruist 14.000 of 14.300 · Brent bevestigt <82 of herkruist 85 · XBANK bereikt een 2e opeenvolgende groendag · een bankprint-voorwaarde wijzigt.
- **E2. Trigger- of stop-raak:** candle-close boven een opgeslagen entry-trigger van een watchlist-naam, of onder een stop/invalidatieniveau van een bestaande positie of actieve setup.
- **E3. Inlegdag:** de 20e van de maand of de 2 handelsdagen ervoor (allocatieplan vereist volledige toets).
- **E4. Fundamenteel nieuws** dat een fundamentele top-3-naam direct raakt (nieuwe kwartaalcijfers, koersdoel-/advieswijziging, M&A/regulatoir).
- **E5. Hedge-alarm:** GLDTR buiten de 5–10%-band of K/Z < -3%.
- **E6. Kritieke datastoring** ontdekt in pre-flight die eerdere besluiten of gate-standen raakt (bv. gecorrigeerde broker-cijfers).
- **E7. Gebruikersverzoek** om een volledige IC-analyse — expliciet verzoek overrult altijd de monitor-modus.

Twijfelgevallen escaleren (Constitution: bij twijfel de striktere route).

## Rapport

`.claude/agent-memory/Master-Stratejist/monitor_DDMMYYYY.md` — bewust een **andere naamreeks** dan `ic_rapport_DDMMYYYY.md`: de ic_rapport-reeks blijft exclusief voor volledige IC-besluiten (authoritatief), monitor-rapporten zijn statuschecks. Compact format:

1. Gate-standen (tabel: gate, stand, delta t.o.v. vorige, bron+datum)
2. Trigger-check (per watchlist-naam: close vs trigger/stop, geraakt ja/nee)
3. Portefeuille (totaal, GLDTR-band, TP2)
4. Data gaps (alleen wijzigingen t.o.v. de staande checklist)
5. Escalatiebeslissing (E1–E7 langsgelopen; GEEN ESCALATIE of ESCALATIE + reden)

Bij escalatie: het monitor-rapport afronden mét de escalatiereden, daarna de volledige IC-workflow starten; het ic_rapport van die dag verwijst naar het monitor-rapport als aanleiding.

## Stopcondities

- Pre-flight faalt op alle broker-bronnen tegelijk (geen enkel T+1-cijfer beschikbaar) → geen gate-update mogelijk, melden aan gebruiker, geen standen "doorrollen" alsof bevestigd.
- Portefeuillestand niet vaststelbaar (geen recent screenshot) → monitor-rapport zonder sectie 3, expliciet gemarkeerd.
- De vraag betreft iets anders dan de dagelijkse check (nieuwe analyse, wijziging, orderadvies) → buiten scope, normale route.

## Tokenregels

- Richtlijn ≤ 5 rapporten per monitor-run, uitsluitend uit de gate-bronnenlijst van stap 2; geen specialist-aanroepen; geen thesis-bestanden herlezen (triggers staan in het laatste ic_rapport).
- Monitor-rapport compact: tabellen, geen proza-herhaling van ongewijzigde standen.

## Kwaliteitseisen

1. Elke gate-stand heeft een T+1-broker-bron met datum; WebSearch-only-standen expliciet als onbevestigd gemarkeerd (pre-flight regel 4).
2. Geen nieuwe niveaus, targets of R:R-berekeningen in monitor-modus — dat is specialistenwerk en dus per definitie een escalatie.
3. De E1–E7-checklist wordt volledig langsgelopen en gerapporteerd, ook als de uitkomst overal "nee" is.
4. Een monitor-rapport is nooit een beleggingsbesluit; het bevestigt hooguit dat het laatste IC-besluit van kracht blijft.
