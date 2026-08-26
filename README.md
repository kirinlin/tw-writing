# tw-writing

**台灣繁體中文技術寫作規範，以 Claude Code Skill 形式提供。**

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
| 簡潔 | 刪除贅字、「進行＋名詞」改為動詞、避免「相關」與「部分」 |
| 精確 | 用數字取代模糊程度，區分 Requirement、Capability、Recommendation |
| 中文語法 | 的／地／得、條件在前結論在後、連接詞與頓號、量詞、避免英文直譯腔 |
| 台灣用語 | 中國大陸用語對照、同形異義詞（文件／檔案、質量／品質、項目／專案） |
| 中英文混排 | 術語保留原文、行內程式碼、中英文之間空格細則、縮寫 |
| 數字與日期 | 單位空格、千分位、範圍、`YYYY-MM-DD`、時區、版本號 |
| 標點 | 全形與半形、頓號、引號、括號、破折號、列表結尾標點 |
| Markdown | 標題、列表、表格、連結、程式碼區塊、強調 |
| 語氣 | 讀者稱謂一致、祈使句、避免情緒性用語 |
| 反模式 | 行銷語言、公文腔、不必要的修飾詞、AI 生成腔調 |
| Agent 規則 | MUST / SHOULD / SHOULD NOT / MUST NOT 四級行為約束 |

完整規範見 [SKILL.md](SKILL.md)。

## 檔案結構

```text
SKILL.md                      完整寫作規範（29 節）
references/taiwan-terms.md    台灣用語與中國大陸用語完整對照表
```

`references/taiwan-terms.md` 依需求載入：Agent 需要確認個別術語，或審查疑似中國大陸用語時才讀取，避免固定佔用 context。

## 安裝

### 個人帳號（所有專案共用）

```bash
git clone https://github.com/kirinlin/tw-writing.git ~/.claude/skills/tw-writing
```

### 單一專案

```bash
git clone https://github.com/kirinlin/tw-writing.git .claude/skills/tw-writing
```

安裝後重新啟動 Claude Code，並以 `/skills` 確認 `tw-writing` 已載入。

## 使用方式

Claude Code 會在偵測到繁體中文寫作任務時自動載入本 Skill。也可以直接指定：

```text
使用 tw-writing 審查 docs/architecture.md
```

```text
依照 tw-writing 規範改寫這段說明
```

```text
用 tw-writing 檢查這份文件有沒有中國大陸用語
```

Agent 套用規範後，應依 SKILL.md §26 的最終檢查清單逐項確認輸出。

## 修改流程

改寫文字時依序進行六個 Pass，不跳過順序：

1. **Structure** — 主題是否明確？結論是否太晚？
2. **Clarity** — 主詞、指涉、修飾範圍是否明確？
3. **Precision** — 術語、數字、規範強度是否正確？
4. **Concision** — 刪除贅字、空泛形容詞與 AI 腔調。
5. **Consistency** — 術語、稱謂、格式、標點是否一致。
6. **Naturalness** — 是否讀起來像自然的台灣繁體中文。

## 貢獻

修改規範時：

1. 在 `SKILL.md` 對應章節新增規則，並附 Before / After 範例。
2. 說明適用情境與例外。只給禁令而不給例外，會導致 Agent 機械套用。
3. 確認 §26 最終檢查清單與 §28 一分鐘版本是否需要同步更新。
4. 新增術語對照時，更新 `references/taiwan-terms.md`。
5. 更新 [CHANGELOG.md](CHANGELOG.md)。

本 repo 的所有繁體中文內容都必須符合 SKILL.md 自身的規範。

## 授權

[MIT](LICENSE)
