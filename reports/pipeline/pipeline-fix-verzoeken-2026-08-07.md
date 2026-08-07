# Verzoeklijst scraper-pipeline-fixes — stand 07.08.2026

**Status: doorgezet naar Hermes (pipeline-uitvoerder) op 07.08.2026.** Vervolgacties liggen bij Hermes; dit project monitort per bundel of de fixes landen (zie verificatiepunten onderaan).

Bestemd voor de beheerder van de externe scraper-pipeline (de bron van de dagelijkse `ziraat-is-report-*.zip`-bundels). Alle punten zijn buiten dit project geconstateerd maar niet oplosbaar vanuit dit project zelf. Gesorteerd op impact.

---

## P0 — breekt dagelijks de technische datalaag

### 1. `yfinance` ontbreekt op de scraper-host
- **Symptoom:** `tradingview-error.txt` in de bundel van 07.08 (09:34-pull): `ModuleNotFoundError: No module named 'yfinance'` in `/root/add_tradingview_analysis.py`, regel 125.
- **Gevolg:** `tradingview-summary.json` en `tradingview-technical-snapshot.txt` bevatten geen verse OHLC/SMA/RSI-data meer (alle 16 symbolen `data_date` = 1 dag oud + TV-aanbeveling `ERROR`).
- **Fix:** `pip install yfinance` op de host die `add_tradingview_analysis.py` draait. Let op: de pipeline lijkt op meerdere hosts te draaien (zie punt 4, fitz aan/uit-patroon) — installeer op álle hosts.
- **Status-nuance:** de 13:43-pull van dezelfde dag was wél gezond — de fout is dus intermitterend of al deels verholpen; graag bevestigen dat het structureel is opgelost.

### 2. Stille cache-fallback zonder waarschuwing in `tradingview-deep-watchlist.md`
- **Symptoom:** op 07.08 (09:34-pull) serveerde de deep-watchlist alle 16 symbolen uit een cache van **29.06** (5,5 weken oud). De `cache_note` ("Fallback cache from 2026-06-29...") staat alléén per symbool in de `.json` — de `.md`-tabel (de menselijk leesbare laag) toont gewoon cijfers en een regime-label ("VOORZICHTIG POSITIEF") alsof ze vers zijn, met een verse top-level `generated_at`.
- **Gevolg:** vergelijkbaar incident eerder op 27.07. Concreet risico-voorbeeld: TUPRS toonde 219,20 TL uit de cache terwijl de echte koers ~321,50 TL was — een schijnbare -32%-afwijking. Wie alleen de `.md` leest neemt een vals regime-label over.
- **Fix (verzoek):** bij elke cache-fallback (a) een duidelijke waarschuwingsheader bovenaan de `.md` ("⚠ CACHED DATA van <datum> — niet actueel"), (b) per rij de data-leeftijd, en (c) het regime-label onderdrukken of expliciet als "stale" markeren wanneer >50% van de symbolen uit cache komt.

## P1 — chronisch, bron al weken uitgevallen

### 3. ~~Gmail-koppeling: OAuth-client uitgeschakeld~~ — **VERVALLEN (07.08.2026)**
- De gebruiker heeft bevestigd de Gmail-bron niet meer te gebruiken. **Geen fix nodig** — de `gmail-ziraat/`-stap mag uit de pipeline worden verwijderd (scheelt ook de dagelijkse `disabled_client`-foutmelding in de manifest).

### 4. `fitz`/PyMuPDF: aan/uit per host (embedded-links vallen willekeurig uit)
- **Symptoom:** `{"source": "Embedded PDF links", "status": "skipped", "error": "No module named 'fitz'"}` op de meeste dagen; op 13–14.07 en 07.08 werkte het wél. Patroon suggereert meerdere hosts waarvan een deel PyMuPDF mist.
- **Gevolg:** `embedded-links/` (şirket-rapport-PDF's, Temettü-lijsten, ZRY-excel) ontbreekt op de uitval-dagen.
- **Fix:** `pip install pymupdf` op alle pipeline-hosts.

## P2 — datakwaliteit / hygiëne

### 5. Hisse Öneri Portföyü: >12 weken hetzelfde bestand
- **Symptoom:** de download levert sinds 20.05 byte-voor-byte hetzelfde PDF (sha256 `598bf964...`). De bron-URL is een vaste (niet datumspecifieke) link.
- **Verzoek:** (a) nagaan of ZFG dit rapport inmiddels elders publiceert, en (b) in de pipeline een hash-vergelijking met de vorige download toevoegen — bij identiek bestand het veld `"unchanged_since": "<datum>"` aan de manifest toevoegen i.p.v. het stilzwijgend als verse download te presenteren.

### 6. Chart-screenshots-submap: toezegging van 04.08 niet nagekomen
- **Symptoom:** op 04.08 werd `tradingview/chart-screenshots/` (5 IC-satellite-tickers) aangekondigd als vast dagelijks onderdeel; sindsdien 3 dagen op rij afwezig (05–07.08, `chart_screenshots: 0`).
- **Verzoek:** herstellen, of expliciet bevestigen dat dit onderdeel vervallen is (dan richten wij de handmatige fallback opnieuw in).

### 7. `master-stratejist-advies-kader.{md,json}`: targetberekening structureel ongeldig (Methode A)
- **Symptoom:** het auto-advieskader gebruikt `entry_trigger = resistance_20d × 1,005` met `target_1 = resistance_20d` — het target ligt daarmee per constructie ónder de trigger. Sinds 23.07 vastgesteld dat ook `tradingview-summary.json`/`technical-snapshot.txt` dezelfde formule bevatten.
- **Gevolg:** de entry/target-velden zijn onbruikbaar; dit project negeert ze structureel (intern besluit DR-003), maar dat maakt de helft van het kader dode data.
- **Verzoek:** de targetmethodiek vervangen door een defensibele variant (bv. target boven de trigger op basis van volgende weerstandszone), of de entry/target-velden weglaten en alleen de beschrijvende marktdata behouden.

## P3 — bekend, ter info

### 8. İş Yatırım-artikel-quota ("Not enough quota to unlock this post / Unlock left: 0")
- Sinds 07.07 wisselt de İş-artikeltekst-laag onvoorspelbaar tussen bruikbare teasers en kaal navigatie-boilerplate. De PDF-nevenlinks ("Pdf rapora ulaşmak için tıklayınız") omzeilen de blokkade betrouwbaar en worden al door de pipeline meegepakt — dat werkt goed, graag zo houden. Structurele oplossing zou een account-quota-aanvulling zijn; ter afweging aan de beheerder.

---

## Verificatiepunten per bundel (voor dit project, na doorzending aan Hermes)

Bij elke nieuwe bundel checken of een fix geland is — per punt het snelste signaal:
1. **yfinance**: geen `tradingview-error.txt` meer én `data_date` = bundeldatum in `tradingview-summary.json`.
2. **Cache-waarschuwing**: `.md`-tabel toont een expliciete stale-markering wanneer de `.json` een `cache_note` bevat (test pas beoordeelbaar bij de eerstvolgende 429-dag).
3. **Gmail**: ~~vervallen~~ — bron gedeprecieerd door gebruiker (07.08); ideaal eindbeeld: de `disabled_client`-fout verdwijnt uit de manifest doordat de stap verwijderd is. Afwezigheid van `gmail-ziraat/` is voortaan de verwachte normaaltoestand, geen gap.
4. **fitz**: `embedded-links/` structureel gevuld (niet meer aan/uit per dag).
5. **Hisse Öneri**: nieuwe sha256 (≠ `598bf964...`) of een `unchanged_since`-veld in de manifest.
6. **Chart-screenshots**: `tradingview/chart-screenshots/`-submap terug (of expliciete bevestiging dat het vervallen is).
7. **Methode-A-kader**: `target_1 > entry_trigger` in `master-stratejist-advies-kader.json`, of de velden zijn verwijderd.
8. **İş-quota**: "Unlock left" > 0 in de artikel-txt's (alleen ter info, geen harde eis).

*Opgesteld vanuit het Ziraat-analyseproject; de gedetailleerde incidenthistorie per punt staat in de projectmemory (`feedback_pipeline_scraper_gaps`) en is op verzoek beschikbaar.*
