# tw-writing

台灣繁體中文寫作規範，以 Agent Skill 形式提供，適用於支援 Skill 的 AI Agent。

本 Skill 讓 AI Agent 產生或修改繁體中文內容時，遵循一致的清晰、精確、簡潔標準。內容以 *The Elements of Style* 的寫作原則為基礎，針對繁體中文語法、資訊結構、台灣用語、中英文混排及技術寫作進行本地化。

適用文件類型：技術文件、軟體文件、README、設計文件、規格書、SOW、工程報告、操作手冊、錯誤訊息、commit message。

## 核心原則

> **清楚優先於簡潔，簡潔優先於華麗。**

規則衝突時的優先順序：

```text
Technical correctness > Semantic accuracy > Clarity > Consistency > Concision > Elegance
```

## 規範內容

| 主題 | 說明 |
|---|---|
| 結構 | 一段一主題、段首先說重點、一句一主要意念 |
| 清楚 | 明確主詞、具體動詞、具體名詞、消除修飾範圍歧義 |
| 簡潔 | 刪除贅字與名詞化，保留有語意功能的限定詞 |
| 精確 | 有依據才量化，保留範圍、不確定性與規範強度，區分要求、能力、建議與許可 |
| 中文語法 | 的／地／得、條件與結論、連接詞與頓號、量詞、避免英文直譯腔 |
| 台灣用語 | 中國用語對照、依語意選詞，辨別文件／檔案、質量／品質、項目／專案 |
| 中英文混排 | 術語保留原文、行內程式碼、中英文之間空格細則、縮寫 |
| 數字與日期 | 單位空格、千分位、範圍、`YYYY-MM-DD`、時區、版本號 |
| 標點 | 全形與半形、頓號、引號、括號、破折號、列表結尾標點 |
| Markdown | 標題、列表、表格、連結、程式碼區塊、強調 |
| 語氣 | 讀者稱謂一致、祈使句、避免情緒性用語 |
| 反模式 | 行銷語言、公文腔、不必要的修飾詞、AI 生成腔調 |
| Agent 規則 | 保護事實與技術內容、依任務範圍交付、覆核工具建議 |

完整規範見 [SKILL.md](SKILL.md)。

## 檔案結構

```text
SKILL.md                          完整寫作規範（29 節）
references/taiwan-terms.md        台灣用語與中國用語完整對照表
AGENTS.md                         AI Agent 共用維護指引
CLAUDE.md                         Claude Code 專用指引
.claude-plugin/marketplace.json   Claude Code Plugin Marketplace 設定
.claude-plugin/plugin.json        Claude Code Plugin 定義
```

`references/taiwan-terms.md` 依需求載入：Agent 需要確認個別術語，或審查疑似中國用語時才讀取，避免固定占用 context。

`.claude-plugin/` 只有 Claude Code 的 Plugin 安裝路徑會用到；`npx skills add` 與手動 Clone 皆直接讀取根目錄的 `SKILL.md`，不受影響。

## 安裝

### Claude Code（Plugin Marketplace）

```bash
claude plugin marketplace add kirinlin/tw-writing
claude plugin install tw-writing@tw-writing
```

### 任何支援 Skill 的 Agent（Codex、opencode、Cursor 等）

```bash
npx skills add kirinlin/tw-writing
```

`npx skills` 會偵測本機已安裝的 Agent，並將 `SKILL.md` 安裝到對應的 Skill 目錄。

### 手動 Clone（Claude Code，不透過 Plugin）

個人帳號（所有專案共用）：

```bash
git clone https://github.com/kirinlin/tw-writing.git ~/.claude/skills/tw-writing
```

單一專案：

```bash
git clone https://github.com/kirinlin/tw-writing.git .claude/skills/tw-writing
```

安裝後重新啟動 Agent，再明確指定使用 `tw-writing` 處理一段文字，確認 Agent 能讀取本 Skill。

## 更新

依原本的安裝方式選擇更新指令。

### Claude Code（Plugin Marketplace）

先更新 Marketplace 清單，再更新已安裝的 Plugin：

```bash
claude plugin marketplace update tw-writing
claude plugin update tw-writing@tw-writing
```

更新後重新啟動 Claude Code。Marketplace 清單與已安裝的 Plugin 是不同的更新對象，詳見 [Claude Code Plugin 更新說明](https://code.claude.com/docs/en/discover-plugins#update-plugins-now)。

### 透過 `npx skills` 安裝

只更新 `tw-writing`：

```bash
npx skills update tw-writing
```

執行時依提示選擇安裝範圍；也可用 `-g` 指定個人帳號，或用 `-p` 指定目前專案。若要更新所有已安裝的 Skill，使用 `npx skills update`，詳見 [skills CLI 更新說明](https://github.com/vercel-labs/skills#skills-update)。

### 手動 Clone

個人帳號：

```bash
git -C ~/.claude/skills/tw-writing pull --ff-only
```

單一專案（在專案根目錄執行）：

```bash
git -C .claude/skills/tw-writing pull --ff-only
```

若 Clone 到其他 Agent 的 skills 目錄，將路徑改為實際安裝位置。

## 使用方式

支援自動選用 Skill 的 Agent 可依任務載入本 Skill，也可以直接指定：

```text
使用 tw-writing 審查 docs/architecture.md
```

```text
依照 tw-writing 規範改寫這段說明
```

```text
用 tw-writing 檢查這份文件有沒有中國用語
```

Agent 套用規範後，應依 `SKILL.md` §26 檢查與任務相關的項目。改寫與翻譯以完成的文字為主；只要求審查時，指出問題與建議，不直接修改檔案。

若環境提供 [`zhtw-mcp`](https://github.com/sysprog21/zhtw-mcp) 的文字檢查工具，Agent 會使用實際可呼叫的工具檢查標點、字形與用語，再依語意覆核建議。工具不存在或呼叫失敗時，改依檢查清單自行檢查，不影響本 Skill 的使用，見 `SKILL.md` §25「外部工具（若可用）」。

## 修改流程

完整文件依下列順序審查；短句或局部修改可合併檢查，修改影響事實或結構時再回頭確認：

1. **Structure** — 主題是否明確？結論是否太晚？
2. **Clarity** — 主詞、指涉、修飾範圍是否明確？
3. **Precision** — 事實、數字、範圍、不確定性與規範強度是否保留？
4. **Concision** — 刪除贅字、空泛形容詞與 AI 腔調。
5. **Consistency** — 術語、稱謂、格式、標點是否一致。
6. **Naturalness** — 是否讀起來像自然的台灣繁體中文。

## 貢獻

修改規範時，完整步驟（包括 `§` 交叉引用檢查與版本號同步）見 [AGENTS.md](AGENTS.md) 的「修改規範時」一節。Claude Code 專用的 Plugin Marketplace 維護規則見 [CLAUDE.md](CLAUDE.md)。本 repository 的所有繁體中文內容都必須符合 `SKILL.md` 的規範。

## 授權

[MIT](LICENSE)
