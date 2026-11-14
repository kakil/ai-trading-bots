# Requirements

## Course flow
Modules run in this order. Each builds on the one before.

1. **What a trading bot is, and what it can and can't do.** A bot is a program that follows exact rules on its own. It watches the market, finds signals and can place orders, and the same signal always gets the same action. It can watch markets around the clock without emotion. It can't predict the future or guarantee profit.
2. **Setup.** TradingView desktop app (Essential plan or higher, which technical alerts need), the Claude desktop app, and the TradingView MCP connecting the two.
3. **The 5 rules for bots** (below).
4. **The Turtle traders** and their breakout rules, as background for the strategy.
5. **Build the bot.** Claude writes *Turtle Breakout 55/20* in Pine Script. No coding by the learner.
6. **Check the bot.** Check about 3 trades by hand against the rules.
7. **Backtest the bot.** Include commission and slippage, compare with buy and hold, read max drawdown including open trades. Past results don't predict future results.
8. **Switch it on.** Alerts by app and email only. The learner places every trade.
9. **Stay in control.** The oversight rules (below).

## The 5 rules for bots
Every bot needs all five written down before Claude builds anything.

| # | Rule | Turtle Breakout 55/20 |
|---|---|---|
| 1 | **Market and timeframe** | Bitcoin, daily chart, long only |
| 2 | **Entry** | Buy when the daily close is above the highest high of the previous 55 days |
| 3 | **Exit** | Sell when the daily close is below the lowest low of the previous 20 days |
| 4 | **Stop loss** | 2 × ATR(20) below the signal close, set at entry and kept fixed |
| 5 | **Position size** | Risk 1% of the account per trade: size = (1% of equity) ÷ stop distance |

Full spec: `strategies/turtle/SPEC.md`

## Oversight rules
1. **You are responsible** for everything the bot does. Not Claude, not TradingView.
2. **No broker or API access for Claude.** Claude builds and checks. It never places orders or holds trading credentials.
3. **Alerts only, by app and email.** You decide on, and place, every trade yourself.
4. **Pause the bot** if its live drawdown goes past the worst drawdown in the backtest.
5. **Renew alerts before they expire**, and log the renewal in `09-alerts-and-oversight-log.md`.
6. **Review regularly.** Check that each alert matched the rules, and log the review.

## Course standards
- Every step works without the learner writing code.
- Every prompt shown in the course has been run for real and logged in `05-prompts-used.md`.
- Every Pine script shown compiles in TradingView, with the check logged in `07-testing-log.md`.
- Every backtest shown is logged in `08-backtest-log.md` with full settings.
- Clear disclaimers: education only, not financial advice, no performance promises.

## Build checklist
- [ ] Setup module: TradingView desktop + Claude desktop + TradingView MCP connected
- [ ] 5 rules written for Turtle Breakout 55/20
- [ ] Turtle Breakout 55/20 v1.0.0 written in Pine Script v6
- [ ] Compiles in TradingView
- [ ] 3 trades checked by hand
- [ ] Backtest logged, with commission, slippage and a buy-and-hold comparison
- [ ] Alerts set up by app and email, and tested
- [ ] Oversight rules recorded and demonstrated

## Repository standards
- Versioned strategy files that are never overwritten.
- Training capture updated in every session.
- No secrets, account numbers or personal details.
