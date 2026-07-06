# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This project is a PDF text extraction utility for investment reports from two brokers — ZFG Yatırım and İş Yatırım — paired with a multi-agent investment analysis system. The single script `lees_pdf.py` uses PyMuPDF to read PDFs stored under `raporlar/`.

## Dependencies

```bash
pip install pymupdf openpyxl
```

## Usage

```bash
# Extract text from a PDF or Excel file
python3 lees_pdf.py "raporlar/2. Günlük Teknik Bülten/04.apr/ZFG_YATIRIM_tb_21-04-26-pdf_676.pdf"
python3 lees_pdf.py "raporlar/10. Fonlar/borsa yatırım fonları/Borsa_Yatirim_Fonlari_EXCEL_Tum_Veri_2026-04-28.xlsx"

# List all PDFs and Excel files under a directory
python3 lees_pdf.py --lijst raporlar/

# List the N most recently added files (by mtime, newest first) — preferred way to find fresh reports
python3 lees_pdf.py --recent 15 raporlar/
python3 lees_pdf.py --recent 5 "raporlar/2. Günlük Teknik Bülten/"
```

## Agent System

All agents are defined in `.claude/agents/` and invoked via `@Agent-Name` in chat. Each file uses this frontmatter:

```yaml
---
name: Agent-Name
description: "When to use this agent"
model: sonnet          # all agents run on sonnet
color: orange          # visual only
memory: project        # agents share project-scoped memory
---
```

**Orchestrator** (`Master-Stratejist`):
- Head of Investment Committee — coordinates the four specialist agents and synthesizes their output into a consolidated recommendation.
- Workflow: (1) Macro-Stratejist → market regime, (2) Hisse-Analist → fundamental top-picks, (3) Teknik-Analist → entry/stop/target levels, (4) Risk-Yoneticisi → stress-test the plan, (5) consolidate into one coherent advice.

**Specialists:**
| Agent | Focus | Priority | Primary Report Folders |
|---|---|---|---|
| Macro-Stratejist | TCMB policy, inflation, CDS, FX regime | 1–2 (highest) | ZFG: `1. Sabah Stratejisi`, `3. Günlük FX Bülteni`, `8. Özel Raporlar` — İş: `2. ELÜS Günlük Bülteni`, `6. FX Teknik Analiz Raporu`, `8. Özel Raporlar` |
| Hisse-Analist | BIST equity fundamentals, sector rotation | 4 | ZFG: `1. Sabah Stratejisi`, `4. Günlük Şirket Getiri ve Çarpanları`, `5. Şirket Raporları`, `6. Hisse Öneri Portföyü`, `8. Özel Raporlar`, `9. Pay Piyasası`, `11. Toplantı Notları` — İş: `3. Günlük Yabancı Oranları`, `7. Şirket Raporları`, `8. Özel Raporlar` |
| Teknik-Analist | Chart timing, entry/exit levels | 5 (lowest) | ZFG: `2. Günlük Teknik Bülten`, `7. Haftalık Teknik Hisse Önerileri` — İş: `1. Teknik Bülten`, `6. FX Teknik Analiz Raporu` |
| Risk-Yoneticisi | Drawdown, concentration, stop-loss | Final filter | ZFG: `8. Özel Raporlar`, `9. Pay Piyasası`, `10. Fonlar` — İş: `8. Özel Raporlar` (Bankacılık sektör, CFTC) |

Agent files use hardcoded absolute paths (`/home/developer/projects/ziraat/`) when invoking `lees_pdf.py` via the Bash tool.

## Decision Engine

Always prioritize in this order:

1. Macro regime (faiz, enflasyon, CDS)
2. Liquidity conditions (TCMB stance, credit expansion)
3. Foreign flow / sentiment
4. Sector rotation
5. Technical timing (entry/exit only)

If signals conflict:
- Macro overrides technical
- Risk management overrides return potential

## Report Structure

`raporlar/` contains PDF reports from two brokers, each in their own subtree.

### ZFG Yatırım (`raporlar/`)

Organized by category (numbered folders) and then by month subdirectory (`01.jan`, `02.feb`, `03.mrt`, `04.apr`, `05.mei`, etc.) or year:

- `1. Sabah Stratejisi` — Morning strategy reports; also contains quarterly earnings summaries (e.g. `1Ç2026_Kar Tahminleri.pdf`) and annual BIST performance analyses
- `2. Günlük Teknik Bülten` — Daily technical bulletin
- `3. Günlük FX Bülteni` — Daily FX bulletin
- `4. Günlük Şirket Getiri ve Çarpanları` — Daily company returns and multiples
- `5. Şirket Raporları` — Company reports, organized by year
- `6. Hisse Öneri Portföyü` — Stock recommendation portfolio
- `7. Haftalık Teknik Hisse Önerileri` — Weekly technical stock recommendations
- `8. Özel Raporlar` — Special reports (sector balance sheets, banking earnings, BIST performance)
- `9. Pay Piyasası` — Company earnings reports named `TICKER-YYYY_MM_DD-QUARTER.pdf` (e.g. `AKBNK-2026_04_29-1Ç26.pdf`); also sector-level analyses
- `10. Fonlar` — All fund data, split into two subfolders each with three sort views:
  - `borsa yatırım fonları/` — Exchange-traded funds; `büyüklük bazlı/`, `getiri bazlı/`, `yönetim ücreti bazlı/`
  - `menkul kıymet fonları/` — Securities funds; same three subfolders
  - Excel files named `Borsa_Yatirim_Fonlari_EXCEL_Tum_Veri_YYYY-MM-DD.xlsx` / `Menkul_Kiymet_Yatirim_Fonlari_EXCEL_Tum_Veri_YYYY-MM-DD.xlsx`
- `11. Toplantı Notları` — Analyst meeting notes per company (bedrijfsbezoeken); filenames vary: `TICKER_Toplantı_Notları.pdf`, `CompanyName_Analist Toplantı Notu_DDMMYYYY.pdf`, or `CompanyName_YYYYMMDD.pdf`

Portfolio screenshots live at the **project root**, not under `raporlar/`:
- `portföyüm/` — User's personal portfolio screenshots (PNG); read with the Read tool directly as images:
  `Read tool → file_path: /home/developer/projects/ziraat/portföyüm/Portföyüm.png`

ZFG PDF filenames follow the pattern: `ZFG_YATIRIM_<type-code>_<date>-pdf_<id>.pdf`

Date format varies by report type:
- Most reports: `DD-MM-YY` (2-digit year) — e.g. `ZFG_YATIRIM_tb_21-04-26-pdf_676.pdf` (`tb` = teknik bülten)
- FX bülten (`fb`): `DD-MM-YYYY` (4-digit year) — e.g. `ZFG_YATIRIM_fb_07-04-2026-pdf_623.pdf`

### İş Yatırım (`raporlar/İş Yatırım/`)

Organized by category (numbered folders) and then by month subdirectory (`06.jun`, etc.) or year. Filenames follow the pattern `YYYY-MM-DD_<ReportType>_DD-MM-YYYY.pdf`.

- `1. Teknik Bülten` — Daily technical bulletin (İş Yatırım)
- `2. ELÜS Günlük Bülteni` — Daily ELÜS (equity/liquidity strategy) bulletin
- `3. Günlük Yabancı Oranları` — Daily foreign investor ratio report
- `4. Piyasalarda Bugün` — Daily market summary bulletin
- `5. İş Varant Raporu` — Daily warrant report
- `6. FX Teknik Analiz Raporu` — Daily FX technical analysis (published on select days)
- `7. Şirket Raporları` — Company initiation/update reports, organized by year (e.g. `2026/`)
- `8. Özel Raporlar` — Periodic special reports: sector analyses (Bankacılık), CFTC FX Trader, Eurotahvil market updates

## Naamgevingsstandaard (nieuwe bestanden)

Bestaande bestanden worden niet hernoemd. Nieuwe imports volgen onderstaande standaard.

**Algemeen patroon:**
```
YYYY-MM-DD_bron_rapporttype_korte-titel.ext
```

| Veld | Waarden |
|---|---|
| `bron` | `zfg`, `is-yatirim` |
| `rapporttype` | `sabah-stratejisi`, `teknik-bulten`, `elus-bulteni`, `fx-bulten`, `sirket-getiri`, `hisse-oneri`, `yabanci-oranlari`, `piyasalarda-bugun`, `varant-raporu`, `fx-teknik-analiz`, `ozel-rapor` |
| `korte-titel` | optioneel, alleen bij speciale rapporten (bijv. ticker of onderwerp) |

**Voorbeelden:**
```
2026-06-16_zfg_sabah-stratejisi.pdf
2026-06-16_zfg_teknik-bulten.pdf
2026-06-16_zfg_ozel-rapor_bankacilik-kar-tahminleri.pdf
2026-06-16_is-yatirim_elus-bulteni.pdf
2026-06-16_is-yatirim_piyasalarda-bugun.txt
2026-06-16_is-yatirim_fx-teknik-analiz.pdf
```

**Uitzonderingen:**
- Broker-pipeline bestanden (ZFG_YATIRIM_...) behouden hun originele naam; URL-encoding wel direct decoderen (`%C4%B1` → `ı`).
- Portföy screenshots: `YYYY-MM-DD_HH-MM_portfoy.png` (tijdstip voor uniciteit bij meerdere screenshots per dag).

## Code Notes

- Variable names and comments in `lees_pdf.py` are in Dutch (`lees` = read, `bestand` = file, `lijst` = list, `pad` = path, `map` = directory). Agent prompts mix Dutch and Turkish.
- The script uses `fitz` (PyMuPDF) — import name differs from package name.
- Excel files (`.xlsx`) are read via `openpyxl` with `data_only=True` (computed cell values, not formulas). Output is sheet-by-sheet, rows as tab-separated values.
- Some PDFs (notably `7. Haftalık Teknik Hisse Önerileri`) are image-based and yield only the cover page text. If extraction returns fewer than ~500 characters, the PDF is likely image-based.
- Daily technical bulletins (`2. Günlük Teknik Bülten`) cover only 3 stocks per issue on a rotating basis. A specific ticker may not appear for several weeks.
- ZFG analyst coverage universe does not include all BIST stocks. Tickers like GMSTR and ALTIN have no ZFG research reports; only technical or percentage-based stop levels can be derived for them.
