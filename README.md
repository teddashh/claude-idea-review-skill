# Claude Idea Review Skill / Claude 點子驗證 Skill

Open-source Claude Code skill for the **Personal IP Co-Building / Coaching Program** and the **「自由工坊」Discord community**.

License: MIT.

This repo is for people who have an idea and want a structured AI review before spending serious time building it. Use it when you want to validate a product, content, startup, feature, creator-IP, community, or business idea.

本 repo 是 **個人 IP 陪跑計畫** / **「自由工坊」Discord 社群** 的開源 Claude Code skill。

授權：MIT。

當你有一個 idea 想驗證，不確定該不該做、怎麼做、風險在哪、第一步要測什麼，可以使用這個 tool。它適合驗證產品、內容、創業、功能、個人品牌、社群、商業模式等 idea。

## What It Does / 它會做什麼

The skill runs a 5 / 12 / 16-round review panel inside Claude Code. It first checks whether Codex CLI, Antigravity/Gemini, and Grok/xAI are available. It uses native providers when available, asks once for missing API keys when needed, and falls back to Claude simulation when a provider is unavailable.

這個 skill 會在 Claude Code 裡跑 5 / 12 / 16 輪 review。開始前會先檢查 Codex CLI、Antigravity/Gemini、Grok/xAI 是否可用。有原生 provider 就用原生 provider；沒有時會問一次是否有 API key；如果仍不可用，就用 Claude 模擬。

It also does web research first when tools are available, so the review starts with current competitor, market, pricing, feasibility, and policy context.

如果工具可用，它會先查網路資料，讓 review 一開始就有目前競品、市場、價格、可行性、政策限制等背景。

## Personalities / 四種思考個性

These are thinking personalities, not departments or identity claims:

- `Optimist`: expands the strongest possible version of the idea.
- `Skeptic`: attacks weak assumptions and hidden risks.
- `Pragmatist`: turns the debate into tests, MVP shape, constraints, and tradeoffs.
- `Synthesizer`: integrates disagreement and tracks what evidence would change the conclusion.

這四個是思考個性，不是職務角色，也不是宣稱真的有四個模型：

- `Optimist`：把 idea 的最強版本展開。
- `Skeptic`：攻擊弱假設與隱藏風險。
- `Pragmatist`：把討論變成測試、MVP、限制與取捨。
- `Synthesizer`：整合分歧，追蹤什麼證據會改變結論。

## Outputs / 輸出

The skill saves a local review workspace:

```text
.idea-review/<slug>/
├── input.md
├── rounds/
│   ├── round-01.md
│   └── ...
├── final.md
├── report.md
└── report.html
```

Skill 會保存本地 review workspace：

```text
.idea-review/<slug>/
├── input.md
├── rounds/
│   ├── round-01.md
│   └── ...
├── final.md
├── report.md
└── report.html
```

`report.html` is a static printable report. Open it in a browser and use the Print / Save PDF button. `report.md` is the full Markdown version.

`report.html` 是靜態可列印報告。用瀏覽器打開後，可以按 Print / Save PDF。`report.md` 是完整 Markdown 版本。

## Requirements / 需求

- **Claude Code** — the review panel runs inside it.
- **Python 3.8+** on your `PATH` — only the helper scripts use it (workspace scaffold + report rendering). The review reasoning itself runs in Claude, so Python is not needed for the analysis.
- **Optional providers** for multi-model cross-checking: Codex CLI, Gemini CLI, and/or Grok CLI. None are required — if a provider is missing, the skill runs fully on Claude and simulates it.

需求：

- **Claude Code** — review panel 在它裡面跑。
- **Python 3.8+**（要在 `PATH` 上）— 只有輔助 scripts 會用到（建立 workspace、產生報告）。實際 review 推理是 Claude 在做，所以分析本身不需要 Python。
- **選用 provider**（多模型交叉驗證）：Codex CLI、Gemini CLI、Grok CLI。都不是必要的；缺哪個，skill 就用 Claude 模擬該 provider 照樣跑完。

## Install / 安裝

Install as a personal Claude Code skill by cloning into your skills directory:

把這個 repo clone 到 Claude Code 的 skills 目錄，當作個人 skill 安裝：

```bash
# macOS / Linux
git clone https://github.com/teddashh/claude-idea-review-skill.git \
  ~/.claude/skills/idea-review-panel
```

```powershell
# Windows (PowerShell)
git clone https://github.com/teddashh/claude-idea-review-skill.git `
  "$env:USERPROFILE\.claude\skills\idea-review-panel"
```

Then **restart Claude Code** (or start a new session). Skills are loaded at startup, so a session that was already running will not see a newly added skill.

然後**重啟 Claude Code**（或開新 session）。Skills 只在啟動時載入，所以還在跑的舊 session 不會看到剛裝好的 skill。

To use it inside one project instead of globally, clone into that project's `.claude/skills/idea-review-panel/` directory.

如果只想在某個專案裡用、不想全域安裝，就 clone 到該專案的 `.claude/skills/idea-review-panel/` 底下。

Update later with:

之後更新：

```bash
git -C ~/.claude/skills/idea-review-panel pull
```

> **Windows note:** the helper scripts call `python3`, but on Windows the command is usually `python`. If typing `python` opens the Microsoft Store, that is the placeholder alias, not a real interpreter — install Python from [python.org](https://www.python.org/downloads/) or run `winget install Python.Python.3.12`, then reopen your terminal.
>
> **Windows 提醒：** 輔助 scripts 用 `python3`，但 Windows 上通常是 `python`。如果打 `python` 跳出 Microsoft Store，那是佔位捷徑、不是真的 Python — 請從 [python.org](https://www.python.org/downloads/) 安裝，或執行 `winget install Python.Python.3.12`，然後重開終端機。

## Usage / 怎麼用

After restarting, just ask Claude Code to validate an idea — the skill triggers from its description:

重啟後，直接請 Claude Code 驗證一個 idea，skill 會依描述自動觸發：

```text
幫我驗證這個點子：<你的 idea>
```

Default is 5 rounds; ask for 12 or 16 for deeper analysis. The review workspace is saved under `.idea-review/<slug>/` in your current working directory.

預設 5 輪；想更深入可以要求 12 或 16 輪。Review workspace 會存在目前工作目錄的 `.idea-review/<slug>/` 底下。

## Helper Scripts / 輔助 scripts

The skill runs these for you; you can also run them manually (use `python` instead of `python3` on Windows).

Skill 會自動幫你跑這些；你也可以手動執行（Windows 上把 `python3` 換成 `python`）。

Check providers:

檢查 provider：

```bash
python3 scripts/check_providers.py --smoke
```

Create a review workspace:

建立 review workspace：

```bash
python3 scripts/init_review.py --idea "your idea" --rounds 5
```

Render reports:

產生報告：

```bash
python3 scripts/render_report.py .idea-review/<slug>
```

## Final Verdict Format / 最終結論格式

`final.md` includes:

- Verdict: `worth_building`, `validate_first`, `pivot`, or `not_worth_building`
- Confidence: 0-100
- One-line conclusion
- Strongest reason
- Strongest counterargument
- Two-week validation plan
- Success threshold
- Kill criterion
- Next 3 actions

`final.md` 會包含：

- Verdict：`worth_building`, `validate_first`, `pivot`, 或 `not_worth_building`
- Confidence：0-100
- 一句話結論
- 最強理由
- 最強反論點
- 兩週驗證計畫
- 成功門檻
- 停止條件
- 下一步三件事
