# slide-workflow

把凌亂的文件（會議逐字稿、多場會議混檔、實驗／數據報告、論文、財報）變成**可直接上台的設計感簡報**的 Claude skill。

A Claude skill that transforms messy documents — meeting transcripts, multi-meeting dumps, experiment/data reports, papers, financial statements — into **presentation-ready, design-quality slides**.

它跟一般「一鍵生成簡報」的工具不同——它先把**內容想清楚、把數據驗算對**，再交給視覺生產：

Unlike typical "one-click slide generators," this skill **thinks through the content first and verifies the numbers**, then hands off to visual production:

1. **提煉＋清點 / Distill + Inventory** — 回報文件範圍、每個區塊標記去向、**把敏感資料攔進備援區**，然後**停下來等你確認**；若你帶著自己的大綱來，切換為**診斷模式**：找漏洞、查邏輯、不直接生產。Reports scope, tags every section, intercepts sensitive data, then **stops and waits for your confirmation**. If you bring your own outline, switches to **critique mode**: finds gaps and logic issues instead of producing.
2. **風格規格 / Style Specification** — 把「有設計感」翻成具體色碼、字體、版型；可從內建 34 種風格庫挑，或「先給看再選」。Translates "make it look designed" into hex codes, fonts, and layouts.
3. **生成 / Generate** — 單一 HTML、固定 16:9 舞台、不准加料。Single HTML file, fixed 16:9 stage, no improvising.
4. **圖表驗算 / Chart Verification** — 所有圖用原始數據實際計算，**畫圖前先重算文件聲稱的統計值**，抓出原文錯誤，標註待核。Re-computes every claimed statistic before drawing; flags discrepancies without guessing or inventing.
5. **視覺驗收 / Visual QA** — 預期 vs 實際、截圖逐頁核對、只改指定頁。Expected vs. actual, screenshot-by-screenshot, only the specified pages get touched.
6. **複盤封裝 / Retrospective Packaging** — 把整套流程存成可重用 SOP。Saves the entire workflow as a reusable SOP.

設計哲學：**AI 量產，人把關**；也可以**人做判斷，AI 找問題**。不要外包大腦給 AI——你整理大綱、AI 診斷缺口，比讓 AI 猜你要說什麼有效得多。三個裁決權永遠在人：備援區去留、圖表數字不一致、視覺驗收。

Design philosophy: **AI produces, humans decide** — or flip it: **you lead the thinking, AI finds the gaps.** Don't outsource your brain. Bring your own outline; let AI diagnose what's missing or unclear. Either way, three decisions always stay with you: reserve area, chart discrepancies, visual sign-off.

---

## 安裝 / Installation

### 方法 A — 一鍵安裝（推薦）/ Option A — One-click (recommended)

1. 前往 [Releases 頁面](https://github.com/Yu-0312/ppt-creater/releases/latest) / Go to the [Releases page](https://github.com/Yu-0312/ppt-creater/releases/latest)
2. 下載 `ppt-creater.skill` / Download `ppt-creater.skill`
3. 雙擊檔案，Claude Desktop 自動安裝 / Double-click — Claude Desktop installs it automatically

### 方法 B — Git Clone

開啟終端機，執行 / Open Terminal and run:

```bash
git clone https://github.com/Yu-0312/ppt-creater.git ~/.claude/skills/slide-workflow
```

> 日後更新 / To update later: `cd ~/.claude/skills/slide-workflow && git pull`

### 方法 C — 下載 ZIP / Download ZIP (no Git required)

1. 點擊頁面上的綠色 **Code** 按鈕 → **Download ZIP** / Click the green **Code** button → **Download ZIP**
2. 解壓縮，將資料夾重命名為 `slide-workflow` / Unzip and rename the folder to `slide-workflow`
3. 移動到 skills 資料夾 / Move to the skills folder:

```bash
mv ~/Downloads/ppt-creater-main ~/.claude/skills/slide-workflow
```

### 確認安裝 / Verify installation

重新啟動 Claude Desktop，丟入任意文件說：/ Restart Claude Desktop, drop in a document and say:

> 「幫我做成簡報」 / "Turn this into slides."

---

## 檔案結構 / File Structure

```
slide-workflow/
├── SKILL.md                      # 主流程（6 步）/ Main workflow (6 steps)
├── references/
│   ├── prompts.md                # 6 段 prompt 模板 / 6 ready-to-paste prompt templates
│   ├── chart-integrity.md        # 圖表驗算紀律 / Chart data verification rules
│   └── visual-craft.md           # 版面工藝 / Visual craft
├── bold-template-pack/           # 34 種風格設計規格 / 34 style design specs
├── CREDITS.md                    # 第三方授權 / Third-party attribution
├── LICENSE                       # MIT License
└── README.md
```

## 與其他 Deck Skill 接力 / Chaining with Other Deck Skills (Optional)

本 skill 是「內容＋數據的大腦」，生成這一步可交棒給專做視覺生產的 skill。
This skill is the **content + data brain**. The generation step can hand off to a visual production skill:

- **guizang-ppt-skill** — 深度型，2 種精裝風格（電子雜誌風／瑞士國際主義風）＋驗版腳本。Depth-focused: 2 refined styles + verification script.
- **frontend-slides** — 廣度型，30+ 種風格＋16:9 舞台＋PPTX 匯入＋部署 URL／PDF 匯出。Breadth-focused: 30+ styles + PPTX import + deploy URL / PDF export.

## 致謝與授權 / Acknowledgements

- 本專案**原創部分**採 **MIT License**，見 [`LICENSE`](LICENSE)。The **original work** is released under the **MIT License**.
- `bold-template-pack/` 來自 **[frontend-slides](https://github.com/zarazhangrui/frontend-slides)**，作者 **Zara Zhang**，MIT License，見 [`bold-template-pack/LICENSE`](bold-template-pack/LICENSE)。上游為 **[`zarazhangrui/beautiful-html-templates`](https://github.com/zarazhangrui/beautiful-html-templates)**。
- 完整說明見 [`CREDITS.md`](CREDITS.md)。Full third-party attribution: [`CREDITS.md`](CREDITS.md).
