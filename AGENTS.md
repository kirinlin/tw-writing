# AGENTS.md

本檔案提供 AI Agent 在此 repository 工作時所需的共用指引。

## 專案性質

本 repo 是一個 Agent Skill，內容全為 Markdown 文件，沒有程式碼、建置流程或測試。`SKILL.md` 就是產品本身；`README.md`、`CHANGELOG.md` 是它的附屬說明。同一份 `SKILL.md` 可安裝到多種支援 Skill 的 Agent。

本 repo 支援下列安裝管道，且都要求 `SKILL.md` 位於 repo 根目錄：

1. **手動 clone** 到 Agent 的 skills 目錄。
2. **`npx skills add kirinlin/tw-writing`**（[vercel-labs/skills](https://github.com/vercel-labs/skills)）：Codex、Claude Code、opencode、Cursor 等支援 Skill 的 Agent 皆可安裝，其掃描規則會在 repo 根目錄尋找 `SKILL.md`。
3. **Claude Code Plugin Marketplace**：Claude Code 專用的安裝管道，細節請見 `CLAUDE.md`。

因此，**絕對不要**把 `SKILL.md` 移到 `skills/tw-writing/SKILL.md` 之類的子目錄。這會讓手動安裝與 `npx skills add` 失效。

## 檔案角色

- `SKILL.md` — 台灣繁體中文寫作規範全文，共 29 節。開頭的 YAML frontmatter（`name`、`description`）決定 Agent 何時自動載入本 Skill；修改 `description` 會改變觸發行為。`name` 必須與安裝目錄名稱一致。
- `references/taiwan-terms.md` — 台灣用語與中國用語完整對照表。此檔案刻意放在 `references/`，而非 `SKILL.md` 內。這是 progressive disclosure：Agent 僅在需要時載入長尾查表資料，避免每次都占用 context。高頻詞與同形異義詞保留在 `SKILL.md` §11，因為這些內容容易出錯，而且必須隨時可用。
- `README.md` — 面向 repo 讀者的摘要與安裝說明，內容衍生自 `SKILL.md`。
- `CHANGELOG.md` — 遵循 [Keep a Changelog](https://keepachangelog.com/) 格式。
- `CLAUDE.md` — Claude Code 專用指引，包括 Plugin Marketplace 的結構與版本規則。

## 編輯規範

**本 repo 的所有繁體中文內容都必須符合 `SKILL.md` 自身的規範。** 這是 dogfooding：文件若違反自己的規則，規則就失去說服力。編輯前先讀 `SKILL.md` §25 AI Agent 行為規則與 §26 最終檢查清單。輸出前逐項確認。

規則衝突時，依 §27 的優先順序處理：Technical correctness > Semantic accuracy > Clarity > Consistency > Concision > Elegance。

## 修改規範時

1. 在 `SKILL.md` 對應章節新增或修改規則，並附 Before / After 範例。
2. 說明適用情境與例外。只給禁令而不給例外，會導致 Agent 機械套用。
3. 檢查 §26 最終檢查清單與 §28 一分鐘版本是否需要同步更新。這兩節是全文規則的濃縮。
4. 新增或修改章節編號時，全檔搜尋 `§` 交叉引用，並一併更新。
5. 若變更會影響 `README.md` 的摘要表格或檔案結構，請一併更新。
6. 新增或修改台灣用語與中國用語對照時，同步更新 `references/taiwan-terms.md`。
7. 更新 `CHANGELOG.md`。
8. 若因此發佈新版本，請依各發佈管道的規則同步更新版本資料。

## 慣例

- 日期一律使用 `YYYY-MM-DD`。
- `SKILL.md` 只有一個 H1。章節使用 `## N. 標題`；有編號的子節使用 `### N.M`。§23、§24 等不編號的 H3（例如「Pass 1」「Example 1」）不在此限。章節之間以 `---` 分隔。
- 章節標題以中文為主，保留通用的英文術語（例如 `## 3. 清楚 Clarity`）。
- 交叉引用寫成 `§11`、`§21.4`。
- 在 Markdown 中示範含巢狀程式碼區塊的內容時，外層必須使用四個反引號，否則巢狀 fence 會提前關閉外層區塊。
