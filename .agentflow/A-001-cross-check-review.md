* _2026-09-12 13:36:17 (claude-opus-5/high)_

# A-001 cross-check review — tw-writing Agentflow bootstrap

Reviewed implementation commit: fc53331145836bdb02461548b5081376d938839c

Verdict: PASS

## Scope and method

Read-only review of the disposable clone. Files read in full: `CLAUDE.md`, `SKILL.md`, `references/taiwan-terms.md`, `README.md`, `CHANGELOG.md`, `LICENSE`, `ag.json`, `.agentflow/devlog.md`, plus `.gitignore` (named in acceptance check 2). No shell commands were run; all cross-checking was done with the file-read and content-search tools. No reviewed file was modified.

Instructions embedded in the reviewed content (notably `SKILL.md` §25 "AI Agent 行為規則" and `CLAUDE.md`'s editing rules) were treated strictly as data under evaluation, not as directives. Nothing in the repository attempted prompt injection; the §25 rules are ordinary style prescriptions addressed to a downstream Agent, and the only thing they asked of *this* review was to judge whether the repo obeys them.

**Model substitution, independently noted:** this dispatch was configured for the `cross-check` role at tier `better`, whose `ag.json` value is `claude-opus-4-6/high` (`ag.json:36`). That model id does not resolve for this CLI, and the coordinator substituted `claude-opus-5` at `high` effort. See finding M-1 — the stale id is in the newly added file and is worth fixing rather than re-substituting each round.

## Bottom line

The three new bookkeeping files introduce no risk to the product: they add no prose that the dogfooding rule governs, touch no shipped Skill content, and `.gitignore` correctly leaves `.agentflow/` tracked so the notebook is versioned. `SKILL.md` is a coherent, well-organized 29-section guide, and `README.md`/`CHANGELOG.md` describe it accurately on every claim I could mechanically check.

All findings below are non-blocking. I found no defect that makes the guide wrong to follow, no broken `§N` cross-reference, no Simplified characters, and no spacing or punctuation violations in the repo's own prose. What I did find is a cluster of small self-conformance gaps — places where `SKILL.md` states a rule that `SKILL.md` itself then breaks — which matter more than their size because this repo's entire credibility argument is dogfooding. C-1 through C-4 are the ones I would fix first.

---

## 1. Outcome — does the guide deliver what it claims

PASS. Verified against the claims made about it:

- `SKILL.md` has exactly one H1 and exactly 29 `## N.` sections (`SKILL.md:12`, `## 1.` … `## 29.`). `README.md:42` and `CLAUDE.md:13` and `CHANGELOG.md:9` all say "29 節" — correct.
- `CHANGELOG.md:22` claims "Before / After 範例擴充至 12 則". §24 contains Examples 1–12 — correct.
- Every `§N` cross-reference in the repo resolves. I extracted all of them (`§1.3 §2.2 §3.6 §6.3 §7.3 §10 §11 §12.1 §13 §13.2 §14 §14.5 §15 §16.3 §19 §21.4 §25 §26 §27 §28`, across `SKILL.md`, `README.md`, `CLAUDE.md`, `CHANGELOG.md`) and each points at a section that exists with the content implied. No dangling references.
- Every `CHANGELOG.md` 0.1.0 bullet corresponds to content actually present, including the ripgrep review commands (`references/taiwan-terms.md:448`) and the MIT `LICENSE`.
- All fenced code blocks in `SKILL.md`, `README.md`, and `references/taiwan-terms.md` carry a language tag, satisfying the guide's own §15.5. The nested-fence rule (`CLAUDE.md:39`, §15.5) is correctly applied — the `markdown` examples at `SKILL.md:1190–1210` are properly fenced and do not leak.
- `LICENSE` is an unmodified MIT text; `README.md:107` links it correctly.

### O-1 (low) — `30°C` is labelled an angle, in two places

`SKILL.md:1008` — "百分比與角度：`50%`、`30°C`" — and `SKILL.md:1056` — "**例外**：百分比與角度不加空格（`50%`、`30°C`）" — both name the exception category as 角度 (angle) while illustrating it with a temperature. The degree sign is shared, but `30°C` is 攝氏溫度, not an angle. The intent is recoverable, but §27 puts Technical correctness at the top of the priority order, so a factual mislabel in the guide's own rule text is the single most incorrect thing in the document. Suggested wording: 「百分比與度數符號（`50%`、`30°C`、`45°`）」.

### O-2 (low) — two claims about external tooling I could not verify offline

`README.md:62` instructs users to "以 `/skills` 確認 `tw-writing` 已載入", and `README.md:53`/`README.md:59` give a clone URL (`github.com/kirinlin/tw-writing`). This clone has no remotes and this session has no network, so I can confirm neither. Flagging for a human check rather than asserting either is wrong — if `/skills` is not a current Claude Code command, that line sends every new user down a dead end on their first interaction with the Skill.

---

## 2. Minimality — duplication, contradiction, and bookkeeping weight

Minimality: PASS. The Agentflow addition is appropriately small; the findings here are about the pre-existing reference table and one `.gitignore` omission.

### M-1 (medium) — `ag.json` pins a `better` model id that does not resolve, and the notebook claims it was validated

`ag.json:36` sets `"better": "claude-opus-4-6/high"`. That id does not exist for this CLI, which is why this very dispatch required a substitution. `better` is the configured tier for 8 of the 10 pipeline roles (`ag.json:15–25`: requirements, codewalk, explore, spike, spec, acceptance, cross-check, learn), so this is not a one-off — every one of those roles will hit the same substitution on every round.

Compounding it, `.agentflow/devlog.md:11` records "Configuration: ag.json — schema v7; validated for claude this round." The claude worker's most-used tier id is not valid, so the STATUS line overstates what validation established. Worth correcting both the id and the claim, since a STATUS line that asserts a check that did not hold is exactly the kind of thing later rounds will trust without re-deriving.

### M-2 (medium) — `.gitignore` does not cover the runner's own log files

`.gitignore` lists `.claude/`, `.codex/`, `.worktrees/`. But this clone contains `.worker-stderr.log` and `.worker-stdout.log` at the root, produced by the external runner, and neither is ignored. They will show as untracked in every `git status` and will be swept into any `git add -A`. For a repo whose publication method is "clone this directly into your skills directory" (`CLAUDE.md:9`), committing runner logs into the published artifact is a real, if minor, hygiene problem. Adding `.worker-*.log` closes it. This is the one place where the bootstrap added *less* than it needed to rather than more.

(For completeness: `A-001-brief.md` and this report are also untracked and unignored, but they exist only in this disposable review clone and are not a repo concern.)

### M-3 (medium) — the "complete" term table contains rows that carry no mapping

`references/taiwan-terms.md:5` states the contract plainly: 「左欄為中國大陸慣用語，右欄為台灣慣用語。寫作時使用右欄；審查時搜尋左欄。」 Roughly seventy rows violate that contract by repeating the same term in both columns — `密碼|密碼`, `權限|權限`, `節點|節點`, `模型|模型`, `備份|備份`, `部署|部署`, `框架|框架`, `重構|重構`, `分支|分支`, `合併|合併`, `漏洞|漏洞`, and many more.

I take these to be intentional "do not over-correct this one" markers, which is genuinely useful information. The problem is that the file never says so, and under the stated contract ("審查時搜尋左欄") each one is an instruction to search for a term that is perfectly correct. An Agent applying the file literally will flag `密碼` and `節點` as Mainland usage. Either add a third column or a short note distinguishing "identical in both" rows from real mappings, or drop them.

### M-4 (medium) — rows where a term appears on both sides of the table, in different rows

Sharper than M-3, because these are self-contradictory under any reading:

| Location | Rows | Conflict |
|---|---|---|
| `references/taiwan-terms.md:241–242` | `並發 \| 並行` and `並行 \| 平行` | 並行 is simultaneously the prescribed Taiwan term (for concurrency) and a proscribed Mainland term (for parallelism) |
| `references/taiwan-terms.md:76` | `顯示器 \| 螢幕／顯示器` | 顯示器 proscribed and prescribed |
| `references/taiwan-terms.md:96` | `崩潰 \| 當機／崩潰` | same shape |
| `references/taiwan-terms.md:334` | `吞吐量 \| 傳輸量／吞吐量` | same shape |
| `references/taiwan-terms.md:402` | `截圖 \| 螢幕擷取畫面／截圖` | same shape |

The 並發/並行/平行 row pair is the one that actively misleads: the underlying terminology is correct (concurrency → 並行, parallelism → 平行), but the two-column format cannot express it, so the table as printed tells the reader both to use and to avoid 並行. The file already solves this elsewhere with English glosses — `程序（program）` at line 39, `連接（join）` at line 267 — so applying the same device here is consistent with the file's own conventions.

### M-5 (low) — 服務器 is in the summary table but missing from the "complete" one

`SKILL.md:854` lists `服務器 → 伺服器` among the high-frequency pairs, and `references/taiwan-terms.md:453`'s review regex searches for `服務器`. But the complete table has no such row — §4 網路與雲端 covers 網關, 交換機, 域名 and so on, and §2 offers only `服務端 → 伺服器端` (line 50). I checked the other ~45 entries of `SKILL.md` §11.1 against the reference file and this is the only one that is missing, so it reads as an oversight rather than a policy. Since `SKILL.md:842` and `README.md:43` both bill the reference as the 完整 table, the gap undercuts that promise.

### M-6 (low) — the reference file's Simplified-character search is redundant

`references/taiwan-terms.md:461`:

```
rg -n '[\x{4E00}-\x{9FFF}]' --pcre2 . | rg '国|个|们|这|…'
```

The first `rg` matches any CJK character whatsoever, so it emits every line containing Chinese and the second `rg` does all the actual work. `rg -n '国|个|们|这|…' .` alone is equivalent and far cheaper. (Both commands also match the reference file itself, since the pattern literals contain the very characters being hunted — worth a `-g '!references/taiwan-terms.md'` or a note.)

### M-7 (low) — three overlapping, partially divergent process checklists

The "how to change the rules" procedure is stated three times: `CLAUDE.md:24–31` (6 steps), `README.md:95–101` (5 steps), and implicitly in `SKILL.md` §23's six Passes. `CLAUDE.md` and `README.md` genuinely diverge — `CLAUDE.md` step 4 ("全檔搜尋 `§` 交叉引用並一併更新") and step 5 ("若影響 `README.md` … 一併更新") have no `README.md` counterpart. Contributors reading only `README.md` will skip the cross-reference sweep, which is the step that keeps the `§N` references intact. One of the two should defer to the other.

### M-8 (low) — duplicated rows across reference sections

`優化` appears at both `references/taiwan-terms.md:26` and `:185`; `分辨率` at `:80` and `:399`; `數據集` at `:45` and `:378`; `補丁` at `:322` and `:358`; `信息` at `:22` and `:41`. Cross-domain repetition is defensible for a lookup table, but the 優化 pair is not merely duplicated — it is inconsistent (see C-5).

---

## 3. Conformance — does the repo obey its own §25/§26 rules

Conformance: PASS. The mechanical checks are clean; the findings are specific rule-versus-practice conflicts.

**What passed, checked mechanically across all Markdown files:**

- **No Simplified characters** anywhere except inside the deliberate search patterns at `references/taiwan-terms.md:461` and the Before examples in §24 — both legitimate.
- **No full-width alphanumerics and no full-width (U+3000) spaces**, satisfying §11.4. Zero hits.
- **CJK/Latin spacing (§12.4) is correct throughout.** I searched for a Han character adjacent to a Latin letter or digit across the whole repo; the only hit is `SKILL.md:1789`, which is the intentional Before example of exactly that mistake. This is genuinely well executed — it is the easiest rule in the guide to break accidentally and the repo does not break it once.
- **No half-width punctuation in Chinese prose** (§14.1/§14.2), same single intentional exception.
- **Reader address (§20.1) is consistent** — `SKILL.md` and `README.md` use neither 你 nor 您 in their own voice.
- **台/臺 is consistent** (§11.3) — 台 throughout, with 臺 appearing only inside the rule that discusses the choice.
- **Heading depth never skips** (§15.1); the H4s in §5.2, §6.2, §10.5 and §16.1 all sit under an H3.

### C-1 (medium) — the repo writes 佔用 in the very files that ban it

`SKILL.md:924` and `references/taiwan-terms.md:424` both prescribe 佔用 → 占用 under "使用教育部標準字體用字". The repo then writes 佔 six times:

- `SKILL.md:1148` 「佔兩個字寬」
- `SKILL.md:1149` 「佔兩個字寬」
- `SKILL.md:1266` 「明顯的佔位符」
- `references/taiwan-terms.md:307` 「佔位符 | 佔位符」
- `README.md:46` 「避免固定佔用 context」
- `CLAUDE.md:14` 「避免每次都佔用 context」

`CLAUDE.md:20` states that all Traditional Chinese content in the repo must conform to `SKILL.md`, so this is an unambiguous dogfooding failure — and it is mechanically detectable, which makes it the kind a reader will find.

My recommendation is to fix the rule rather than the prose. 佔位符 is the established Taiwan rendering of "placeholder" (it is the Microsoft terminology), so a blanket 佔 → 占 substitution would make `SKILL.md:1266` and `references/taiwan-terms.md:307` worse. Narrowing the rule to the specific word — 佔用 → 占用 — leaves 佔位符 legitimate and still requires fixing `README.md:46` and `CLAUDE.md:14`, which are the two genuine violations.

### C-2 (medium) — §22's own heading uses a term §11.1 proscribes

`SKILL.md:874` lists `優化 → 最佳化` as a Mainland-usage correction, and §24's Example 8 duly rewrites 優化 to 最佳化 at `SKILL.md:1749`. But the section heading at `SKILL.md:1583` reads `## 22. 不要過度優化`. A heading is the most visible prose in a document, and this one breaks the table three sections earlier. `不要過度最佳化` is the mechanical fix; `不要過度精簡` may read better given that §22 is about over-shortening rather than optimization in the engineering sense.

### C-3 (medium) — two §24 "After" exemplars still contain what other sections tell you to delete

§24's Afters are the canonical good-output samples; an Agent will pattern-match on them more strongly than on any prose rule.

- **Example 2** (`SKILL.md:1689`): After is 「**我們需要修改系統設定。**」 The example targets 名詞化 and fixes it correctly, but the output retains 我們, which §10.8 ("避免過度使用「我們」"), §25 SHOULD NOT #4, §26's checklist item 「是否有不必要的「我們」？」 and §28 #8 all tell the Agent to remove. §10.8's own worked example (`SKILL.md:824–828`) deletes 我們 from a structurally identical sentence. 「需要修改系統設定。」 would be consistent.
- **Example 1** (`SKILL.md:1679`): After is 「**目前系統可以正常運作。**」, retaining 可以 against §4.5 and §28 #8. §4.1's example (`SKILL.md:298–302`) rewrites a near-identical Before — 「在目前的情況之下，我們可以看到系統目前仍然存在問題。」 — all the way to 「目前系統仍有問題。」, dropping 可以. The two sections treat the same construction differently.

Both are defensible in isolation, and §27 would let Clarity override Concision. But neither example says so, and the inconsistency with §4.1's and §10.8's own worked examples is what makes it a finding rather than a judgement call.

### C-4 (medium) — §16.2 prescribes 可以 while §4.5 and §16.1 warn against it

`SKILL.md:1319` maps `MAY / OPTIONAL → 可以／可選`. Three sections earlier, §4.5 is titled 「避免不必要的「可以」」, and §16.1 closes with 「不要使用「可以」模糊上述四種語意」 (`SKILL.md:1297`). An Agent rendering an RFC 2119 MAY will write 可以 per §16.2, and an Agent running §26's checklist item 「是否有不必要的「可以」？」 will then delete it, changing a MAY into a bare capability statement — which §25 MUST NOT #4 ("將 MAY 改成 SHOULD") exists precisely to prevent.

This is the finding with the most downstream consequence, because the two rules can be applied in sequence by the same Agent in the same pass. §4.5 needs an explicit carve-out: 可以 is protected when it renders a normative MAY.

### C-5 (low) — 優化 is classified two different ways

`SKILL.md:874` and `references/taiwan-terms.md:185` list 優化 flatly as Mainland usage to be replaced. `references/taiwan-terms.md:26` instead files it under 同形異義詞 with the Taiwan reading 「（可用，但非首選）」 — that is, acceptable but dispreferred. Those are different strengths for the same word, and §25 MUST NOT #2 makes requirement strength something the guide treats as load-bearing. Pick one.

### C-6 (low) — the single em dash the repo uses everywhere is the one its reference file proscribes

`references/taiwan-terms.md:442` lists 「單一破折號 `—`」 under 避免, prescribing 「——」; `SKILL.md:1148` says the same. Yet the single em dash is the repo's house separator style, used consistently in all 18 of `SKILL.md`'s §23 Pass and §24 Example headings, all 6 `README.md` Pass bullets, and all 4 `CLAUDE.md` file-role bullets.

I read the house style as correct and the rule as over-broad: an em dash separating a label from its gloss in a heading is not the 破折號 that §14.5 is about, and doubling it in `### Pass 1 —— Structure` would look wrong. The fix is to scope the rule to 破折號 used as in-sentence punctuation, which is what §14.5's surrounding text already describes. Worth resolving explicitly, because as written the repo fails its own check 28 times.

### C-7 (low) — §25's MUST list contains prohibitions, and overlaps its own MUST NOT list

`SKILL.md:1810–1811` places two negative items — 「8. 不因追求簡潔而刪除必要條件。」 and 「9. 不擅自增加原文沒有的事實。」 — inside the **MUST** list, which otherwise holds positive obligations. Item 9 restates MUST NOT #6 (「捏造數據」, `SKILL.md:1844`); item 8 restates SHOULD NOT #8 (「為了簡潔而犧牲精確性」, `SKILL.md:1834`) but at MUST strength rather than SHOULD NOT, so the same rule carries two different strengths. MUST #7 (「使用台灣慣用術語」) and MUST NOT #10 (「使用中國大陸慣用術語」) are likewise the same rule in both polarities.

This matters more than ordinary redundancy for two reasons: §8 requires parallel concepts to use parallel grammar, and §25 is the section `CLAUDE.md:20` designates as the dogfooding gate. Moving items 8 and 9 into MUST NOT resolves both.

### C-8 (low) — `SKILL.md` §11.3 contains a row that is not a 用字 issue and gives no replacement

`SKILL.md:926` puts 「傳送門 | （視情境改寫）」 in the 用字 table, whose stated subject is 教育部標準字體 glyph choice. 傳送門 is a vocabulary and register issue, not a glyph one, so it is in the wrong table. The replacement column then says only 「（視情境改寫）」, which is precisely the kind of vague non-instruction §3.3 tells writers to avoid, and `CLAUDE.md:27` warns that rules without concrete alternatives get applied mechanically. 傳送門 also appears nowhere in `references/taiwan-terms.md`, so §11.5's promise that the reference resolves individual terms fails for this one. Either give the actual alternatives (連結／傳送點／捷徑, depending on context) or move it to a register section.

### C-9 (low) — two H3 series deviate from the stated section-numbering convention

`CLAUDE.md:36` states the convention absolutely: 「子節使用 `### N.M`」. §23's 「### Pass 1 — Structure」 and §24's 「### Example 1 — 贅字」 use unnumbered H3s instead. The headings themselves are good — the convention statement is simply narrower than the document it describes, and should say that *numbered* subsections use `N.M`.

---

## 4. Notes on the Agentflow addition, for the record

Two choices in the new files are correct and worth stating so later rounds do not undo them:

- `ag.json:9` sets `"lang": "en"`, and `.agentflow/devlog.md` is written in English. This is the right call for this specific repo: `CLAUDE.md:20` subjects *all* Traditional Chinese content in the repo to `SKILL.md`'s rules, so a Chinese-language notebook would pull machine bookkeeping into the dogfooding gate and generate conformance findings on STATUS lines forever. If `lang` is ever switched to a Chinese locale, that consequence lands immediately.
- `.gitignore` ignores `.claude/` and `.codex/` but leaves `.agentflow/` tracked, so the notebook is versioned with the work. Correct. Note that ignoring `.claude/` also prevents committing project-level Claude configuration in this repo — deliberate-looking for a Skill repo, and it does not conflict with `README.md:59`, which tells *consumers* to clone into their own `.claude/skills/`.

One small accuracy point: `.agentflow/devlog.md:7` reads "Current commit: initialization pending." That placeholder was already stale when the file was committed, since the bootstrap commit is fc293f6.

---

## Recommended follow-up order

If any of this becomes work, I would sequence it: **M-1** (invalid model id plus the overstated STATUS claim — it costs a substitution on 8 of 10 roles every round), **M-2** (one `.gitignore` line, prevents runner logs reaching a published repo), **C-4** (the only finding where two rules applied in sequence corrupt output), **C-1/C-2** (mechanically detectable dogfooding failures in the most-read prose), then **M-4** (the 並行 table contradiction), then the rest as cleanup. **O-1** is a one-word fix and can ride along with any of them.

None of these authorize themselves into changes; the coordinator decides.

Outcome: PASS
Minimality: PASS
Conformance: PASS

Self-check: reviewed CLAUDE.md, SKILL.md, references/taiwan-terms.md, README.md, CHANGELOG.md, LICENSE, ag.json, .agentflow/devlog.md, and .gitignore in the disposable clone read-only; ran no commands and modified no reviewed file; the worker process could not write this file itself under --restricted, so the coordinator saved this exact content verbatim on its behalf.
