# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This project is a personal investment-analysis system for BIST (Borsa Istanbul), built around daily reports from three brokers — ZFG Yatırım, İş Yatırım, and Halk Yatırım (added 07.08.2026). It has four layers:

1. **Data** — `raporlar/` (broker PDFs/Excel, ~900 MB) and `portföyüm/` (portfolio screenshots + raw scraper data), fed by an external daily scraper pipeline that delivers zip bundles.
2. **Tooling** — `lees_pdf.py` (PyMuPDF-based text extraction from PDFs and Excel).
3. **Agents** — an Investment Committee of analysis agents plus a set of governance agents, defined in `.claude/agents/`, with persistent per-agent memory in `.claude/agent-memory/`.
4. **Governance** — `blueprint/` (constitution, decision records ZD-xxxx, agent/prompt passports, workflows, risk register).

## Project Layout

| Path | Contents | In git? |
|---|---|---|
| `raporlar/` | Broker reports (ZFG categories 1–11, İş Yatırım 1–8, Halk Yatırım 1–9, `IC Raporları/`) | No (`.gitignore`) |
| `portföyüm/` | Portfolio screenshots (PNG) + `YYYY-MM-DD_ruwe-data/` archives (raw/tradingview/tefas) | No (`.gitignore`) |
| `lees_pdf.py`, `CLAUDE.md` | Tooling and project instructions | Yes |
| `.claude/agents/` | Agent definitions (11) | Yes |
| `.claude/agent-memory/` | Per-agent persistent memory: IC reports (`ic_rapport_DDMMYYYY.md`), regime logs, feedback/reference notes | No (`.gitignore`, since 17.09.2026) |
| `blueprint/` | Governance: books 1–4, constitution, decision register, passports, workflows | Yes |
| `knowledge/`, `reports/` | Knowledge base and review-report output. Subfolders are created just-in-time with the first document (ZD-0011); taxonomy and filename formats live in each README | Yes |

Git: repository on branch `main`; only the text/knowledge/tooling layer is versioned. `raporlar/`, `portföyüm/` and `.claude/agent-memory/` are deliberately ignored (large binaries, privacy-sensitive screenshots, and concrete personal portfolio figures respectively — repo went public on 17.09.2026, see below). Commit after meaningful changes to agents, blueprint, or tooling; agent-memory changes are no longer committed.

**Note (17.09.2026):** this repo was converted from private to public. `.claude/agent-memory/` was purged from git history entirely (267 historical file versions, via `git filter-repo`) because it contains concrete personal portfolio figures (balances, position sizes, deposit amounts) — it now lives only on disk, untracked. One leaked balance figure in `blueprint/book-01-foundation/00-executive-summary.md` was redacted from history the same way. Going forward, agent-memory stays local-only; if it needs versioning again, use a separate private repo, not this one.

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
- Full IC workflow: (1) Macro-Stratejist → market regime, (2) Hisse-Analist → fundamental top-picks, (3) Teknik-Analist → entry/stop/target levels, (4) Risk-Yoneticisi → stress-test the plan, (5) consolidate into one coherent advice.
- **Monitor mode (default for the daily check, since 07.08.2026/ZD-0012):** Master-Stratejist alone verifies gate states, watchlist triggers, and the portfolio against the last `ic_rapport` — no specialist calls, output `monitor_DDMMYYYY.md`. Escalates to the full IC workflow on any of the criteria E1–E7 in `blueprint/workflows/daily-monitor-workflow.md` (gate change, trigger/stop hit, deposit day ±2, top-3 fundamental news, hedge alarm, critical data failure, explicit user request). The `ic_rapport_DDMMYYYY.md` series remains exclusively for full IC decisions.

**Specialists:**
| Agent | Focus | Priority | Primary Report Folders |
|---|---|---|---|
| Macro-Stratejist | TCMB policy, inflation, CDS, FX regime | 1–2 (highest) | ZFG: `1. Sabah Stratejisi`, `3. Günlük FX Bülteni`, `8. Özel Raporlar` — İş: `2. ELÜS Günlük Bülteni`, `6. FX Teknik Analiz Raporu`, `8. Özel Raporlar` — Halk: `5. Finansal Radar`, `1. Günlük Piyasa Yorumu` |
| Hisse-Analist | BIST equity fundamentals, sector rotation | 4 | ZFG: `1. Sabah Stratejisi`, `4. Günlük Şirket Getiri ve Çarpanları`, `5. Şirket Raporları`, `6. Hisse Öneri Portföyü`, `8. Özel Raporlar`, `9. Pay Piyasası`, `11. Toplantı Notları` — İş: `3. Günlük Yabancı Oranları`, `7. Şirket Raporları`, `8. Özel Raporlar` — Halk: `7. Analist Tavsiyeleri ve Hedef Fiyatları`, `8. Yabancı Takas Oranları`, `9. Özel Raporlar` |
| Teknik-Analist | Chart timing, entry/exit levels | 5 (lowest) | ZFG: `2. Günlük Teknik Bülten`, `7. Haftalık Teknik Hisse Önerileri` — İş: `1. Teknik Bülten`, `6. FX Teknik Analiz Raporu` — Halk: `2. Günlük Teknik Bülten`, `3. VİOP Teknik Analiz Bülteni`, `4. Sentiment Algo Bülteni` |
| Risk-Yoneticisi | Drawdown, concentration, stop-loss | Final filter | ZFG: `8. Özel Raporlar`, `9. Pay Piyasası`, `10. Fonlar` — İş: `8. Özel Raporlar` (Bankacılık sektör, CFTC) — Halk: `6. Yatırım Fonları Haftalık Bülteni` |

Agent files use hardcoded absolute paths (`/home/developer/projects/ziraat/`) when invoking `lees_pdf.py` via the Bash tool.

**Governance agents** (review/meta layer, not part of the IC workflow): `Agent-Reviewer` (periodic agent audits), `Architecture-Guardian` (GO/REVISE/NO-GO on architecture and prompt changes), `Documentation-Manager` (doc audits, changelog/glossary), `Prompt-Architect` (prompt design per the Ziraat prompt standard), `Risk-Manager` (risk register, pre-execution risk assessment of *changes* — distinct from Risk-Yoneticisi, which assesses *investments*), `Token-Optimizer` (token-usage audits). Their mandates live in `blueprint/governance/agent-passports/`.

**Agent memory**: each analysis agent persists knowledge in `.claude/agent-memory/<Agent-Name>/` with a `MEMORY.md` index. The authoritative IC decisions are `ic_rapport_DDMMYYYY.md` files under `Master-Stratejist/`; the recurring data-gap checklist is `Master-Stratejist/reference_data_gaps_terugkerend.md`. Read these before re-analyzing anything.

**Key methodology rule (DR-003)**: entry/stop/target levels must use *Methode B* (multi-timeframe hold-reclaim). *Methode A* (resistance-swing: `entry_trigger ≈ resistance_20d × 1,005` with `target_1 = resistance_20d`) is structurally invalid — target below trigger by construction. The auto-generated `master-stratejist-advies-kader.{md,json}` in the daily bundles uses Methode A and is raw input, never an IC decision. Minimum net R:R (after ~0.8–1.0% round-trip costs) is 2x.

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

`raporlar/` contains PDF reports from three brokers, each in their own subtree, plus `IC Raporları/`.

### IC Raporları (`raporlar/IC Raporları/`)

Organized by month subdirectory. Contains the auto-generated daily `master-stratejist-advies-kader.{md,json}` (one running file per month, overwritten daily — raw TradingView-derived input, **not** a validated IC decision) and dated synthesis reports (`YYYY-MM-DD_turkiye-yatirim-report.md`). The real IC decisions live in `.claude/agent-memory/Master-Stratejist/ic_rapport_DDMMYYYY.md`.

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

Portfolio data lives at the **project root**, not under `raporlar/`:
- `portföyüm/` — User's portfolio screenshots, named `YYYY-MM-DD_HH-MM_portfoy.png`; read the newest one with the Read tool directly as an image. Also contains `YYYY-MM-DD_ruwe-data/` folders archiving raw scraper output (`raw/` HTML, `tradingview/`, `tefas/`) per bundle day.
- Incoming zip bundles (`ziraat-is-report-*.zip` and variants) land in `portföyüm/`; the routing table for unpacking them lives in Claude's memory (`reference_bundle_routing`). After archiving, the zip is deleted.

ZFG PDF filenames follow the pattern: `ZFG_YATIRIM_<type-code>_<date>-pdf_<id>.pdf`

Date format varies by report type:
- Most reports: `DD-MM-YY` (2-digit year) — e.g. `ZFG_YATIRIM_tb_21-04-26-pdf_676.pdf` (`tb` = teknik bülten)
- FX bülten (`fb`): `DD-MM-YYYY` (4-digit year) — e.g. `ZFG_YATIRIM_fb_07-04-2026-pdf_623.pdf`

### İş Yatırım (`raporlar/İş Yatırım/`)

Organized by category (numbered folders) and then by month subdirectory (`06.jun`, `07.jul`, etc.) or year. Older files follow the pattern `YYYY-MM-DD_<ReportType>_DD-MM-YYYY.pdf`; files imported since late June 2026 follow the Naamgevingsstandaard below (e.g. `2026-07-06_is-yatirim_elus-bulteni.pdf`). Article-text snapshots are saved as `.txt` alongside PDFs; İş Yatırım articles are often partially paywalled ("Locked marker: True" in the txt header) — the teaser above the paywall usually contains the key numbers.

- `1. Teknik Bülten` — Daily technical bulletin (İş Yatırım)
- `2. ELÜS Günlük Bülteni` — Daily TÜRİB ELÜS spot-market bulletin (Elektronik Ürün Senedi: electronic warehouse receipts for agricultural commodities — **not** equities; limited relevance for BIST equity analysis)
- `3. Günlük Yabancı Oranları` — Daily foreign investor ratio report
- `4. Piyasalarda Bugün` — Daily market summary bulletin
- `5. İş Varant Raporu` — Daily warrant report
- `6. FX Teknik Analiz Raporu` — Daily FX technical analysis (published on select days)
- `7. Şirket Raporları` — Company initiation/update reports, organized by year (e.g. `2026/`)
- `8. Özel Raporlar` — Periodic special reports: sector analyses (Bankacılık), CFTC FX Trader, Eurotahvil market updates

### Halk Yatırım (`raporlar/Halk Yatırım/`)

Added 07.08.2026 as a third daily broker source. Organized by category (numbered folders) and then by month subdirectory (`08.aug`, etc.), same convention as the other two brokers. Each report's own `.txt` snapshot carries a `Use:` header line from the scraper (e.g. "Risk Officer: CDS, TCMB rate...") that summarizes its intended analytical role — worth reading when triaging a new/unfamiliar Halk report type.

- `1. Günlük Piyasa Yorumu` — Daily market/macro/BIST commentary
- `2. Günlük Teknik Bülten` — Daily technical bulletin: XU100/XU030/XBANK levels, MA, MACD, RSI, SuperTrend
- `3. VİOP Teknik Analiz Bülteni` — Daily futures (VİOP) technical analysis: XU030, USD/TRY, gold/silver pivots, open interest
- `4. Sentiment Algo Bülteni` — Daily BIST30 sentiment/breadth/momentum leaders & laggards
- `5. Finansal Radar` — Daily macro/risk dashboard: CDS 5Y, TCMB policy rate, TÜFE, BIST100 in USD, global comparison data — the first broker-native source for CDS Turkey 5Y (previously a chronic WebSearch-only data gap, see `reference_data_gaps_terugkerend`)
- `6. Yatırım Fonları Haftalık Bülteni` — Weekly fund/TEFAS context bulletin (published Mondays, stays current through the week)
- `7. Analist Tavsiyeleri ve Hedef Fiyatları` — Weekly consensus analyst target prices/upside (valuation sanity-check, not a standalone buy signal; published Mondays)
- `8. Yabancı Takas Oranları` — Foreign custody/clearing ratio analysis (foreign-flow scout)
- `9. Özel Raporlar` — Irregular/on-request reports, e.g. Fiyat Tespit Raporu değerlendirmesi (IPO price-determination report reviews) — no month subfolder needed yet given the low, irregular volume; revisit if volume grows

**Note (07.08.2026):** the 07.08 direct edits (Halk Yatırım mapscope across the four specialists + Master, the PRE-FLIGHT DATAKWALITEIT section, the broker-precedence rule, and the monitor-mode default) were made on explicit user request outside the formal Prompt-Architect/Architecture-Guardian flow, and are retroactively formalized in **ZD-0012** (`blueprint/governance/decision-register.md`); agent footers now reference `DR-006, ZD-0012`. The prompt-passports themselves have NOT yet been updated — that is delegated to the August prompt-review run (per ZD-0012), together with the still-open passport question for the six governance agents.

## Naamgevingsstandaard (nieuwe bestanden)

Bestaande bestanden worden niet hernoemd. Nieuwe imports volgen onderstaande standaard.

**Algemeen patroon:**
```
YYYY-MM-DD_bron_rapporttype_korte-titel.ext
```

| Veld | Waarden |
|---|---|
| `bron` | `zfg`, `is-yatirim`, `halk` |
| `rapporttype` | `sabah-stratejisi`, `teknik-bulten`, `elus-bulteni`, `fx-bulten`, `sirket-getiri`, `hisse-oneri`, `haftalik-teknik-oneri`, `yabanci-oranlari`, `piyasalarda-bugun`, `varant-raporu`, `fx-teknik-analiz`, `ozel-rapor`; Halk-specifiek: `piyasa-yorumu`, `viop-teknik-analiz`, `sentiment-algo`, `finansal-radar`, `fon-bulteni`, `analist-tavsiyeleri`, `yabanci-takas-oranlari` |
| `korte-titel` | optioneel, alleen bij speciale rapporten (bijv. ticker of onderwerp); vaste İş-`ozel-rapor`-suffixen: `pay-geri-alimlari`, `sermaye-artirimlari-temettu`, `aciga-satis`, `en-cok-onerilenler-degisiklik`; vaste Halk-`ozel-rapor`-suffix: `fiyat-tespit-<ticker/onderwerp>` |

**Voorbeelden:**
```
2026-06-16_zfg_sabah-stratejisi.pdf
2026-06-16_zfg_teknik-bulten.pdf
2026-06-16_zfg_ozel-rapor_bankacilik-kar-tahminleri.pdf
2026-06-16_is-yatirim_elus-bulteni.pdf
2026-06-16_is-yatirim_piyasalarda-bugun.txt
2026-06-16_is-yatirim_fx-teknik-analiz.pdf
2026-08-07_halk_finansal-radar.pdf
2026-08-07_halk_ozel-rapor_fiyat-tespit-bewen-enerji.pdf
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
