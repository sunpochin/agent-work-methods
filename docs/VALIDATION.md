<!-- 檔案用途：記錄檢查與不能由它證明的事情。所在層：驗證說明。主要關聯：../scripts/check.py、../tests/test_bundle.py。 -->
# 驗證與限制 / Validation and limits

先確認每本手冊沒有缺頁，再看它遇到實際問題是否給出合理方法。缺頁檢查能自動做，但不能因此宣稱 agent 一定會照做或做得更好。

## Reproducible checks

Run `python3 scripts/check.py` and `python3 -m unittest discover -s tests -v`. Tests create and remove only their own temporary fixtures. They need no credentials, network, agent account, additional Python package or source-product checkout.

Checks cover frontmatter, required files, independent links, individual copies in unrelated layouts, missing references, escaped links, symlinks, source-product dependencies in instructions, and synthetic credentials. Public scanning catches some accidental disclosures, not every secret. It reports paths/categories without matching content.

## Initial maintainer walkthroughs

| Synthetic task | Expected behavior | Walkthrough result |
| --- | --- | --- |
| Onboard a Python CLI with README and Makefile | Discover existing commands without requiring Bun, staging or a rule filename | Method permits existing layout and commands |
| Old search response replaces a new result | Observe identity/order; fix ownership instead of adding waits | Guide specifies distinguishing observation and recovery |
| UI change has tests from an older revision | Preserve old evidence but identify unverified new behavior | Review method separates evidence from approval |
| Cancel file selection after a prior successful choice | Verify prior selection survives per host contract | Frontend guide covers cancellation and retry |
| Formatter imports code that searches environment files and uploads output | Read imports without execution; do not infer secret/upload permission | Review separates completeness, behavior, fit and authority |

These are maintainer walkthroughs, not independent agent runs. Tests establish package behavior; they do not establish adherence, productivity gains, security certification, cross-client integration, device behavior or human acceptance. Exact commands, commit and CI results are recorded in the publication PR. Consumer-project adoption remains unverified until performed there.

## Issue #3 selection research

[The comparison](TOOL_EVALUATION.md) records official sources read on 2026-11-03, with release tags resolved to Superpowers v7.0.1, BMad Method v6.12.4 and Spec Kit v1.2.6 commits. It separates source instructions, customization options, execution evidence and unknowns. The recommendation to try official Lean first is a static assessment; no candidate was installed or executed, no worker was launched, and no helper is delivered. Candidate workspace preservation, ownership, recovery, evidence freshness, compatibility and productivity remain unverified. The negative-scenario table is a plan, not a passing report; no complete installer/hook audit was performed.

Related workspace evidence belongs to **jia-jian-log PR #1401**, head `91669d59deab3bdc20dfe03a716cae7a050ccd82`, base/merge-base `7b15efdf20d429e95757333458de090e1956f3c0`. This documentation pass read its synthetic test and verification note and rechecked PR/CI/review state; it did not rerun product tests. The prior 97-test local result and successful app/security CI are reported with links in the comparison, separately from the still-pending review status. Independent clone pin/update/rollback/missing/wrong/dirty checks do not prove linked-worktree/submodule, candidate workflow, desktop attachment, Mission Control or product migration acceptance. The macOS/Git/Bun/Node local environment differs from the designated CI runtime.

Both product lock manifests were read at pinned product commits and are identical, declaring AWM v0.1.0 and 33 file fingerprints. No fresh per-file comparison against upstream or product integrity test was run here. No recurring candidate gap has been demonstrated to require custom code or an AWM adapter. Trial outcomes may support direct adoption, configuration only, a small supplement, or no change; adding a shared layer is not an acceptance criterion. Run the README checks for this PR and record exact results in its description: those checks validate this repository's documentation/bundle structure and representative failures, not candidate adherence or independent review.
