# Session log

One entry per working session with Claude or another agent. Use `SESSION-TEMPLATE.md`. Newest entries go at the bottom.

---

## 2026-11-14: Set up training capture

**Goal:** Set up the training-capture structure for the course, based on the Futures Trading Lab repository.

**What we did**
- Reviewed `training-capture/` in the Futures Trading Lab repo.
- Created `AGENTS.md`, `CLAUDE.md`, `STATUS.md` and this folder, adapted for the course.
- Added a Bootstrap section to `AGENTS.md`, so the setup can be repeated in new TradingView repositories.

**Tools:** Claude Code, GitHub

**Tested**
- [x] All files listed in `README.md` exist
- [ ] Claude Code loads `AGENTS.md` through `CLAUDE.md` in a fresh session: **UNVERIFIED**

**Unverified or open:** the TradingView MCP server details aren't chosen yet.

**Course moments:** "Set up your project so Claude remembers the rules" (see `12-course-map.md`).

**Next:** Choose and connect the TradingView MCP, then record it in `03-architecture.md`.

---

## 2026-11-14: Fill in the 5 rules and course map

**Goal:** Turn the course plan into concrete rules and modules.

**What we did**
- Used the YouTube course transcript, without its promotional material, to set the course flow.
- Filled in the 5 rules for Turtle Breakout 55/20 and the oversight rules in `02-requirements.md`.
- Wrote the strategy spec in `strategies/turtle/SPEC.md`.
- Mapped the 9 modules in `12-course-map.md`.
- Added the apps and plans to `03-architecture.md`.

**Tools:** Claude Code, GitHub

**Tested**
- [ ] Rules checked against TradingView: **UNVERIFIED**. No Pine code exists yet.

**Unverified or open:** the TradingView MCP server isn't chosen yet. Pine details to decide when building: whether "previous 55 days" excludes today's bar (the spec says it does), and how the 1% size is rounded for Bitcoin.

**Course moments:** "Write the 5 rules before asking Claude to build" (module 3).

**Next:** Connect the TradingView MCP, then have Claude write Turtle Breakout 55/20 v1.0.0.
