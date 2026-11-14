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
- **Server:** TradingView MCP Bridge (`tradingview-mcp`), https://github.com/tradesdontlie/tradingview-mcp. MIT license, unofficial (not made by TradingView or Anthropic).
- **Version checked:** package 1.0.0, commit `c05b8f5755ed8e64ea242de88ddbf46aa24d56a4` (2026-07-28). Record the commit you actually install.
- **Needs:** Node.js 18+, TradingView desktop started with `--remote-debugging-port=9222`, and a chart open.
- **How it connects:** Claude desktop runs `node <folder>/src/server.js` (set up in `claude_desktop_config.json` under `mcpServers.tradingview`), and that talks to TradingView over the local debug port.
- **What it can do:** 84 tools covering reading the chart, changing symbol and timeframe, writing and compiling Pine, reading Strategy Tester results and trades, replay, drawings, price alerts, screenshots and UI automation. It can't place real trades.
- **Secrets:** none needed. The config holds only a file path, and your TradingView login stays in the app.
- **Risks:** it uses TradingView's internal interface, so it can break after an update. Port 9222 must stay local. The MCP's disclaimer warns that programmatic use may conflict with TradingView's Terms of Use.
- **Setup guide:** `setup/TRADINGVIEW-MCP-SETUP.md`

## Repository layout
```
AGENTS.md            standing instructions for any agent
CLAUDE.md            Claude Code entry point (imports AGENTS.md)
STATUS.md            where things stand right now
setup/               setup guides (TradingView MCP)
training-capture/    living record
strategies/          versioned Pine Script (created when needed)
backtests/           backtest settings and summaries (created when needed)
course/              lesson drafts (created when needed)
```

## Source-of-truth rules
- Strategy code lives in `strategies/`, one file per version.
- What happened, and when, lives in `training-capture/`.
- The current state lives in `STATUS.md`.
