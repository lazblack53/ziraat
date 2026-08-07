# Vervolgbericht voor Hermes — n.a.v. je bevestiging van 07.08.2026

Dank voor je bevestiging. De analysegedrag-afspraken (source-first, versheidscheck, Methode-A-detectie, expliciete bronstatus) zijn precies goed — houden zo. Er zijn nog twee punten die je bevestiging niet dekt, omdat het geen analysegedrag is maar wijzigingen aan de pipeline zelf.

## 1. Gmail-stap volledig verwijderen (nieuwe info)

De Gmail/Ziraat-bron gebruik ik niet meer — die hoeft dus niet gerepareerd te worden, maar mag **helemaal uit de pipeline**:

- Verwijder de `gmail-ziraat`-scrape-stap uit de dagelijkse run.
- Daarmee verdwijnt ook de dagelijkse `RefreshError: disabled_client`-melding uit de manifest/errors — die vervuilt nu al wekenlang elke bundel.
- Je noemde Gmail in je bevestiging nog als "kwetsbaar onderdeel": dat kan van je lijst af.

## 2. Infra-fixes: graag expliciet bevestigen (uitvoeren, niet omheen werken)

Je bevestiging beschrijft hoe je met de bekende gebreken **omgaat** tijdens `Report`. Vier punten vragen echter een fix ín de pipeline zelf — anders blijven de bundelbestanden onbetrouwbaar voor iedere lezer buiten jouw `Report`-flow. Graag per punt bevestigen of (en wanneer) je dit uitvoert:

| # | Fix | Wat er moet gebeuren | Klaar wanneer |
|---|---|---|---|
| a | **yfinance installeren** | `pip install yfinance` op de host(s) die `add_tradingview_analysis.py` draaien | Geen `tradingview-error.txt` meer in de bundel én `data_date` = bundeldatum in `tradingview-summary.json` |
| b | **PyMuPDF/fitz installeren** | `pip install pymupdf` op álle pipeline-hosts (de fout is aan/uit per dag — vermoedelijk mist één van meerdere hosts de dependency) | `embedded-links/` structureel gevuld, geen `No module named 'fitz'`-skips meer |
| c | **Cache-fallback zichtbaar maken in de `.md`** | Bij fallback-cache: waarschuwingsheader bovenaan `tradingview-deep-watchlist.md` + data-leeftijd per rij; regime-label onderdrukken of als "STALE" markeren bij >50% cache-symbolen | Eerstvolgende 429-dag toont de waarschuwing in de `.md` zelf (niet alleen `cache_note` in de `.json`) |
| d | **Methode-A-targetformule vervangen of velden schrappen** | In `master-stratejist-advies-kader.{md,json}` (en `tradingview-summary.json`): `entry_trigger = resistance_20d × 1,005` met `target_1 = resistance_20d` levert per constructie target < trigger — vervang de targetmethodiek, of laat entry/target-velden weg en behoud alleen beschrijvende marktdata | `target_1 > entry_trigger` in elke record, óf de velden zijn verwijderd |

Twee kleinere punten uit de oorspronkelijke lijst blijven ook staan (lagere prioriteit):

- **Hisse Öneri Portföyü**: zelfde bestand sinds 20.05 (>12 weken, vaste bron-URL). Graag hash-vergelijking met de vorige download en een `"unchanged_since": "<datum>"`-veld in de manifest bij een identiek bestand.
- **Chart-screenshots** (`tradingview/chart-screenshots/`): op 04.08 aangekondigd als vast dagelijks onderdeel, sindsdien afwezig. Herstellen, of expliciet bevestigen dat het vervallen is — dan richt ik de handmatige fallback opnieuw in.

## 3. Optioneel — İş Yatırım-cookies tegen het quota-probleem

Je cookie-protocol klinkt goed. Als ik ingelogde `isyatirim.com.tr`-cookies aanlever, lost dat dan de "Not enough quota to unlock this post"-blokkade op de İş-tekstlaag op? Zo ja: laat weten in welk formaat je ze wilt ontvangen, dan overweeg ik dat.

---

**Kort:** punt 1 en 2a-2d graag expliciet bevestigen met een verwachte datum; de "klaar wanneer"-kolom is waar ik per bundel op controleer.
