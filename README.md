# slide-workflow

把凌亂的文件（會議逐字稿、多場會議混檔、實驗／數據報告、論文、財報）變成**可直接上台的設計感簡報**的 Claude skill。

它跟一般「一鍵生成簡報」的工具不同——它先把**內容想清楚、把數據驗算對**，再交給視覺生產：

1. **提煉＋清點** — 回報文件範圍、每個區塊標記去向（上簡報／備援區／另案處理）、**把敏感資料（姓名／薪資／競業條款／個資）攔進備援區**，然後**停下來等你確認**。
2. **風格規格** — 把「有設計感」翻成具體色碼、字體、版型；可從內建的 34 種風格庫挑，或「先給看再選」。
3. **生成** — 單一 HTML、固定 16:9 舞台、不准加料。
4. **圖表驗算** — 所有圖用原始數據實際計算，**畫圖前先重算文件聲稱的統計值**，抓出原文寫錯的數字，標註待核而不擅改、不捏造、不指控。
5. **視覺驗收** — 預期 vs 實際、截圖逐頁核對、只改指定頁。
6. **複盤封裝** — 把整套流程存成可重用 SOP。

設計哲學一句話：**AI 量產，人把關。** 三個裁決權永遠留給人：備援區去留、圖表數字不一致、視覺驗收。

## 安裝

- **Cowork／Claude 桌面版**：在 skill 卡片按 **Save skill**，會安裝到 `~/.claude/skills/slide-workflow/`。
- **手動**：把整個 `slide-workflow/` 資料夾放到 `~/.claude/skills/` 下即可。

裝好後，丟一份檔案說「幫我做成簡報」「把這份報告整理成投影片」就會自動觸發。

## 檔案結構

```
slide-workflow/
├── SKILL.md                      # 主流程（6 步）
├── references/
│   ├── prompts.md                # 6 段可直接貼上的 prompt 模板
│   ├── chart-integrity.md        # 圖表數據驗算紀律（真算、不造假、不指控）
│   └── visual-craft.md           # 版面工藝（節奏、中文字號、圖片比例、預檢、驗收、接力）
├── bold-template-pack/           # 34 種風格設計規格（見下方致謝與授權）
├── CREDITS.md                    # 第三方出處與授權
├── LICENSE                       # 本專案原創部分授權（MIT）
└── README.md
```

## 與其他 deck skill 接力（可選）

本 skill 是「內容＋數據的大腦」，生成這一步可交棒給專做視覺生產的 skill：

- **guizang-ppt-skill** — 深度型，2 種精裝風格（電子雜誌風／瑞士國際主義風）＋驗版腳本。
- **frontend-slides** — 廣度型，30+ 種風格＋固定 16:9 舞台＋PPTX 匯入＋部署 URL／PDF 匯出。

選用建議見 `references/visual-craft.md` 第 10 節。

## 致謝與授權（Acknowledgements）

- 本專案**原創部分**（工作流、`references/`、`SKILL.md`）採 **MIT License**，見 [`LICENSE`](LICENSE)。
- `bold-template-pack/`（34 種風格設計規格）來自 **[frontend-slides](https://github.com/zarazhangrui/frontend-slides)**，作者 **Zara Zhang**，採 MIT License，見 [`bold-template-pack/LICENSE`](bold-template-pack/LICENSE)。這些設計系統的上游為 **[`zarazhangrui/beautiful-html-templates`](https://github.com/zarazhangrui/beautiful-html-templates)**。
- 完整第三方出處與合規說明見 [`CREDITS.md`](CREDITS.md)。
