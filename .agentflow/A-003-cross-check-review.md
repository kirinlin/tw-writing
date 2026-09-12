* _2026-09-12 17:20:00 (claude-opus-5/medium)_

# A-003 cross-check review — zhtw MCP tool integration rule

Reviewed implementation commit: da340f8b271fe2aa273553e44ce19828b2694c9a

Verdict: PASS

Outcome: PASS
Minimality: PASS
Conformance: PASS

## Method

Cross-check-plan.js selected level "targeted" (changed_files: SKILL.md, README.md, CHANGELOG.md, .claude-plugin/plugin.json, .claude-plugin/marketplace.json; changed_lines: 29; behavior_change/trust_boundary/broad_change/consequential_change: false). Two rounds of read-only review, each in a fresh disposable no-remote clone of this repository (local `git clone`, `git remote remove origin`, then `git apply` of the exact candidate diff), dispatched via `claude -p --restricted` at `claude-opus-5/medium` (the `better` tier), with only read-oriented tools allowed and Write/Edit/NotebookEdit denied. No reviewed file was modified by the reviewer in either round. Full reviewer transcripts are kept in this session's scratchpad, not committed.

## Round 1 (superseded) — the reviewer's dimension verdicts that round were Outcome blocking, Minimality passing, Conformance passing

Blocking finding: the first draft of §25's "外部工具（若可用）" subsection told the Agent to apply `zhtw` MCP tool suggestions directly, without semantic re-check, over an unscoped `§2–§22` range that included §11/§12/§14 — sections governing code-block punctuation, identifier spelling, and casing that §14.6 and existing §25 MUST NOT items 8 and 11 declare have no exceptions. Since `zhtw` has no guaranteed Markdown-fence or identifier awareness, this could have made the Agent corrupt a code sample or rename an identifier when `zhtw` mis-flagged it — exactly the failure §14.6 and those MUST NOT items exist to prevent.

Six non-blocking findings were also raised: an introduced synonym ("跨海峽用詞") competing with the document's established term ("中國大陸用語"); a 頓號 joining non-parallel elements; a checklist group header inconsistent with the rest of §26; a discouraged mid-sentence 破折號; a 公文腔 pronoun ("呼叫其") in README/CHANGELOG; and a README placement mismatch (under 檔案結構 instead of 使用方式).

## Fix applied

- Scoped the "apply directly" bullet to prose text only, and added a new bullet giving code blocks/inline code/API/identifier names an explicit, exception-free priority over `zhtw`, citing §14.6 and MUST NOT 8/11.
- Replaced the fragile `§2–§22` range with "本文件其他各節" — removing the enumeration rather than merely narrowing it.
- Applied all six non-blocking fixes: standardized on 「中國大陸用語」; fixed the 頓號; simplified the §26 header; split the 破折號 sentence in two; replaced 「呼叫其」 with 「呼叫 `zhtw`」; moved the README note to 使用方式.

## Round 2 (final, matches the reviewed commit above) — Outcome, Minimality, and Conformance all confirmed passing

Confirmed the round-1 blocking finding resolved on both axes (prose-only scoping, exception-free code/identifier carve-out with correct §-number cross-references), confirmed no new contradiction, and confirmed the terminology/dogfooding fixes landed with zero remaining occurrences of the introduced synonym.

Two further non-blocking cosmetic observations were raised: the §26 checklist item had lost its own in-place "(若可用)" marker after the header simplification, and the CHANGELOG quoted a checklist heading string that no longer matched post-fix. Both were corrected directly (checklist item now reads "若環境提供 zhtw MCP 工具，是否已呼叫 zhtw 做機械檢查…"; CHANGELOG line no longer quotes a heading) without a third review round, since round 2's reviewer itself classified them as non-correctness cosmetic drift rather than a defect.

Self-check: Reconstructed the coordinator record from both external review transcripts, confirmed round 2 returned the required exactly-one-each PASS verdict for Outcome, Minimality, and Conformance against implementation commit da340f8b271fe2aa273553e44ce19828b2694c9a, and independently re-read the final SKILL.md §25/§26, README.md, and CHANGELOG.md state after the post-round-2 cosmetic fixes to confirm they match what round 2 accepted.
