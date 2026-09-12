# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案性質

本 repo 是一個 Agent Skill，內容全為 Markdown 文件，沒有程式碼、建置流程或測試。`SKILL.md` 就是產品本身；`README.md`、`CHANGELOG.md` 是它的附屬說明。以 Claude Code 為主要發佈對象，但同一份 `SKILL.md` 也可安裝到其他 Skill-aware Agent（見下方安裝管道）。

本 repo 同時支援三種安裝管道，三者都要求 `SKILL.md` 位於 repo 根目錄：

1. **手動 clone** 到 skills 目錄（`~/.claude/skills/tw-writing` 或專案的 `.claude/skills/tw-writing`）。
2. **`npx skills add kirinlin/tw-writing`**（[vercel-labs/skills](https://github.com/vercel-labs/skills)）：任何 Skill-aware Agent（Codex、opencode、Cursor 等）皆可安裝，其掃描規則會在 repo 根目錄尋找 `SKILL.md`。
3. **Claude Code Plugin Marketplace**（`claude plugin marketplace add kirinlin/tw-writing` 後 `claude plugin install tw-writing@tw-writing`）：repo 根目錄同時是 marketplace 與唯一的 plugin。Plugin 根目錄若只有 `SKILL.md`，沒有 `skills/` 子目錄，Claude Code 會自動視為單一 Skill 的 Plugin，不需要在 `plugin.json` 額外宣告 `skills` 欄位。

因此**絕對不要**把 `SKILL.md` 移到 `skills/tw-writing/SKILL.md` 之類的子目錄——這會讓管道 1、2 失效。

## 檔案角色

- `SKILL.md` — 台灣繁體中文寫作規範全文，共 29 節。開頭的 YAML frontmatter（`name`、`description`）決定 Claude Code 何時自動載入本 Skill；修改 `description` 會改變觸發行為。`name` 必須與安裝目錄名一致。
- `references/taiwan-terms.md` — 台灣用語與中國大陸用語完整對照表。刻意放在 `references/` 而非 `SKILL.md` 內：這是 progressive disclosure，長尾查表資料按需載入，避免每次都佔用 context。高頻詞與同形異義詞則保留在 `SKILL.md` §11，因為那是最容易出錯又必須永遠在場的部分。
- `.claude-plugin/marketplace.json` — 宣告本 repo 為名稱 `tw-writing` 的 Plugin Marketplace，內含唯一的 plugin 項目，`source` 指向 repo 根目錄（`./`）。
- `.claude-plugin/plugin.json` — 該 plugin 的 metadata（`name`、`description`、`version`、`author` 等）。`version` 應與 `CHANGELOG.md` 最新版本號一致；兩個 JSON 檔的 `version` 也必須互相一致。
- `README.md` — 面向 repo 讀者的摘要與安裝說明，內容衍生自 `SKILL.md`。
- `CHANGELOG.md` — 遵循 [Keep a Changelog](https://keepachangelog.com/) 格式。

## 編輯規範

**本 repo 的所有繁體中文內容都必須符合 `SKILL.md` 自身的規範。** 這是 dogfooding：文件若違反自己訂的規則，規則就失去說服力。編輯前先讀 `SKILL.md` §25 AI Agent 行為規則與 §26 最終檢查清單，輸出前逐項確認。

規則衝突時依 §27 的優先順序處理：Technical correctness > Semantic accuracy > Clarity > Consistency > Concision > Elegance。

## 修改規範時

1. 在 `SKILL.md` 對應章節新增或修改規則，並附 Before / After 範例。
2. 說明適用情境與例外。只給禁令而不給例外，會導致 Agent 機械套用。
3. 檢查 §26 最終檢查清單與 §28 一分鐘版本是否需要同步更新，這兩節是全文規則的濃縮。
4. 新增或修改章節編號時，全檔搜尋 `§` 交叉引用並一併更新。
5. 若影響 `README.md` 的摘要表格或檔案結構，一併更新。
6. 更新 `CHANGELOG.md`。
7. 若因此發佈新版本，同步更新 `.claude-plugin/marketplace.json` 與 `.claude-plugin/plugin.json` 的 `version` 欄位，使其與 `CHANGELOG.md` 一致。

## 慣例

- 日期一律使用 `YYYY-MM-DD`。
- `SKILL.md` 只有一個 H1；章節使用 `## N. 標題`，子節使用 `### N.M`。章節之間以 `---` 分隔。
- 章節標題以中文為主，保留通用的英文術語（如 `## 3. 清楚 Clarity`）。
- 交叉引用寫成 `§11`、`§21.4`。
- 在 Markdown 中示範含巢狀程式碼區塊的內容時，外層必須使用四個反引號，否則巢狀 fence 會提前關閉外層區塊。
