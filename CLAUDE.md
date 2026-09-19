# CLAUDE.md

Claude Code 在此 repository 工作時，必須遵循 `AGENTS.md` 的共用指引。本檔案僅補充 Claude Code 專用內容。

## Claude Code 安裝管道

本 repository 同時是 Claude Code Plugin Marketplace 與其中唯一的 Plugin。使用者可執行以下指令：

```bash
claude plugin marketplace add kirinlin/tw-writing
claude plugin install tw-writing@tw-writing
```

此 repository 的根目錄同時是 Marketplace 與 Plugin 的根目錄。Plugin 根目錄包含 `SKILL.md`，但不含 `skills/` 子目錄時，Claude Code 會自動將該 Plugin 視為單一 Skill。因此，`plugin.json` 不需要額外宣告 `skills` 欄位。

## Claude Code 專用檔案

- `.claude-plugin/marketplace.json`：將本 repository 宣告為 `tw-writing` Plugin Marketplace。此檔案包含唯一的 Plugin 項目，且 `source` 指向 repository 根目錄（`./`）。
- `.claude-plugin/plugin.json`：包含 Plugin 中繼資料，例如 `name`、`description`、`version` 與 `author`。`version` 應與 `CHANGELOG.md` 的最新版本號一致。兩個 JSON 檔案的 `version` 也必須相同。

若發佈新版本，請同步更新 `.claude-plugin/marketplace.json` 與 `.claude-plugin/plugin.json` 的 `version` 欄位，並確保它們與 `CHANGELOG.md` 一致。
