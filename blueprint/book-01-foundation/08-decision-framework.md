---
document: book-01-foundation/08-decision-framework.md
versie: v1.0
status: Approved
strategic_owner: Gebruiker
technical_owner: Master-Stratejist
reviewer: Risk-Yoneticisi
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: per kwartaal
laatste_review: 2026-07-03
---

# Decision Framework

Hoe Ziraat van signalen naar één besluit komt. Formeel vastgelegd als DR-002.

## Signaalprioriteit (Decision Engine)

1. **Macro-regime** — faiz, enflasyon, CDS (Macro-Stratejist)
2. **Liquiditeit** — TCMB-stance, kredietexpansie
3. **Buitenlandse stromen / sentiment** — yabancı oranları
4. **Sectorrotatie** — (Hisse-Analist)
5. **Technische timing** — uitsluitend entry/exit (Teknik-Analist)

## Conflictregels

- Macro overrulet technisch.
- Risk management overrulet rendementspotentieel.
- Bij documentconflicten geldt de volgorde uit Meta-Architecture §13 (Constitution → Meta-Architecture → Decision Register → Book II → III → IV → lokaal → inline).

## IC-besluitproces

1. Master-Stratejist draait de vier specialisten in vaste volgorde (regime → picks → niveaus → stress-test).
2. Elk trade-voorstel bevat: entry, stop, target (Methode B), netto R:R inclusief kosten, positiegrootte, bron per niveau.
3. Risk-Yoneticisi is de laatste filter; zonder diens akkoord geen voorstel aan de gebruiker.
4. **Default is GEEN ACTIE.** Ontbreekt een R:R-input (bijv. candle-close-bevestiging, yabancı-data, CDS), dan blijft kapitaal in TP2. Precedenten: IC-besluiten 20-06, 30-06, 01-07, 02-07 (alle GEEN ACTIE wegens datagaten).
5. De data-gap-checklist (memory: `reference_ic_data_gaps`) wordt vóór elk IC-besluit afgelopen.
6. Uitkomst wordt vastgelegd in project-memory; architectuur- of procesbeslissingen daarnaast in het Decision Register.

## Drempels voor een Decision Record

Verplicht bij: nieuwe/verwijderde agents, architectuurwijziging, nieuwe workflows, grote promptwijzigingen, wijzigingen met kosten- of risico-impact (Meta-Architecture §7).
