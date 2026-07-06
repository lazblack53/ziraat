---
document: book-02-architecture/07-knowledge-architecture.md
versie: v1.0
status: Approved
strategic_owner: Claude Code (rol: Chief AI Officer)
technical_owner: Claude Code (rol: CTO)
documentation_owner: Claude Code (rol: Documentation Manager)
review_frequentie: maandelijks
laatste_review: 2026-07-03
---

# Knowledge Architecture

Waar kennis leeft, wie haar bezit en hoe veroudering wordt voorkomen.

## Kennislagen (van vluchtig naar duurzaam)

| Laag | Locatie | Inhoud | Levensduur |
|---|---|---|---|
| Rapporten | `raporlar/` | Broker-research ZFG + İş Yatırım | dagwaarde vervalt snel; archief blijft |
| Portefeuille | `portföyüm/` | Screenshots (PNG, via Read als image) | momentopname |
| Project-memory | memory-directory + `MEMORY.md`-index | IC-besluiten, feedback, marktsignalen, pipeline-lessen | tot herroepen |
| CLAUDE.md | projectroot | Repo-structuur, tooling, naamgeving | onderhouden bij structuurwijziging |
| Blueprint | `blueprint/` | Governance, architectuur, processen | versiebeheerd, hoogste gezag |

## Bronwaarheid-regels

1. Rapportstructuur en bestandsnaamconventies: CLAUDE.md is leidend; de Blueprint dupliceert die niet.
2. Nieuwe imports volgen de naamgevingsstandaard `YYYY-MM-DD_bron_rapporttype_korte-titel.ext` (CLAUDE.md); broker-pipeline-bestanden behouden hun originele naam, URL-encoding direct decoderen.
3. Marktcijfers zijn alleen geldig met bron (rapport + datum). Rapporten ouder dan de vraagperiode worden als verouderd gemarkeerd, niet stilzwijgend gebruikt.
4. Memory-items beschrijven wat waar was op schrijfdatum; bij gebruik in een IC-run wordt de datum meegewogen.

## Bekende kennisvallen

- Image-based PDF's (<500 tekens output) — inhoud niet beschikbaar, niet "leeg" noemen.
- Günlük Teknik Bülten roteert 3 aandelen per editie — afwezigheid van een ticker is geen signaal.
- ZFG-coverage dekt niet alle BIST-tickers (GMSTR, ALTIN zonder research).
- Evergreen downloadlinks: hash-check vóór "nieuw rapport" concluderen.
- Standaard níét opgehaald maar wel besluitrelevant: CDS-niveau, yabancı payı, candle-close-bevestiging — zie data-gap-checklist (memory `reference_ic_data_gaps`).

## Veroudering voorkomen

- Reviewfrequenties per Meta-Architecture §10 (dit boek: maandelijks).
- Bij conflict tussen kennislagen: Blueprint-conflictvolgorde (§13); lager document wordt aangepast of gemarkeerd als verouderd.
- Kennisevolutie (nieuwe bronnen, nieuwe checklists): `book-04-evolution/`, met change-log-regel.
