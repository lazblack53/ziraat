# Ziraat

A personal, agent-based investment-analysis system for **BIST (Borsa Istanbul)**, built on top of [Claude Code](https://claude.com/claude-code). It reads daily broker research (PDF/Excel) from three Turkish brokers, runs it through a multi-agent "Investment Committee," and produces structured, methodology-constrained trading advice.

This is a personal tool, published for reference and reuse of the pattern. **It is not financial advice, not a product, and not actively supporting external users** — issues/PRs may not get attention.

## What this is

Four layers, coordinated by a set of [Claude Code subagents](https://docs.claude.com/en/docs/claude-code/sub-agents):

1. **Data** — daily broker PDF/Excel bundles (ZFG Yatırım, İş Yatırım, Halk Yatırım) and portfolio snapshots, delivered by an external scraper pipeline. *Not included in this repo* (see [Privacy](#privacy--whats-not-here)).
2. **Tooling** — [`lees_pdf.py`](lees_pdf.py), a small PyMuPDF/openpyxl-based extractor for turning broker PDFs and Excel sheets into plain text.
3. **Agents** — an "Investment Committee" of analysis agents plus a set of governance agents, defined in [`.claude/agents/`](.claude/agents/), each with its own persistent memory.
4. **Governance** — [`blueprint/`](blueprint/): a written constitution, a decision register (ZD-xxxx), agent/prompt "passports," workflows, and a risk register that constrain how the agents are allowed to change over time.

## Repository layout

| Path | Contents |
|---|---|
| `lees_pdf.py` | PDF/Excel text extraction tool |
| `.claude/agents/` | 11 agent definitions (5 Investment Committee + 6 governance) |
| `blueprint/` | Constitution, decision register, agent/prompt passports, review workflows, risk register |
| `knowledge/`, `reports/` | Distilled knowledge base and review-report output (structure created just-in-time; see each folder's README) |
| `CLAUDE.md` | Full project instructions for Claude Code — naming conventions, report taxonomy, agent responsibilities, decision-priority rules |

## The agent system

**Orchestrator — `Master-Stratejist`:** coordinates the specialists and synthesizes a single recommendation. Runs either a lightweight daily **monitor mode** (checks gates/triggers/portfolio against the last committee decision, no specialist calls) or escalates to the **full IC workflow**:

| Agent | Focus | Priority |
|---|---|---|
| Macro-Stratejist | Central bank policy, inflation, CDS, FX regime | 1–2 (highest) |
| Hisse-Analist | Equity fundamentals, sector rotation | 4 |
| Teknik-Analist | Chart timing, entry/exit levels | 5 (lowest) |
| Risk-Yoneticisi | Drawdown, concentration, stop-loss — final filter | Final filter |

**Decision priority when signals conflict:** macro regime → liquidity → foreign flow/sentiment → sector rotation → technical timing. Macro overrides technical; risk management overrides return potential.

**Governance agents** (`Agent-Reviewer`, `Architecture-Guardian`, `Documentation-Manager`, `Prompt-Architect`, `Risk-Manager`, `Token-Optimizer`) audit and evolve the agents/prompts themselves, gated by the rules in `blueprint/`.

Full detail — naming conventions, per-broker report taxonomy, the entry/stop/target methodology rule (DR-003: only multi-timeframe "Method B" is valid; the resistance-swing "Method A" is structurally invalid), and how agent memory is organized — lives in [`CLAUDE.md`](CLAUDE.md).

## Requirements

```bash
pip install pymupdf openpyxl
```

## Usage

```bash
# Extract text from a broker PDF or Excel report
python3 lees_pdf.py "path/to/report.pdf"

# List all PDFs and Excel files under a directory
python3 lees_pdf.py --lijst raporlar/

# List the N most recently added files (newest first)
python3 lees_pdf.py --recent 15 raporlar/
```

Agents are invoked from Claude Code via `@Agent-Name` in chat.

## Privacy / what's not here

This system runs against real personal financial data. That data is deliberately kept out of this repository:

- `raporlar/` (broker PDFs/Excel) and `portföyüm/` (portfolio screenshots + raw scraper data) were never tracked in git (`.gitignore`).
- `.claude/agent-memory/` — per-agent persistent memory, including the daily Investment Committee decisions — contained concrete personal portfolio figures (balances, position sizes, deposit amounts) and has been **removed from git history entirely** as part of preparing this repo for public release. It now exists only on disk, untracked.

What remains public is the tooling, the agent definitions/prompts, and the governance framework — the reusable pattern, not the personal data that runs through it.

## License

No license has been chosen yet — all rights reserved by default under copyright law. Open an issue if you'd like to discuss reuse.
