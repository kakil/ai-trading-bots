# Testing log

Record what was checked, how, and the result: **PASS**, **FAIL** or **UNVERIFIED**.

Typical checks:
- Pine Script compiles in TradingView (version, any warnings)
- The strategy loads on the chart and the Strategy Tester shows results
- TradingView MCP connects, and each tool used responds
- An alert fires on its condition and delivers its message

---

## 2026-11-14: Repository setup

- [x] Training-capture files created
- [x] `AGENTS.md`, `CLAUDE.md` and `STATUS.md` created
- [x] Secret patterns added to `.gitignore`
- [ ] Fresh Claude Code session picks up `CLAUDE.md` → `AGENTS.md`: **UNVERIFIED**

**Result:** PASS for the file structure. One check still UNVERIFIED.
