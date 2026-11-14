# Turtle Breakout 55/20: strategy spec

This is the rule set Claude builds from. Change the rules here first, give the change a new version, then update the Pine Script.

**Spec version:** 1.0.0 (2026-11-14)
**Pine file (when built):** `turtle_v1.0.0.pine`

## Background
The Turtle traders were a group taught to trade with fixed breakout rules. This bot uses a simplified version of their long-term system: buy breakouts to new 55-day highs and exit on breaks of 20-day lows.

## The 5 rules

| # | Rule | Setting |
|---|---|---|
| 1 | Market and timeframe | Bitcoin, daily chart (1D), long only |
| 2 | Entry | Daily close > highest high of the **previous** 55 daily bars (today's bar not included) |
| 3 | Exit | Daily close < lowest low of the **previous** 20 daily bars (today's bar not included) |
| 4 | Stop loss | Signal close − 2 × ATR(20). Set when the trade opens and **never moved** |
| 5 | Position size | Risk 1% of equity: quantity = (0.01 × equity) ÷ (2 × ATR(20)) |

Only one position at a time. No adding to winners, and no short trades.

## Inputs (exposed in settings)
| Input | Default |
|---|---|
| Entry lookback | 55 |
| Exit lookback | 20 |
| ATR length | 20 |
| Stop ATR multiple | 2.0 |
| Risk per trade | 1% |

## Signals and alerts
- Plot the 55-day high and the 20-day low on the chart.
- Mark entries, exits and stop-outs.
- Send an alert on each entry, exit and stop-out, with a message that gives the symbol, action, price and stop level.

## Backtest settings (defaults to log)
- Commission and slippage: set to realistic values for the learner's exchange, and record both in `08-backtest-log.md`.
- Compare with buy and hold over the same dates.
- Report max drawdown, including open trades.

## Hand check
Before backtesting, pick 3 trades on the chart and confirm the entry, stop and exit each match the rules above. Log the result in `07-testing-log.md`.
