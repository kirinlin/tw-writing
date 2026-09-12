# Changelog

本專案遵循 [Keep a Changelog](https://keepachangelog.com/) 格式。

## [0.3.0] - 2026-09-12

### Added

- §25 新增「外部工具（若可用）」小節：執行環境提供 [`zhtw`](https://github.com/sysprog21/zhtw-mcp) MCP 工具時，Agent 於 §23 六個 Pass 後呼叫 `zhtw` 做機械檢查（標點、字形、中國大陸用語），作為語意判斷之外的補充；程式碼與識別名稱不套用其建議，§14.6 與 MUST NOT 優先；工具不存在時略過，不影響本 Skill 既有運作方式。
- §26 最終檢查清單新增「外部工具」條目，僅於環境提供 `zhtw` 時適用。
- §1.4、`README.md` 補充 `references/taiwan-terms.md`（語意查表）與 `zhtw` MCP 工具（機械規則庫）的分工說明，避免混淆或重複維護兩份用語清單。

## [0.2.1] - 2026-09-12

### Fixed

- §25 AI Agent 行為規則：修正 `README.md`、`CLAUDE.md` 中「佔用 context」誤用（規則已規定 佔用 → 占用，僅修正兩處未依規則書寫的段落）。
- §22 標題「不要過度優化」改為「不要過度精簡」，避免與 §11.1「優化 → 最佳化」矛盾，並更準確描述本節主旨（避免過度刪減語意，而非工程上的最佳化）。
- §11.3 用字表：`傳送門` 的替代寫法從模糊的「（視情境改寫）」改為具體選項「連結／傳送點／捷徑（依情境擇一）」。
- §13.1 修正 `30°C` 誤標為「角度」，改稱「度數符號」，並補上真正的角度範例 `45°`。
- §4.5、§16.1：為「可以」新增明確例外——作為 RFC 2119 MAY 的正式對應詞時不受「避免不必要的可以」規則影響，避免兩條規則依序套用時把 MAY 誤改為 SHOULD。
- §25 MUST 清單第 8、9 項（不因追求簡潔而刪除必要條件／不擅自增加原文沒有的事實）改列入 MUST NOT，修正否定敘述誤置於正面義務清單、且與既有 MUST NOT 項目強度不一致的問題。
- §24 Example 1、2 的 After 範例移除殘留的「可以」與「我們」，使其與 §4.1、§10.8 的示範一致。
- `references/taiwan-terms.md`：移除「優化」在同形異義詞表中的重複分類（與 §2 及 `SKILL.md` §11.1 的「優化 → 最佳化」分類衝突），統一為單一分類。
- `references/taiwan-terms.md`：`並發`、`並行` 兩列分別補上英文原詞（concurrency、parallelism），解決「並行」同時是建議用語與應避免用語的矛盾。
- `references/taiwan-terms.md`：補上遺漏的「服務器 → 伺服器」列，與 `SKILL.md` §11.1 高頻對照表一致。
- `references/taiwan-terms.md`：簡化簡體字搜尋指令，移除多餘的前置 `rg` 呼叫並排除本檔案自身。
- `references/taiwan-terms.md`：破折號規則新增範圍說明，標題中以單一 em dash 分隔標籤與說明（如「Pass 1 — Structure」）不受「破折號需加倍」規則規範。
- `.gitignore` 新增 `.worker-*.log`，避免外部審查流程產生的執行紀錄檔混入已發佈的 repo。
- `ag.json` 修正 `better` tier 的 `claude` 模型 id（`claude-opus-4-6` 不存在，改為 `claude-opus-5/medium`）。

### Changed

- `README.md` 的「修改規範時」步驟改為指向 `CLAUDE.md` 對應章節，避免兩份清單各自增修後失去同步（原本 `README.md` 缺少 `CLAUDE.md` 才有的 `§` 交叉引用檢查步驟）。
- `CLAUDE.md` 的「修改規範時」步驟新增「更新 `references/taiwan-terms.md`」一項，並補充子節編號慣例的例外（§23、§24 等不編號的 H3 不受 `### N.M` 規則限制）。
- `references/taiwan-terms.md` 開頭新增說明：左右欄相同的列代表台灣與中國大陸寫法一致，審查命中不必改寫。

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

[0.3.0]: https://github.com/kirinlin/tw-writing/releases/tag/v0.3.0
[0.2.1]: https://github.com/kirinlin/tw-writing/releases/tag/v0.2.1
[0.2.0]: https://github.com/kirinlin/tw-writing/releases/tag/v0.2.0
[0.1.0]: https://github.com/kirinlin/tw-writing/releases/tag/v0.1.0
