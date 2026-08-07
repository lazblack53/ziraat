# Vervolgbericht 2 voor Hermes — laatste openstaande punt: chart-screenshots

Datum: 2026-08-07 (na verificatie van de 19:08-bundel)

Allereerst: de 19:08-bundel is gecontroleerd en vrijwel alles is geland — yfinance vers, eerlijke lege tabel met Data-age-kolom bij 429 (beter dan gevraagd), gmail-stap verwijderd, embedded-links gevuld, `unchanged_since`-veld bij de Hisse Öneri, en de targetformule gefixt (target > trigger, `target_valid`-veld). Netjes, dank.

Er resteert **één punt** uit de lijst:

## Chart-screenshots (`tradingview/chart-screenshots/`)

- **Situatie:** op 04.08 geïntroduceerd (5 IC-satelliet-tickers: TSKB, TURSG, CIMSA, TOASO, TAVHL + een `chart_screenshots_summary.json`) en aangekondigd als vast dagelijks onderdeel. Sindsdien in elke bundel afwezig — ook in de 19:08-bundel van vandaag staat `chart_screenshots: 0`.
- **Vraag:** herstel het onderdeel, óf bevestig expliciet dat het vervallen is — dan richt ik de handmatige fallback opnieuw in. Nu hangt het ertussenin.
- **Bij herstel, één wens uit de 04.08-ervaring:** de namiddag-regeneratie van 04.08 verloor de 1D/4H/1H-ratings aan een TradingView-429 terwijl de prijzen wél klopten. Als de ratings door een 429 niet lukken: lever de PNG's dan tóch (prijs/candles blijven bruikbaar) en zet de 429 als error in de summary-json — zelfde eerlijke-markering-aanpak als je nu al bij de deep-watchlist doet.
- **Klaar wanneer:** `tradingview/chart-screenshots/` met de 5 PNG's + summary-json terug in de bundel, óf een expliciete "vervallen"-bevestiging.

---

*PS (optioneel, geen haast): de cookie-vraag uit het vorige bericht staat ook nog open — lossen ingelogde `isyatirim.com.tr`-cookies de "Not enough quota"-blokkade op de İş-tekstlaag op, en zo ja, in welk formaat wil je ze ontvangen?*
