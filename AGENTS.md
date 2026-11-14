# AGENTS.md: TradingView + Claude development environment

These are standing instructions for any AI coding agent (Claude Code, Codex, Cursor and others) working in this repository.

This file works in two ways:

1. **In this repository**, it tells the agent how to work and how to record what happened.
2. **As a setup file**, you can give it to Claude in a new, empty repository with the words *"Set up this repository using AGENTS.md"*. The agent follows the **Bootstrap** section below to build the same structure there.

`CLAUDE.md` imports this file, so Claude Code reads it automatically.

---

## 1. What this project is

> Edit this section when you reuse the file in another project.

- **Project:** AI Trading Bots, a free no-code course.
- **Goal:** teach beginners to build, test and supervise a TradingView trading bot with Claude, without writing code themselves.
- **Course topics:** the TradingView MCP, 5 rules for bots, the Turtle breakout strategy in Pine Script, backtesting, alerts, and oversight rules.
- **Audience:** people who don't code. Write everything in plain language.
- **The course is the product.** The code, prompts, mistakes and fixes recorded here are raw material for lessons.

## 2. Ground rules

1. **Capture as you go.** Every working session with an agent gets an entry in `training-capture/`. See section 4.
2. **Don't rewrite history.** Failed ideas, bad backtests and wrong turns stay in the record. Write a correction as a new dated entry.
3. **Never claim profit.** Don't write "this strategy makes money," guaranteed returns, or results you haven't verified. A backtest is a simulation, not a promise.
4. **Keep these separate:**
   - one good trade is not a validated strategy;
   - a chart example is not a backtest;
   - a backtest is not live results;
   - paper trading is not live trading.
5. **Humans decide.** A bot is a tool you supervise. Don't let an agent place live orders, connect a funded broker account, or change a running alert unless the person asks for that step in so many words.
6. **No secrets in Git.** That means API keys, webhook URLs that contain tokens, broker or account numbers, TradingView session cookies, and anything from an MCP config that holds credentials. Record *that* a secret exists and where it's kept, never its value.
7. **One change at a time.** Change a strategy in small, versioned steps. Don't mix unrelated changes into one version.
8. **Say what's unverified.** If you couldn't check something (say, a strategy compiled in TradingView), write **UNVERIFIED** and say who needs to check it.

## 3. Repository layout

```
AGENTS.md            standing instructions (this file)
CLAUDE.md            Claude Code entry point; imports AGENTS.md
STATUS.md            one-page "where things stand right now"
training-capture/    the living record of what actually happened
strategies/          Pine Script, one folder per strategy, versioned files  (create when first needed)
backtests/           backtest settings and result summaries                  (create when first needed)
course/              lesson drafts, built from training-capture             (create when first needed)
```

Pine files are named `strategies/<name>/<name>_v<major>.<minor>.<patch>.pine`, for example `strategies/turtle/turtle_v1.0.0.pine`. Keep old versions. Put the version in the script's title so the version showing on the chart can be matched to its file.

## 4. Training capture: what to record and when

### At the start of a session
- Read `STATUS.md` and the newest entry in `training-capture/04-session-log.md`.

### During the session, add to the file that fits

| What happened | Where it goes |
|---|---|
| Any working session | `04-session-log.md` (use `SESSION-TEMPLATE.md`) |
| A decision and why it was made | `01-decisions.md` |
| A prompt that changed the outcome | `05-prompts-used.md` |
| Something broke, and how it was fixed | `06-bugs-and-fixes.md` |
| Compile checks, MCP connection checks, other tests | `07-testing-log.md` |
| Any backtest run | `08-backtest-log.md` (every field filled in) |
| Alerts created or changed, and oversight checks | `09-alerts-and-oversight-log.md` |
| Something published (video, lesson, post) | `10-publishing-log.md` |
| A lesson worth teaching | `11-results-and-lessons.md` |
| A moment that should become course material | `12-course-map.md` |

### At the end of a session
1. Finish the session-log entry: what changed, what was tested, what's still unverified, and what comes next.
2. Update `STATUS.md` if the current version, known-good baseline or next step changed.
3. Add a row to `12-course-map.md` for anything worth teaching.
4. Commit the work and the capture together.

### At the end of a phase
Copy `PHASE-CHECKPOINT-TEMPLATE.md` into the session log and answer every question before marking the phase **CLOSED**.

### Writing style for capture
- Date every entry as `## YYYY-MM-DD: short title`. Newest entries go at the bottom.
- Write plainly. A beginner should be able to follow it.
- Record exact versions, settings and commit SHAs. "It worked" isn't evidence. Record what was checked and how.
- Screenshots go in `training-capture/screenshots/` as `YYYY-MM-DD-short-description.png`. Hide account numbers, balances and personal details first.

## 5. TradingView and Pine Script rules

- Use Pine Script v6 unless there's a recorded reason not to.
- After any Pine change, the person (or the TradingView MCP, if it can) must compile it in TradingView. Record the result in `07-testing-log.md`. Never mark code as working until it compiles.
- Before handing over a changed script, list what changed and what was meant to stay the same.
- Log every backtest in `08-backtest-log.md` with symbol, timeframe, date range, initial capital, order size, commission, slippage, the strategy version, and the results. A backtest you can't reproduce doesn't count.
- Before any alert is turned on, record its condition, the message and where it goes in `09-alerts-and-oversight-log.md`.

## 6. TradingView MCP

- Record which MCP server is used, its version or commit, and how it's connected, in `03-architecture.md`. Leave out secrets.
- If an MCP call fails, log it in `06-bugs-and-fixes.md` with the exact error and the workaround. These are useful teaching moments.
- Ask before using any MCP action that can change a live chart, a saved script or an alert. Reading data doesn't need permission.

## 7. Git

- Work on a branch and open a pull request for anything meaningful.
- When a phase is stable: update training capture, then commit, then record the known-good commit SHA in `STATUS.md`.
- Tag frozen strategy versions, for example `turtle-v1.0.0`.

---

## 8. Bootstrap: set up a new environment from this file

Follow these steps when this file is given to an agent in a repository that doesn't have `training-capture/` yet.

1. **Ask only for what you can't infer:** the project name, its goal, and the main strategies or tools. Fill in section 1 with the answers.
2. **Create the root files:**
   - `AGENTS.md`: a copy of this file, with section 1 updated.
   - `CLAUDE.md`: the single line `@AGENTS.md`, plus any notes that apply only to Claude.
   - `STATUS.md`: project name, date, current phase, current strategy versions (none yet), known-good commit (the setup commit), and next step.
3. **Create `training-capture/`** with these files. Give each a short header that says what it holds, then add the first dated entry where one is noted:

   | File | Holds | First entry |
   |---|---|---|
   | `README.md` | The capture rules from section 4, in short | none |
   | `00-objective-and-constraints.md` | Goal, audience, limits, what success looks like | Fill in from section 1 |
   | `01-decisions.md` | Dated decisions: the decision, why, and the alternatives turned down | "Adopt the training-capture structure" |
   | `02-requirements.md` | What must be built or taught | Fill in from section 1 |
   | `03-architecture.md` | Tools and how they connect (agent, MCP, TradingView, alerts), plus the repo layout | The tool chain as currently known |
   | `04-session-log.md` | One entry per working session | The setup session |
   | `05-prompts-used.md` | Prompts that changed the outcome: prompt, tool, result, and whether to reuse it in the course | The setup prompt |
   | `06-bugs-and-fixes.md` | Attempt, symptom, diagnosis, fix, lesson | none |
   | `07-testing-log.md` | Checklists of what was checked and the PASS / FAIL / UNVERIFIED result | Setup checks |
   | `08-backtest-log.md` | One block per backtest run, with the fields from section 5 | Empty block template |
   | `09-alerts-and-oversight-log.md` | Alerts created or changed, plus regular oversight reviews | Empty block template |
   | `10-publishing-log.md` | What was published, where and when, and whether the link was checked | none |
   | `11-results-and-lessons.md` | Lessons worth keeping or teaching | none |
   | `12-course-map.md` | A table linking captured moments to lessons or modules | Header row only |
   | `SESSION-TEMPLATE.md` | The short per-session template | Copy from this repo |
   | `PHASE-CHECKPOINT-TEMPLATE.md` | The end-of-phase questions | Copy from this repo |
   | `screenshots/README.md` | Naming rule and the reminder to hide personal details | none |
   | `evidence/README.md` | What counts as evidence (compile output, backtest exports, hashes) | none |

4. **Add secret patterns to `.gitignore`:** `.env`, `.env.*`, `*.secret*`, `*.local.json`, and `.claude/settings.local.json`.
5. **Record the setup** in `04-session-log.md` and `07-testing-log.md`, then commit on a branch and open a pull request.
6. **Tell the person** what was created and what still needs their input.

If you can see the source repository (`kakil/ai-trading-bots`), copy the template files from there. If you can't, build them from the table above.
