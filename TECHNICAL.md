<!-- 檔案用途：先解釋使用方法，再記錄邊界與取捨。所在層：設計文件。主要關聯：README.md、docs/ADOPTION.md、docs/VALIDATION.md。 -->
# 設計與取捨 / Design decisions

## 怎麼用、為什麼有效

像拿一本只教做法的小手冊：挑這次需要的方法，把整個資料夾帶進自己的專案，再照自己的規則操作。手冊提醒你找入口、重現問題、留下證據，但不決定產品怎麼部署或誰能合併。

每個資料夾都有完整參考與授權，單取一個也不缺頁。固定版本讓你知道目前採用了哪套方法，更新時能先看差異。

## Packaging and policy

Five text-only skills use standard `SKILL.md` frontmatter and one-level, skill-local references. Short instructions route to reasoning and examples on demand. Each includes LICENSE and NOTICE.md so an individual copy preserves its distribution context; this small duplication of legal text is intentional.

Root documentation supports adoption and maintenance, not mandatory consumer rules. There is no installer, plugin, remote fetch, global symlink, auto-update or executable skill helper. Branch targets, push policy, language, framework, storage contracts, acceptance thresholds and publication authority stay local.

Provenance records the MIT baseline. Methods are rewritten from that source, rather than copied from later product-specific derivatives. No application, database, deployment, incident or credential material is imported.

## Validation

`scripts/check.py` and `tests/test_bundle.py` use Python's standard library. The checker validates the narrow frontmatter used here (JSON-quoted YAML scalars), required files, names, independent links, unsafe paths and common accidental disclosures. It is not a general YAML parser or proof of trustworthy instructions. The skill-authoring validator also checks frontmatter during initial preparation; it is not a consumer dependency.

Tests copy individual skills into unrelated synthetic layouts. Negative cases remove a reference, add an escaped path or symlink, introduce a source-product dependency, and include a synthetic secret. Maintainer walkthroughs inspect realistic tasks; they do not measure agent effectiveness. See [validation](docs/VALIDATION.md).

## Rejected alternatives

- A full archive would carry unrelated assumptions; only five concrete workflows are included.
- Live shared rules or cross-repository links create external-state dependencies. Complete pinned copies preserve independent operation.
- An installer/synchronizer needs more permissions and conflict handling than this version requires. Adoption uses explicit copies and reviewed updates.
- A universal constitution turns local choices into rules for strangers. This collection is a selectable library of methods.

## Evaluate existing capabilities before adding a runtime

Issue #3 evaluates [existing workflows and feasibility in two products](docs/TOOL_EVALUATION.md). Compare Superpowers, BMad Method and Spec Kit against the existing workflow, then select one for an authorized small trial in each product. Other workspace/orchestration products are considered only for an observed need. No candidate has been selected or tested yet.

Product-specific rules establish a need to check configuration and acceptance, not a need for an AWM layer. Existing workflows already cover planning, tasks, implementation, checks, review and handoff. First inspect their configuration, templates and extensions against the owning AGENTS.md, tests and PR rules. No new task contract, workflow, adapter, executable helper or skill is a required deliverable.

Acceptable outcomes are direct adoption, configuration only, a small custom supplement, or keeping the current workflow. AWM may retain only the decision, pinned versions and necessary project notes; no new shared process is also a valid result. Adapter, Strategy and Facade are not assumed architecture. A second integration or repeated settings alone do not justify shared code. Consider custom work only for recurring, reproduced gaps that configuration and feasible upstream improvements cannot resolve, with a separately reviewed scope and maintenance cost.

Source inspection identifies candidate conflicts around setup, fallback isolation, recovery, cleanup and tool interfaces, not proven unconfigurable defects. Use relevant synthetic cases only where needed before the product trial; do not build a new test framework as a prerequisite. All candidate trials remain unperformed. Package checks validate this repository's documentation and existing bundle, not tool compatibility or adoption benefits.
