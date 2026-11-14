# Connect Claude to TradingView (TradingView MCP)

This guide covers setting up the bridge that lets Claude read and control your TradingView desktop chart. You don't need to write any code. Claude can walk you through every step.

**Sources:**
- The Mind Math Money article "How to connect Claude to TradingView, step by step, no coding required" (updated 2026-07-02).
- The MCP's own README, checked on 2026-11-14.

---

## What the TradingView MCP is

- **Name:** TradingView MCP Bridge (`tradingview-mcp`)
- **Official repo:** https://github.com/tradesdontlie/tradingview-mcp
- **Author:** GitHub user `tradesdontlie`
- **License:** MIT
- **Version checked:** package `1.0.0`, commit `c05b8f5755ed8e64ea242de88ddbf46aa24d56a4` (2026-07-28)
- **Made by TradingView or Anthropic?** No. It's an unofficial community tool.

### How it works
```
Claude desktop ←→ MCP server (node, on your computer) ←→ debug port 9222 ←→ TradingView desktop
```
It talks only to the TradingView app running on your own computer, through Chromium's standard debugging port. It doesn't connect to TradingView's servers, and your TradingView login isn't shared with Claude.

### What it can do
It has 84 tools at the version checked. The ones this course uses:

| Course step | Tools |
|---|---|
| Check the connection | `tv_health_check`, `tv_launch` |
| Read the chart | `chart_get_state`, `quote_get`, `data_get_ohlcv` |
| Switch to Bitcoin daily | `chart_set_symbol`, `chart_set_timeframe` |
| Build the Pine strategy | `pine_new`, `pine_set_source`, `pine_smart_compile`, `pine_get_errors` |
| Check trades and backtest results | `data_get_strategy_results`, `data_get_trades`, `data_get_equity`, `capture_screenshot` (Strategy Tester region) |
| Check trades by hand | `chart_scroll_to_date`, `replay_start`, `replay_step` |
| Alerts | `alert_list`, `alert_create`, `alert_delete` (price alerts only) |

### What it can't do
- **Place real trades.** It has no broker access. (`replay_trade` only works in TradingView's practice replay mode.)
- **Work in the browser version** of TradingView or Claude. Both desktop apps are needed.
- **Stay stable through every TradingView update.** It uses TradingView's internal interface, which can change without notice. If it breaks after an update, check the repo for a fix.

---

## What you need

| Item | Notes |
|---|---|
| **TradingView desktop app** | https://www.tradingview.com/desktop/. A paid plan is required. The course uses Essential or higher, because technical alerts need it. |
| **Claude desktop app** | https://claude.ai/download (Windows or Mac). The browser version can't connect to local tools. |
| **Node.js 18 or newer** | https://nodejs.org. Install the LTS version with the default options. |
| **Time** | About 15 to 30 minutes |

Windows, Mac and Linux are supported. This guide covers Windows and Mac.

---

## Setup steps

> **Easiest path:** open a new conversation in Claude desktop and say: *"Walk me through installing the TradingView MCP from https://github.com/tradesdontlie/tradingview-mcp, one step at a time. I'm on [Windows / Mac]."* Then follow along with the steps below.

### 1. Check Node.js
Open **Command Prompt** (Windows) or **Terminal** (Mac) and run:
```
node -v
```
If you see a version number of 18 or higher, you're set. If you get "not recognized," install Node.js LTS, then **close and reopen** the terminal.

### 2. Download the MCP
On the [GitHub repo](https://github.com/tradesdontlie/tradingview-mcp), click the green **Code** button, then **Download ZIP**, and extract it.

The ZIP often puts one folder inside another. Use the folder that directly contains `package.json` and a `src` folder. Copy that folder's full path, because you'll need it in step 5.

*(If you have Git, `git clone https://github.com/tradesdontlie/tradingview-mcp.git` works too.)*

### 3. Install it
In the terminal, go to that folder and install:
```
cd "<path to the folder>"
npm install
```
Vulnerability warnings during install are normal. **Don't** run `npm audit fix`.

### 4. Start TradingView with the debug port
Fully close TradingView first, including from the system tray (Windows) or the Dock (Mac). Then start it like this:

- **Windows:**
  ```
  "%LOCALAPPDATA%\TradingView\TradingView.exe" --remote-debugging-port=9222
  ```
  If that says the path wasn't found (common with Microsoft Store installs), run:
  ```
  powershell -c "Get-AppxPackage *trading* | Select-Object Name, InstallLocation"
  ```
  Then use `"<InstallLocation>\TradingView.exe" --remote-debugging-port=9222`.
- **Mac:**
  ```
  open -a TradingView --args --remote-debugging-port=9222
  ```
- **Or use the launch script** in the MCP folder: `scripts\launch_tv_debug.bat` (Windows) or `./scripts/launch_tv_debug_mac.sh` (Mac).

Sign in and **open a real chart**, not the welcome tab. You need to start TradingView this way every time you want Claude connected, so a launcher script saves time.

### 5. Add the MCP to Claude desktop
In Claude desktop, go to **Settings → Developer → Edit Config**. This opens `claude_desktop_config.json`. Add the `tradingview` entry:

```json
{
  "mcpServers": {
    "tradingview": {
      "command": "node",
      "args": ["<full path to the folder from step 2>/src/server.js"]
    }
  }
}
```

- **Windows:** use double backslashes in the path, for example `"C:\\Users\\you\\tradingview-mcp\\src\\server.js"`.
- **If the file already has content,** add `tradingview` inside the existing `mcpServers` block rather than replacing the file.

*(Claude Code users: put the same block in `~/.claude/.mcp.json` or a project `.mcp.json` instead. Don't commit a config that holds secrets.)*

### 6. Restart Claude
Fully quit Claude. On Windows, quit from the system tray, because closing the window isn't enough. Then reopen it. **Settings → Developer** should now list a server named **tradingview**.

### 7. Check the connection
In a **new** conversation, ask:
> Run tv_health_check and tell me if TradingView is connected.

Success looks like `cdp_connected: true` and `api_available: true`. Then ask: *"What symbol and price is on my chart?"*

Record the result in `training-capture/07-testing-log.md`.

---

## Troubleshooting

| Problem | Likely cause and fix |
|---|---|
| `npm is not recognized` | Node.js isn't installed, or the terminal was opened before installing it. Reopen the terminal. |
| `Could not read package.json` | Wrong folder, usually the outer folder of the ZIP. Go one level in. |
| `The system cannot find the path specified` (Windows) | It's a Microsoft Store install. Use the `Get-AppxPackage` command from step 4. |
| `tradingview` missing in Claude's Developer settings | Claude wasn't fully quit, or there's a typo in the JSON (a missing comma or single backslashes). |
| `tv_health_check` fails | TradingView wasn't started with `--remote-debugging-port=9222`, or no chart tab is open. |
| Worked before, broke after a TradingView update | TradingView's internal interface changed. Check the repo for an update. |

---

## Safety rules (these follow the course's oversight rules)

1. **Debug mode stays on your computer.** While TradingView runs with port 9222 open, any program on your computer can control it. Never expose port 9222 to your network or the internet, and close TradingView when you're done.
2. **Claude never gets broker or API access.** The MCP can't trade, and the course never connects it to anything that can.
3. **Ask before changes.** Claude should ask before it saves scripts (`pine_save`), creates or deletes alerts, or uses UI automation (`ui_click`, `ui_evaluate`). Reading the chart is fine without asking.
4. **Don't run commands you don't understand.** If Claude suggests deleting files or changing anything unrelated to this setup, stop and ask.
5. **TradingView's terms.** The MCP's own disclaimer says programmatic use of TradingView may conflict with TradingView's Terms of Use, which restrict automated data collection. Use it only on your own charts, for personal and educational use, and don't redistribute data.
6. **Education only.** None of this is financial advice.
