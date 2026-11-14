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
