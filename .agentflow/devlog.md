# STATUS

Project: tw-writing

Notebook: .agentflow/devlog.md — root.

Current commit: 627080e on main (not yet pushed — awaiting owner confirmation per A-004's suggested-default question). origin/main is at 9fa620b (A-003's `int/zhtw-mcp` was merged to main and a follow-up fix bumped 0.3.0 → 0.3.1 in a prior round not recorded here at the time).

Tests/scenarios: none (Markdown-only repo; no build or test suite).

Configuration: ag.json — schema v7; validated for claude this round.

Proven: A-001's brownfield baseline cross-check passed (Outcome/Minimality/Conformance all PASS); A-002 applied direct-route fixes for 17 of its 19 parked findings and bumped 0.2.0 to 0.2.1; A-003 added SKILL.md §25's conditional "外部工具（若可用）" rule integrating the external `sysprog21/zhtw-mcp` MCP tool as an optional mechanical-check companion, bumped 0.2.1 to 0.3.0, passed a two-round targeted-level external cross-check, was merged to main, and a follow-up fix bumped 0.3.0 to 0.3.1; A-004 renamed `中國大陸用語` → `中國用語` across 7 files (SKILL.md, README.md, CHANGELOG.md, CLAUDE.md, references/taiwan-terms.md, both plugin manifests), passed a one-round targeted-level external cross-check (Outcome/Minimality/Conformance all PASS).

Open: M-4's 4 remaining self-referencing rows (parked, no clear fix specified); O-2's `/skills` command claim (unverifiable offline); whether the mid-A-002 `allow-ag` change from `ask` to `on`, not made by this session, was intentional; A-002's 3 questions still unanswered; A-004 flagged (non-blocking, parked for owner) that a differently-worded `中國大陸` prefix remains in a few places outside this Ask's scope.

Next: await owner's answers to A-002's questions, and A-004's two questions (push `627080e`? extend the rename to the parked `中國大陸` occurrences?).

Artifacts: .agentflow/A-001-cross-check-review.md, .agentflow/A-003-cross-check-review.md, .agentflow/A-004-cross-check-review.md.

Archived eras: none.

Streams: none.

---

# → Ask / A-001

+ /agentflow:agentflow

# ← Reply / A-001

* _2026-09-12 13:36:17 (Asia/Taipei)_ — Sonnet 5, Claude Code

## [SUMMARY]

- Ran `agf.js init` and `resume-intake.js` — clean bootstrap, no problems reported.
- The command carried no task text this round, so no work route was selected.
- Closing this first Reply triggered Agentflow's brownfield baseline rule (first-ever Reply treats every pre-existing tracked file as reviewed), which required an external cross-check before the round could close. Dispatched a full-level review via `external-runner-v1` (`claude -p --restricted`, disposable no-remote clone); it returned Verdict: PASS with Outcome/Minimality/Conformance all PASS, plus 19 non-blocking findings on the pre-existing `SKILL.md`/`references/taiwan-terms.md` content (mostly places where the guide breaks its own dogfooding rule). None of those findings are promoted to work here — they're parked for you to decide on.
- Configured `better` model tier (`ag.json:36`, `claude-opus-4-6`) does not resolve for this CLI; substituted `claude-opus-5/high` for this dispatch. Flagged as finding M-1 in the report — worth fixing the config so future rounds don't need this substitution.

## Questions (batched — each with a suggested default)

- What would you like to work on in `tw-writing`?
- Suggested default: none — this waits on your next message.
- ans:

- Should any of the review's 19 findings (invalid `better` model id, the 並行/並發/平行 table contradiction, the §16.2-vs-§4.5 可以 conflict, the 佔用/佔位符 mix, etc. — full list in `.agentflow/A-001-cross-check-review.md`) become actual follow-up work?
- Suggested default: no action now — revisit if/when you're next editing those sections.
- ans:

Cross-check review: `.agentflow/A-001-cross-check-review.md`
Cross-check implementation: fc53331145836bdb02461548b5081376d938839c

---

# → Ask / A-002

+ ag follow-up work on A-001-cross-check-review.md

+ skip-review: mechanical, git-reversible documentation/config fixes for the A-001 cross-check findings; host self-verified via grep sweeps (no stray 佔用, no stale model id, all 29 SKILL.md sections and § cross-references intact); owner declined the external narrow-tier cross-check dispatch given the direct-route choice already made to avoid external dispatch cost.

## [RUN-001] Event — 2026-09-12 14:29 (during round A-002)

- Route: direct (owner-confirmed via interactive question). A-002 opens with the explicit "ag" word, which per ag.md forces full_pipeline when allowed; ag.json has allow-ag: ask, so a complex route required recorded owner approval rather than silent selection either way.
- Owner chose direct route over full external pipeline given the work is markdown-only cleanup of the 19 A-001 cross-check findings in a repo with no build/test suite.
- Plan: apply mechanical/clearly-specified fixes directly; surface genuine judgment calls (M-3 table redesign scope, C-5 term classification, O-2 unverifiable external-tooling claims) as owner questions.

## [RUN-002] Event — 2026-09-12 14:44 (during round A-002)

- Applied direct-route fixes for 17 of 19 A-001 cross-check findings (M-1, M-2, M-3, M-4 partial, M-5, M-6, M-7, C-1 through C-9, O-1) across SKILL.md, CLAUDE.md, README.md, references/taiwan-terms.md, .gitignore, ag.json; bumped 0.2.0 -> 0.2.1 in CHANGELOG.md, plugin.json, marketplace.json per the projects own release-sync rule.
- Parked without action: remaining 4 self-referencing rows under M-4 (displays/crash/throughput/screenshot pairs, lower severity than the fixed concurrency row per the report own text) and part of M-8 (duplicate rows judged defensible by the report). Surfaced O-2 (unverifiable /skills command claim) as an owner question instead of guessing; verified the clone URL half of O-2 against git remote and it is correct, no change needed there.
- Self-verified with grep sweeps: no remaining bare 占用/占用 violations outside the rule tables and history, no stale claude-opus-4-6 id, all 29 SKILL.md sections and every found paragraph-sign cross-reference still resolve, section/H1 counts unchanged.
- skip-review: accepted tradeoff, owner-confirmed. Completion gate normally requires one external narrow-tier cross-check dispatch before closing; owner chose to skip it given the changes are mechanical, git-reversible, documentation/config-only edits already host-verified, consistent with the earlier direct-route choice that was made specifically to avoid external dispatch cost.

# ← Reply / A-002

* _2026-09-12 14:46:00 (Asia/Taipei)_ — Sonnet 5, Claude Code

## [SUMMARY]

- Route: direct, owner-confirmed. The "ag" trigger word would normally force full_pipeline, but `allow-ag: ask` required recorded approval first; owner chose direct route given the work is markdown-only, git-reversible cleanup.
- Fixed 17 of the 19 A-001 cross-check findings directly across `SKILL.md`, `CLAUDE.md`, `README.md`, `references/taiwan-terms.md`, `.gitignore`, `ag.json`.
- Bumped 0.2.0 to 0.2.1 in `CHANGELOG.md`, `plugin.json`, `marketplace.json` per the repo's own release-sync convention, since the rule-content changes are substantive enough to matter to guide users.
- Skipped the completion gate's external narrow-tier cross-check with owner's recorded `skip-review` (in the Ask text) — self-verified instead via targeted greps and structural checks.
- Noticed `ag.json`'s `allow-ag` changed from `ask` to `on` on disk mid-session, not made by this session — flagged below, not reverted.

## [FINAL REPORT]

### Fixed (17 of 19 findings)

| Finding | Fix |
|---|---|
| M-1 | `ag.json` `better` tier: `claude-opus-4-6/high` (invalid) changed to `claude-opus-5/medium`. STATUS's configuration line already read accurately, no change needed there. |
| M-2 | `.gitignore`: added `.worker-*.log`. |
| M-3 | Added a note at the top of `references/taiwan-terms.md` explaining identical-left/right rows mean already correct, do not flag them — smaller footprint than restructuring roughly 70 rows. |
| M-4 (partial) | Fixed the actively misleading pair: `並發`/`並行` rows now carry English glosses (concurrency/parallelism), the same device the file already uses elsewhere. The other four self-referencing rows (顯示器, 崩潰, 吞吐量, 截圖) are lower severity per the report's own text and have no single obvious fix; parked, see Open below. |
| M-5 | Added the missing `服務器` to `伺服器` row to the complete table, matching `SKILL.md` Section 11.1. |
| M-6 | Simplified the Simplified-character ripgrep command to one call, excluding the reference file itself from the match. |
| M-7 | `README.md`'s modify-the-rules checklist now points to `CLAUDE.md`'s (the more complete, canonical one) instead of maintaining a second, drifting copy; `CLAUDE.md`'s list gained the taiwan-terms.md update step that only `README.md`'s divergent copy had. |
| M-8 | Resolved via C-5 (the only inconsistent duplicate); the rest were judged defensible by the report itself, left as-is. |
| C-1 | Fixed the two actual violations: `README.md` and `CLAUDE.md`'s phrase about occupying context now use 占用 instead of 佔用. The rule itself (佔用 to 占用) was already correctly scoped to the word, not the character, so no rule change was needed. |
| C-2 | Section 22 heading changed from "not over-optimizing" wording to "not over-shortening" wording, more accurate to the section's actual subject, and removes the Section 11.1 conflict. |
| C-3 | Section 24 Examples 1 and 2 After-outputs no longer retain unnecessary 可以/我們, now consistent with Section 4.1 and Section 10.8's own worked examples. |
| C-4 | Added an explicit MAY/RFC-2119 carve-out to Section 4.5 and a pointer from Section 16.1, so 可以 survives when it renders a normative MAY. |
| C-5 | Removed 優化 from the different-meaning (同形異義詞) table in `references/taiwan-terms.md` — it does not fit that pattern (same meaning, just a style preference), and is already correctly classified as a plain substitution elsewhere. |
| C-6 | Scoped the em-dash-doubling rule (`SKILL.md` Section 14.5 and `references/taiwan-terms.md`) to sentence-internal use; heading label separators like "Pass 1 — Structure" are now explicitly exempted. |
| C-7 | Moved Section 25 MUST items 8-9 (negative prohibitions) into MUST NOT, resolving both the polarity mismatch and the strength conflict with the existing SHOULD-NOT-shaped duplicate. |
| C-8 | The 傳送門 replacement column now gives concrete alternatives instead of a vague placeholder note. |
| C-9 | `CLAUDE.md`'s numbering-convention line now says numbered subsections use the N.M format, explicitly carving out Section 23/24's unnumbered Pass-N/Example-N headings. |
| O-1 | `30°C` relabeled from angle to degree symbol at both `SKILL.md` locations, with a real angle example added. |

### Verified, not changed

- O-2 (clone URL half): checked `git remote -v`, which returned `git@github.com:kirinlin/tw-writing.git`, matching the `github.com/kirinlin/tw-writing` URL in `README.md` exactly. No fix needed.

### Parked (2 items, genuine judgment calls, not decided unilaterally)

- M-4, remaining 4 rows (screen/monitor, crash, throughput, screenshot pairs): each repeats its own avoid-term in the use-column to mean also acceptable, which is technically self-contradictory under the table's stated contract, even though a reader would likely parse it correctly. The report did not specify a concrete fix for these the way it did for the concurrency row, and reformatting the whole class of rows is a real design decision. Left as-is.
- O-2, the slash-skills command claim in `README.md`'s onboarding instructions: this session does not have reliable confirmation that this is a current Claude Code slash command. Flagged as a question below rather than guessed at.

### Self-verification performed

- Grepped the whole repo for the banned character: only the review/devlog history (legitimate, describing past state) and the rule tables themselves remain, both correct.
- Grepped for the stale model id: no hits.
- Grepped for the old section heading text: no hits, renamed cleanly.
- Confirmed `SKILL.md` still has exactly one H1 and 29 numbered sections.
- Extracted every section cross-reference across `SKILL.md`, `README.md`, `CLAUDE.md`, `CHANGELOG.md` post-edit; all resolve to sections that exist.
- Checked all newly added Traditional Chinese prose against `SKILL.md`'s own rules (CJK/Latin spacing, full-width vs half-width punctuation, no unnecessary first-person plural or hedging) per the dogfooding requirement in `CLAUDE.md`.

### Note: ag.json changed on disk mid-session, not by this session

Partway through this round, `ag.json`'s `switches.allow-ag` changed from `ask` to `on` on disk. This session did not make that change; none of the commands run here touch that field. Surfacing it rather than reverting it, per instruction to treat unexplained changes as possibly deliberate and flag rather than undo. Practically: this means a future ag/agentflow/all-in trigger will no longer stop to ask before running the full external-dispatch pipeline. Worth confirming this was an intentional edit.

## Questions (batched — each with a suggested default)

- Is there a current Claude Code command that lists loaded Skills, matching what `README.md` tells new users to run to confirm `tw-writing` loaded? This session cannot verify that claim offline.
- Suggested default: leave the line as-is until confirmed one way or the other; if wrong, the fix is a one-line wording change pointing at whatever the actual skill-listing UI or command is.
- ans:

- Was the change to `ag.json`'s `allow-ag` (from `ask` to `on`) during this session intentional?
- Suggested default: confirm it was intentional and leave it; if not, set it back to `ask`.
- ans:

- Want the remaining 4 self-referencing rows in `references/taiwan-terms.md` (the lower-severity half of M-4) reformatted now, or left parked?
- Suggested default: leave parked — they are not actively misleading the way the concurrency row was, and the right reformatting is a style call, not a mechanical fix.
- ans:

Implementation: uncommitted working-tree changes (10 files), not yet committed or pushed.

---

# → Ask / A-003

+ If I want this SKILL can work with `sysprog21/zhtw-mcp`, how to achive it?

## [RUN-001] Event — 2026-09-12 17:14 (during round A-003)

- Route: direct. Owner asked how to integrate this Skill with the external sysprog21/zhtw-mcp MCP tool (a Rust zh-TW linguistic linter); researched the tool via `gh api repos/sysprog21/zhtw-mcp/readme`, then asked the owner (AskUserQuestion) which integration level to build. Owner chose "Active rule in SKILL.md" — a conditional rule calling `zhtw` as a final mechanical check when available.
- Plan: add §25 "外部工具（若可用）" subsection and matching §26 checklist item, §1.4 relationship note, README mention, following CLAUDE.md's 8-step "修改規範時" protocol; bump 0.2.1 -> 0.3.0.

## [RUN-002] Event — 2026-09-12 17:20 (during round A-003)

- Implemented the change across SKILL.md (§25 new subsection, §26 checklist item, §1.4 note), README.md, CHANGELOG.md, .claude-plugin/plugin.json, .claude-plugin/marketplace.json (0.2.1 -> 0.3.0).
- cross-check-plan.js facts (changed_files: 5, changed_lines: 29, behavior/trust/broad/consequential: false) selected level: targeted.
- Dispatched external read-only reviewer (external-runner-v1: disposable no-remote clone, `claude -p --restricted`, claude-opus-5/medium, the `better` tier) against the candidate diff. Round 1 result: Outcome BLOCKING — the "apply zhtw suggestions directly" bullet was unscoped over a range that swallowed §11/§12/§14, which could let the Agent corrupt code samples or rename identifiers in violation of §14.6 and MUST NOT 8/11 (both stated as having no exceptions). Six non-blocking findings also raised (introduced synonym vs. established term, a 頓號 error, checklist header inconsistency, discouraged 破折號, 公文腔 pronoun, README section mismatch).
- Applied the fix: scoped the "apply directly" bullet to prose only, added an explicit exception-free carve-out for code/identifiers citing §14.6 and MUST NOT 8/11, replaced the fragile §-range with prose, and applied all six non-blocking fixes.
- Re-dispatched a fresh disposable-clone reviewer (round 2, same tier) to verify the fix. Result: Outcome/Minimality/Conformance all PASS. Two further non-blocking cosmetic findings (checklist item lost its own "(若可用)" marker after header simplification; CHANGELOG quoted a now-changed heading string) were fixed directly without a third review round, since the reviewer itself classified them as non-correctness drift.
- Committed implementation as da340f8 with Assisted-by trailer (this repo's git-attribution hook requires it; rejected the Claude-Session trailer form). Saved the full two-round review record at .agentflow/A-003-cross-check-review.md.
- Host gate: PASS.

# ← Reply / A-003

* _2026-09-12 17:19:00 (Asia/Taipei)_ — Sonnet 5, Claude Code

## [SUMMARY]

- Owner asked how to make this Skill work with `sysprog21/zhtw-mcp` (an external MCP linter for zh-TW). Researched the tool, presented three integration options, owner chose "active rule in SKILL.md."
- Added a conditional §25 subsection so the Agent calls `zhtw` as a final mechanical check when the tool is present in the environment, with an explicit no-exception carve-out for code/identifiers; the Skill still works with no behavior change when `zhtw` is absent.
- Two-round external cross-check: round 1 found a real BLOCKING defect (the rule could have let `zhtw` override the code-punctuation and identifier-spelling protections in §14.6/§25 MUST NOT); fixed, and round 2 returned PASS/PASS/PASS.
- Bumped 0.2.1 -> 0.3.0 (CHANGELOG, plugin.json, marketplace.json) and committed as `da340f8`. Not yet pushed to origin.

## [FINAL REPORT]

### Task: "If I want this SKILL can work with `sysprog21/zhtw-mcp`, how to achive it?"

**Answered, then implemented per the owner's chosen option.**

`zhtw-mcp` and this Skill operate at different layers: `zhtw` is a Rust MCP server that mechanically lints zh-TW text against ~1100 vocabulary rules, MoE punctuation/character-shape standards, and cross-strait terminology, with auto-fix; `SKILL.md` is a knowledge document shaping generation/judgment (structure, clarity, tone, spacing conventions) that a rule-based linter cannot do. I presented three integration levels (no repo change / passive README documentation / active SKILL.md rule) and the owner picked the active rule.

**Implementation**, all in commit `da340f8`:

- `SKILL.md` §25 gained a new "外部工具（若可用）" subsection: when `zhtw` is available, the Agent calls it after the §23 six Passes for punctuation/字形/中國大陸用語 (mechanical categories), applies its suggestions directly for prose, but gives code blocks, inline code, API names, and identifiers an explicit, exception-free priority over `zhtw` (citing §14.6 and MUST NOT 8/11) — this carve-out exists specifically because of a defect the external review caught (see below). `zhtw` never overrides the Skill's own semantic-layer judgment (structure/clarity/concision/tone), and the step is skipped entirely when the tool is absent — no new hard dependency.
- `SKILL.md` §26's final checklist and §1.4's file table got matching entries/notes; `README.md` documents the pairing under 使用方式.
- Version bumped 0.2.1 → 0.3.0 across `CHANGELOG.md`, `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, following `CLAUDE.md`'s 8-step "修改規範時" protocol.

**External cross-check** (this change touches `SKILL.md`/`README.md`/`CHANGELOG.md`, so the completion gate applied; cross-check-plan.js selected "targeted" level): two rounds, each a fresh disposable no-remote git clone reviewed read-only by `claude -p --restricted` at `claude-opus-5/medium`.

- Round 1 reported the outcome dimension as blocking: the first draft's rule told the Agent to apply `zhtw`'s suggestions directly across a range that included the sections governing code-block punctuation and identifier spelling — both of which `SKILL.md` itself states have *no exceptions* (§14.6, §25 MUST NOT 8/11). Since `zhtw` has no guaranteed awareness of Markdown fences or identifiers, this could have made the Agent corrupt a code sample or rename an API under a future `zhtw`-integration round. Six non-blocking findings also came back (an introduced synonym competing with the document's established term, a 頓號 grammar slip, a checklist-header inconsistency, a discouraged mid-sentence dash, a 公文腔 pronoun, a README section mismatch).
- Fixed all seven findings, including the exception-free code/identifier carve-out.
- Round 2 confirmed all three dimensions passing. Two further cosmetic (non-blocking) observations came back and were fixed directly without a third round.

Cross-check review: `.agentflow/A-003-cross-check-review.md`
Cross-check implementation: da340f8b271fe2aa273553e44ce19828b2694c9a

**Status:** committed (`da340f8`); not yet pushed — I did not push without asking, since that's a shared/visible action.

## Questions (batched — each with a suggested default)

- Push `da340f8` to `origin/int/zhtw-mcp` now?
- Suggested default: yes — it's a normal, reviewed, git-reversible documentation change with no open concerns.
- ans:

Implementation: committed as `da340f8`, working tree otherwise clean apart from this devlog round.

---

# → Ask / A-004

s/中國大陸用語/中國用語/g

## [RUN-001] Event — 2026-09-13 (during round A-004)

- Route: direct. Global terminology rename `s/中國大陸用語/中國用語/g` across SKILL.md, README.md, CHANGELOG.md, CLAUDE.md, references/taiwan-terms.md, and both plugin manifests (34 occurrences found, 31 replaced across 7 files). Left `.agentflow/devlog.md` and `.agentflow/A-003-cross-check-review.md` unchanged — those are historical review records quoting the old term as it stood at the time; rewriting them would misrepresent history.
- cross-check-plan.js facts (changed_files: 7, changed_lines: 62, behavior/trust/broad/consequential: false) selected level: targeted (two of the seven changed files are `.json` manifests, so the change is not documentation-only by the tool's pattern, even though it is a pure text substitution).
- Committed as 627080e with Assisted-by trailer.

## [RUN-002] Event — 2026-09-13 (during round A-004)

- Dispatched external read-only reviewer (external-runner-v1: disposable no-remote clone, `claude -p --restricted --permission-prompts none`, claude-opus-5/medium, the `better` tier) against implementation commit 627080e, one round, targeted level. Diff embedded verbatim in the prompt (from `git show`) since `--restricted` removes Bash. Result: Outcome/Minimality/Conformance all PASS; clone unmodified (no writes); exit 0.
- Non-blocking observation raised: several nearby-but-different strings using the longer `中國大陸` prefix (`中國大陸慣用術語`, `中國大陸語意`, etc. in SKILL.md/CHANGELOG.md/references/taiwan-terms.md) were correctly left untouched — different exact string than the Ask targeted, so touching them would be scope creep. Parked for the owner, not actioned.
- Host gate: PASS. Independently re-ran `rg 中國大陸` against the working tree and confirmed every location the reviewer cited is real.
- Saved review record at .agentflow/A-004-cross-check-review.md; removed working scratch files (brief, diff) not meant for the committed repo.

# ← Reply / A-004

* _2026-09-13 09:45 (Sonnet 5)_

## [SUMMARY]

- Renamed `中國大陸用語` → `中國用語` across SKILL.md, README.md, CHANGELOG.md, CLAUDE.md, references/taiwan-terms.md, and both plugin manifests. Historical `.agentflow` logs left untouched.
- Committed as `627080e`. Targeted-level external cross-check: Outcome/Minimality/Conformance all PASS. Host gate: PASS.
- One non-blocking observation parked below (not part of this Ask).

## [FINAL REPORT]

### Task: `ad s/中國大陸用語/中國用語/g` — global rename

**Succeeded.**

Found 34 occurrences across 9 files. Replaced 31 of them (7 files: `SKILL.md`, `README.md`, `CHANGELOG.md`, `CLAUDE.md`, `references/taiwan-terms.md`, `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`). Deliberately left 3 occurrences in `.agentflow/devlog.md` and `.agentflow/A-003-cross-check-review.md` unchanged — those are historical review-round logs quoting the old term as it stood at the time; rewriting them would misrepresent history rather than serve the rename.

Committed as `627080e` with an `Assisted-by: Claude:claude-sonnet-5` trailer (this repo's git-attribution hook rejects the `Claude-Session:` trailer form and requires `Assisted-by` instead).

**Cross-check** (changed source/config touched the completion gate; cross-check-plan.js selected "targeted", since two of the seven changed files are `.json` manifests and so the change isn't "documentation-only" by the tool's own file-pattern check, even though it is a pure text substitution): one round, a fresh disposable no-remote clone reviewed read-only by `claude -p --restricted` at `claude-opus-5/medium`. Outcome/Minimality/Conformance all PASS on the first round; no rework needed.

Cross-check review: .agentflow/A-004-cross-check-review.md
Cross-check implementation: 627080e85b39071716de164462c251185f32dfd8

**Parked (not actioned — outside this Ask's scope):** the reviewer flagged that the repo still uses the longer, differently-worded `中國大陸` prefix in a handful of places — `中國大陸慣用術語` (SKILL.md:844, 1851), `中國大陸語意` (SKILL.md:897, references/taiwan-terms.md:15), and the descriptive prose in references/taiwan-terms.md (lines 5, 7, 13, 446) and CHANGELOG.md:42 that explains the table convention. These are a different exact string than the one this Ask's sed command targeted, so leaving them untouched is correct minimality — but if you'd like the same shortening applied there too, say so and I'll do a follow-up round.

**Status:** committed (`627080e`); not yet pushed — a normal reviewed documentation change with no open concerns, but push is a shared/visible action I don't take without confirmation.

## Questions (batched — each with a suggested default)

- Push `627080e` to `origin/main` now?
- Suggested default: yes — it's a small, reviewed, git-reversible documentation change with no open concerns.
- ans:

- Should the parked `中國大陸` occurrences (a different string from what this Ask targeted) also be shortened to match, in a follow-up?
- Suggested default: no — leave them as-is unless you specifically want that broader consistency pass; they weren't part of this Ask.
- ans:

---

# → Ask / A-005

+
