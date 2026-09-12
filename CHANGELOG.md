# Changelog

本專案遵循 [Keep a Changelog](https://keepachangelog.com/) 格式。

## [0.2.0] - 2026-09-12

### Added

- `.claude-plugin/marketplace.json` 與 `.claude-plugin/plugin.json`，支援以 Claude Code Plugin Marketplace 安裝：`claude plugin marketplace add kirinlin/tw-writing` 後 `claude plugin install tw-writing@tw-writing`。
- README 新增 `npx skills add kirinlin/tw-writing` 安裝方式，支援任何 Skill-aware Agent（Codex、opencode、Cursor 等）。

### Changed

- README 安裝章節依管道拆分為 Plugin Marketplace、`npx skills add`、手動 Clone 三個小節。
- CLAUDE.md 補充三種安裝管道皆要求 `SKILL.md` 位於 repo 根目錄的限制，避免未來誤將檔案移入 `skills/` 子目錄。

## [0.1.0] - 2026-08-26

### Added

- 繁體中文寫作規範 `SKILL.md`，共 29 節，以 The Elements of Style 為基礎本地化。
- 台灣用語規範（§11）：中國大陸用語對照、同形異義詞、教育部標準字體用字、全形與半形。
- 台灣用語完整對照表 `references/taiwan-terms.md`，涵蓋作業系統、網路、程式語言、資料結構、資料庫、UI、維運、資安、AI 與影音領域，並提供 ripgrep 審查指令。
- AI 生成腔調反模式（§21.4）：空泛開場、空泛收尾、插入語與結構性贅述。
- 中文語法特有規則（§10）：條件在前結論在後、連接詞與頓號、「或」的歧義、量詞、英文直譯腔對照表。
- 修飾範圍歧義的判斷與改寫方式（§3.6）。
- 雙重否定改寫（§6.3）與不確定性標示（§7.3）。
- 標點符號完整規範（§14）：頓號、引號、書名號、括號、破折號、刪節號、列表結尾標點。
- Markdown 與版面規範（§15）：標題、列表、表格、連結、程式碼區塊、強調。
- 語氣與稱謂規範（§20）。
- 適用範圍與例外（§1.3），明確列出不套用本規範的文件類型。
- 前置條件與限制的撰寫要求（§16.3）。
- 時區、千分位、數值範圍與版本號格式（§13）。
- Before / After 範例擴充至 12 則，新增台灣用語、修飾範圍歧義、AI 腔調、條件語序與中英文混排。
- `README.md`、`CLAUDE.md`、MIT `LICENSE`。

[0.2.0]: https://github.com/kirinlin/tw-writing/releases/tag/v0.2.0
[0.1.0]: https://github.com/kirinlin/tw-writing/releases/tag/v0.1.0
