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
