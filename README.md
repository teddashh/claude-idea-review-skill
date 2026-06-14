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

## Install / 安裝

Use this repo as a Claude Code skill package. The root contains `SKILL.md`, so you can copy or zip this repo directory as the skill.

這個 repo 本身就是 Claude Code skill package。root 有 `SKILL.md`，所以可以直接 copy 或 zip 這個 repo 資料夾作為 skill。

## Helper Scripts / 輔助 scripts

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
