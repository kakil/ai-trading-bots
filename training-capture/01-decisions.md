# Decisions

Format for each entry: the decision, why, and what else was considered.

## 2026-11-14: Adopt the training-capture structure

### Decision
Use the same training-capture structure as the Futures Trading Lab repository, adapted for a course.

### Why
That structure already records "what actually happened" in a way that can be audited. For a course, the same record doubles as lesson material.

### Changes from the Futures Trading Lab version
- `04-build-log.md` became `04-session-log.md`, with one short entry per Claude session, so capture happens every time.
- Added `08-backtest-log.md` with required fields, so every backtest can be reproduced.
- Added `09-alerts-and-oversight-log.md`, because alerts and supervision are course topics.
- Added `12-course-map.md` to link captured moments to lessons.
- Added `SESSION-TEMPLATE.md`, a short template that's quicker to fill in than the full phase checkpoint.
- Merged deployment and launch into `10-publishing-log.md`.
- Dropped the commercialization file, because the course is free.
- Added `AGENTS.md` and `CLAUDE.md`, so any agent follows the capture rules automatically and the setup can be reused in new repositories.

### Considered and set aside
- A single long journal file. It would be easier to start, but harder to find backtests, bugs and prompts later.

## 2026-11-14: Hold the README

### Decision
Leave the README as the one-line placeholder for now.

### Why
The person asked to wait on drafting the README.

## 2026-11-14: First bot is Turtle Breakout 55/20 on Bitcoin daily

### Decision
The course builds one bot: *Turtle Breakout 55/20*, long only on Bitcoin's daily chart. The rules are in `02-requirements.md` and `strategies/turtle/SPEC.md`.

### Why
It follows the YouTube course the project is based on. Turtle breakout rules are simple and mechanical, so a beginner can check each trade by hand.

### Considered and set aside
- Long and short. Long only keeps the first bot simpler to check.

## 2026-11-14: Alerts only, with no automated orders

### Decision
The bot sends alerts by app and email. The learner places every trade. Claude gets no broker or API access.

### Why
The learner stays responsible for every trade, which is the center of the oversight module.

## 2026-11-14: Use tradesdontlie/tradingview-mcp as the TradingView MCP

### Decision
Use TradingView MCP Bridge (https://github.com/tradesdontlie/tradingview-mcp) to connect the Claude desktop app to TradingView desktop.

### Why
It's the server the Mind Math Money setup article uses. It's free, open source (MIT), runs locally, can write and compile Pine and read Strategy Tester results, and can't place trades.

### Risks accepted
- It's unofficial and uses TradingView's internal interface, so an update can break it.
- Its disclaimer warns that it may conflict with TradingView's Terms of Use. The course limits use to the learner's own charts, for personal and educational use.
