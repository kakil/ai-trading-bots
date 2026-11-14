# Course map

Links each course module to the captured work that will supply its material. Add a row whenever something happens that's worth teaching: a good prompt, a clear bug, a surprising backtest.

Status values: **idea** → **drafted** → **recorded** → **published**

## Modules

| # | Module | What it teaches | Source in training capture | Status |
|---|---|---|---|---|
| 1 | What a trading bot is | A program that follows exact rules on its own, and what it can and can't do | `02-requirements.md` | idea |
| 2 | Setup | TradingView desktop (Essential or higher), Claude desktop, the TradingView MCP | `03-architecture.md`, `06-bugs-and-fixes.md` | idea |
| 3 | The 5 rules for bots | Market/timeframe, entry, exit, stop loss, position size | `02-requirements.md`, `strategies/turtle/SPEC.md` | idea |
| 4 | The Turtle traders | Breakout rules as the basis for the bot | `strategies/turtle/SPEC.md` | idea |
| 5 | Build the bot | Claude writes Turtle Breakout 55/20 in Pine Script, no coding | `05-prompts-used.md`, `07-testing-log.md` | idea |
| 6 | Check the bot | Check 3 trades by hand against the rules | `07-testing-log.md` | idea |
| 7 | Backtest the bot | Commission, slippage, buy and hold, max drawdown, past ≠ future | `08-backtest-log.md` | idea |
| 8 | Switch it on | Alerts by app and email, and you place the trades | `09-alerts-and-oversight-log.md` | idea |
| 9 | Stay in control | The oversight rules | `02-requirements.md`, `09-alerts-and-oversight-log.md` | idea |

## Captured moments

| Date | Moment | Source | Module | Status |
|---|---|---|---|---|
| 2026-11-14 | Setting up a project so Claude follows the rules automatically | `04-session-log.md` | Optional extra | idea |
| 2026-11-14 | Writing the 5 rules before asking Claude to build anything | `01-decisions.md` | 3 | idea |
