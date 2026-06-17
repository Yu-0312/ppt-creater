# slide-workflow

把凌亂的文件（會議逐字稿、多場會議混檔、實驗／數據報告、論文、財報）變成**可直接上台的設計感簡報**的 Claude skill。

A Claude skill that transforms messy documents — meeting transcripts, multi-meeting dumps, experiment/data reports, papers, financial statements — into **presentation-ready, design-quality slides**.

它跟一般「一鍵生成簡報」工具不同——它**先一次問完所有設定**，再**一層一層地**把內容想清楚、把數據驗算對，最後交給視覺生產：

Unlike typical "one-click slide generators," this skill starts by **collecting all your preferences upfront in a single message**, then proceeds layer by layer — content first, then design spec, then generation:

0. **預設問卷 / Upfront Config** — 一次問完所有設定（素材來源、受眾、尺寸、品牌資產、版型偏好），**填完就一路跑到底**。Collects all settings in one message — audience, canvas format, brand assets, and more — before any work begins.
1. **提煉＋清點 / Distill + Inventory** — 回報文件範圍、每個區塊標記去向、**把敏感資料攔進備援區**，然後**停下來等你確認**；若你帶著自己的大綱來，切換為**診斷模式**：找漏洞、查邏輯、不直接生產。Reports scope, tags every section, intercepts sensitive data, then **stops and waits for your confirmation**. If you bring your own outline, switches to **critique mode**: finds gaps and logic issues instead of producing.
2. **模板選擇 / Template Selection** — 根據你的內容與場合，從 **34 種風格模板庫**篩出 3–5 個候選，⛔ 等你挑選後再進配色。Shortlists 3–5 templates from a **34-style library** based on your content and context — stops and waits for your pick before proceeding to color.
3. **風格規格 / Style Specification** — 把「有設計感」翻成具體色碼、字體、版型；套入選定模板；若有品牌資產則先擷取品牌色。Translates "make it look designed" into hex codes, fonts, and layouts — applied on top of your chosen template, with brand color extraction if you have brand assets.
4. **生成 / Generate** — 單一 HTML、對應 Canvas 格式、不准加料。Single HTML file, matching canvas format (16:9 / 4:3 / 9:16 / A4), no improvising.
5. **圖表驗算 / Chart Verification** — 所有圖用原始數據實際計算，**畫圖前先重算文件聲稱的統計值**，抓出原文錯誤，標註待核。Re-computes every claimed statistic before drawing; flags discrepancies without guessing or inventing.
6. **視覺驗收 / Visual QA** — 預期 vs 實際、截圖逐頁核對、只改指定頁。Expected vs. actual, screenshot-by-screenshot, only the specified pages get touched.
7. **複盤封裝 / Retrospective Packaging** — 把整套流程存成可重用 SOP。Saves the entire workflow as a reusable SOP.

設計哲學：**AI 量產，人把關**；也可以**人做判斷，AI 找問題**。不要外包大腦給 AI——你整理大綱、AI 診斷缺口，比讓 AI 猜你要說什麼有效得多。三個裁決權永遠在人：備援區去留、模板選擇、圖表數字不一致。

Design philosophy: **AI produces, humans decide** — or flip it: **you lead the thinking, AI finds the gaps.** Don't outsource your brain. Bring your own outline; let AI diagnose what's missing or unclear. Either way, three decisions always stay with you: reserve area, template pick, chart discrepancies.

---

## 安裝 / Installation

### 方法 A — 終端一步安裝（最快）/ Option A — One-line Terminal Install (fastest)

不需要 Git，直接貼進終端機執行 / No Git required — paste and run in Terminal:

```bash
curl -L https://github.com/Yu-0312/ppt-creater/archive/refs/heads/main.zip -o /tmp/slide-workflow.zip \
  && unzip -q /tmp/slide-workflow.zip -d /tmp \
  && mkdir -p ~/.claude/skills \
  && mv /tmp/ppt-creater-main ~/.claude/skills/slide-workflow \
  && rm /tmp/slide-workflow.zip \
  && echo "✅ 安裝完成 / Installed successfully"
```

> 日後更新：重新執行以上指令即可（會覆蓋舊版）/ To update: re-run the same command.

---

### 方法 B — 直接下載 ZIP / Option B — Direct ZIP Download

**👉 [點這裡下載最新版 ZIP](https://github.com/Yu-0312/ppt-creater/archive/refs/heads/main.zip)**

下載後 / After downloading:

```bash
unzip ~/Downloads/ppt-creater-main.zip -d ~/Downloads \
  && mkdir -p ~/.claude/skills \
  && mv ~/Downloads/ppt-creater-main ~/.claude/skills/slide-workflow
```

---

### 方法 C — Git Clone（想追蹤更新）/ Option C — Git Clone (stay in sync)

```bash
git clone https://github.com/Yu-0312/ppt-creater.git ~/.claude/skills/slide-workflow
```

> 日後更新 / To update later: `cd ~/.claude/skills/slide-workflow && git pull`

---

### 確認安裝 / Verify installation

重新啟動 Claude Desktop，丟入任意文件說：/ Restart Claude Desktop, drop in a document and say:

> 「幫我做成簡報」 / "Turn this into slides."

---

## 流程總覽 / Workflow Overview

| 步 / Step | 做什麼 / What | 人工裁決 / Human Decision |
|---|---|---|
| **0** | 預設問卷：一次問完素材、受眾、格式、品牌、設計偏好 | ✅ 全部功能開關 |
| 前置 | 路徑分流（有素材 / 主題研究 / 跨 session 銜接）| — |
| **1** | 提煉＋清點 → ⛔ 停下確認範圍與備援區 | ✅ 備援區去留 |
| **2** | 模板選擇：從 34 種風格篩出 3–5 候選 → ⛔ 等你選 | ✅ 使用者挑模板 |
| **3** | 風格規格（套入模板；品牌色擷取；Refine Spec opt-in）| ✅ Refine Spec（opt-in）|
| **4** | 生成（單一 HTML，Canvas 格式對應 Step 0 設定）| — |
| **5** | 圖表驗算（原始數據繪製、重算統計值、抓錯標註）| ✅ 重大數字差異 |
| **6** | 視覺驗收（預期 vs 實際、截圖逐頁核對）| ✅ |
| **7** | 複盤封裝（整理成可重用 SOP）| — |

---

## 檔案結構 / File Structure

```
slide-workflow/
├── SKILL.md                      # 主流程（Step 0–7）/ Main workflow (Step 0–7)
├── references/
│   ├── prompts.md                # 各步 prompt 模板 / Ready-to-paste prompt templates
│   ├── chart-integrity.md        # 圖表驗算紀律 / Chart data verification rules
│   └── visual-craft.md           # 版面工藝 / Visual craft
├── bold-template-pack/           # 34 種風格設計規格 / 34 style design specs
├── CREDITS.md                    # 第三方授權 / Third-party attribution
├── LICENSE                       # MIT License
└── README.md
```

---

## 與其他 Deck Skill 接力 / Chaining with Other Deck Skills (Optional)

本 skill 是「內容＋數據的大腦」，生成這一步可交棒給專做視覺生產的 skill。
This skill is the **content + data brain**. The generation step can hand off to a visual production skill:

- **guizang-ppt-skill** — 深度型，2 種精裝風格（電子雜誌風／瑞士國際主義風）＋驗版腳本。Depth-focused: 2 refined styles + verification script.
- **frontend-slides** — 廣度型，30+ 種風格＋16:9 舞台＋PPTX 匯入＋部署 URL／PDF 匯出。Breadth-focused: 30+ styles + PPTX import + deploy URL / PDF export.

---

## 致謝與授權 / Acknowledgements

- 本專案**原創部分**採 **MIT License**，見 [`LICENSE`](LICENSE)。The **original work** is released under the **MIT License**.
- `bold-template-pack/` 來自 **[frontend-slides](https://github.com/zarazhangrui/frontend-slides)**，作者 **Zara Zhang**，MIT License，見 [`bold-template-pack/LICENSE`](bold-template-pack/LICENSE)。上游為 **[`zarazhangrui/beautiful-html-templates`](https://github.com/zarazhangrui/beautiful-html-templates)**。
- 部分工作流設計概念（主題研究前置、執行紀律標記、品牌擷取）參考並改寫自 **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)**（MIT License，Copyright © 2025–2026 Hugo He）。
- 完整說明見 [`CREDITS.md`](CREDITS.md)。Full third-party attribution: [`CREDITS.md`](CREDITS.md).
