# Status

**Project:** AI Trading Bots, a free no-code course
**Updated:** 2026-11-14
**Phase:** Planning: rules defined, no code yet

## Current state
- Training-capture structure and agent instructions (`AGENTS.md`, `CLAUDE.md`) are in place.
- README is on hold.
- The 5 rules, the oversight rules and the course map are written (`training-capture/02-requirements.md`, `training-capture/12-course-map.md`).
- Strategy spec: `strategies/turtle/SPEC.md` (Turtle Breakout 55/20, spec v1.0.0).
- TradingView MCP chosen: tradesdontlie/tradingview-mcp. Setup guide in `setup/TRADINGVIEW-MCP-SETUP.md`. Connection not tested yet.
- No Pine code, backtests or alerts yet.

## Strategy versions
- Turtle Breakout 55/20: spec v1.0.0, not built yet

## Known-good baseline
`650467a` (merge of PR #2: rules, spec and course map)

## Next step
Install the TradingView MCP using `setup/TRADINGVIEW-MCP-SETUP.md`, pass `tv_health_check` and log it, then build Turtle Breakout 55/20 v1.0.0.
