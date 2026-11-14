# Architecture

## Tool chain

```
Learner ──prompts──▶ Claude ──TradingView MCP──▶ TradingView
                       │                          ├─ Pine Editor (strategy)
                       │                          ├─ Strategy Tester (backtest)
                       │                          └─ Alerts
                       └─ writes Pine Script, explains results

TradingView alerts ──app / email──▶ Learner ──places trade by hand──▶ Broker
```

Claude has no broker or API access. The learner places every order.

## Apps and plans
- **TradingView desktop app**, Essential plan or higher (technical alerts need a paid plan)
- **Claude desktop app**
- **TradingView MCP**, which connects Claude desktop to TradingView desktop

## TradingView MCP
- **Server:** *to be recorded (name, source link, version or commit)*
- **How it connects:** *to be recorded*
- **What it can do:** *to be recorded (read chart data, write scripts, run backtests, manage alerts)*
- **Secrets:** *where they're kept; never their values*

## Repository layout
```
AGENTS.md            standing instructions for any agent
CLAUDE.md            Claude Code entry point (imports AGENTS.md)
STATUS.md            where things stand right now
training-capture/    living record
strategies/          versioned Pine Script (created when needed)
backtests/           backtest settings and summaries (created when needed)
course/              lesson drafts (created when needed)
```

## Source-of-truth rules
- Strategy code lives in `strategies/`, one file per version.
- What happened, and when, lives in `training-capture/`.
- The current state lives in `STATUS.md`.
