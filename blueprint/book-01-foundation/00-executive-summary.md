---
document: book-01-foundation/00-executive-summary.md
versie: v1.0
status: Approved
strategic_owner: Gebruiker
technical_owner: Claude Code (rol: Architecture Guardian)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: per kwartaal
laatste_review: 2026-07-03
---

# Executive Summary

## Wat is Ziraat

Ziraat is een persoonlijk multi-agent beleggingsanalyse-systeem voor de Turkse markt (BIST, FX, fondsen). Het combineert dagelijkse brokerresearch van ZFG Yatırım en İş Yatırım (PDF/Excel onder `raporlar/`, ontsloten via `lees_pdf.py`) met een Investment Committee van vijf Claude-agents die samen tot één risico-gecontroleerd advies komen.

## Voor wie en waarom

Eén gebruiker, die maandelijks 20.000 TRY inlegt (de 20ste) met als doel 25.000 TRY/maand rendement binnen 12–24 maanden. Het systeem bestaat omdat de rapportstroom (±750 bestanden en groeiend) te groot is om handmatig te verwerken, en omdat beslissingen discipline vereisen die door een vaste governance (Constitution, Decision Engine, IC-proces) wordt afgedwongen.

## Hoe het werkt (één alinea)

Master-Stratejist orkestreert vier specialisten in vaste volgorde: Macro-Stratejist bepaalt het marktregime, Hisse-Analist levert fundamentele picks, Teknik-Analist levert entry/stop/target-niveaus (alleen Methode B), Risk-Yoneticisi stress-test het geheel. Bij conflict wint macro van technisch en risico van rendement. Zonder sluitende data is het besluit GEEN ACTIE en blijft kapitaal in het geldmarktfonds TP2 — dat is de huidige stand ([bedrag verwijderd voor publicatie]).

## Documentstructuur

De Blueprint (`blueprint/`) is het besturingssysteem: Book I waarom, Book II hoe gebouwd, Book III hoe dagelijks gewerkt, Book IV hoe verbeterd, plus `governance/` (constitution, decision register, templates, change-log). Conflictvolgorde en regels: `Ziraat Blueprint Meta-Architecture v1.0.pdf` (projectroot).
