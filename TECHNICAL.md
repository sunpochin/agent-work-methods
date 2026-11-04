<!-- 檔案用途：先解釋使用方法，再記錄邊界與取捨。所在層：設計文件。主要關聯：README.md、docs/ADOPTION.md、docs/AI_WORKFLOWS.md、docs/VALIDATION.md。 -->
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

Issue #3 records [a pinned comparison, trial recommendation and workspace evidence](docs/TOOL_EVALUATION.md). Source inspection of Superpowers v7.0.1, BMad Method v6.12.4 and Spec Kit v1.2.6 supports trying Spec Kit's official Lean preset first. Its small artifact sequence and optional Git/agent-context extensions appear to require fewer changes to the existing product workflow. This is an inference from text, not measured compatibility or adoption; extra spec/plan/task maintenance may outweigh its benefit. Other workspace/orchestration products are deferred until an observed need.

Product-specific rules establish a need to check configuration and acceptance, not a need for an AWM layer. Existing workflows already cover planning, tasks, implementation, checks, review and handoff. First inspect their configuration, templates and extensions against the owning AGENTS.md, tests and PR rules. No new task contract, workflow, adapter, executable helper or skill is a required deliverable.

Acceptable outcomes are direct adoption, configuration only, a small custom supplement, or keeping the current workflow. AWM may retain only the decision, pinned versions and necessary project notes; no new shared process is also a valid result. Adapter, Strategy and Facade are not assumed architecture. A second integration or repeated settings alone do not justify shared code. Consider custom work only for recurring, reproduced gaps that configuration and feasible upstream improvements cannot resolve, with a separately reviewed scope and maintenance cost.

Source inspection distinguishes instructions, existing customization keys, execution evidence and unknowns. Superpowers' inline path still includes final review and workspace cleanup; BMad's release-specific overrides do not by themselves prove local no-push/dispatch conflicts resolved. Spec Kit Lean is not the core plan, which instructs research-agent dispatch. A constitution should point to the product's AGENTS.md as authority, without duplicating policy. The initial source-comparison pass installed no candidate and performed no complete installer/hook audit.

The later Dance Stamp #249 / PR #250 pilot used Spec Kit v1.2.6 with official Lean v1.0.0, local settings and explicit generated-skill loading. It completed a diagnostic-message fix through existing checks and PR rules, but those boundaries remained product/tool/manual responsibilities. Extra spec/plan/tasks and evidence exceeded the tiny code change; no causal time or cost saving was demonstrated. Keep the native workflow for similar small fixes. The comparison links the exact head, CI, preserved fixture-isolation failure and subsequent merge separately. Generated activation files were removed; no shared adapter, runtime, dependency update or product migration follows from this single sample. jia-jian-log and larger-task value remain untested.

The comparison separately records jia-jian-log PR #1401 at its exact head/base: confirmed task-clone support and synthetic independent-clone/submodule tests remain in an open, unmerged product PR. CI success and a completed bot summary coexist with a pending review status. This does not change staging policy or establish candidate execution, linked-worktree/submodule support, arbitrary desktop clone attachment or Mission Control acceptance. The two products' v0.1.0 lock manifests match; their 33 upstream files were not rehashed in this pass.

Submodules can replace a manual per-file version manifest with a Git commit pin, but initialization, source/commit availability, dirty-tree detection, integrity checks, CI and public scanning still need product-specific review. Relaxing workspace policy supplies a clone alternative; it does not fix linked worktrees with submodules. Keep pinned copies for now and decide how much shared AWM content is useful before changing distribution. Use only necessary synthetic cases before an authorized product trial; no new test framework is a prerequisite. Package checks establish documentation/bundle structure, not independent behavioral review or adoption benefits.

## AI workflows, skills, and framework inventory

<!-- 說明為何建立專門清單：記錄專案生態系所用之 AI 工作流與框架（Spec Kit、pstack、gstack、gbrain、AWM 等），釐清選型邊界與借鑑要點，避免重蹈過度工程化覆轍。 -->
For a consolidated inventory of workflows, skills, and frameworks used, piloted, or referenced across this collection and adopting products (including GitHub Spec Kit, pstack, gstack, gbrain, Superpowers, BMad Method, Serena, and our two-tier agent hierarchy), see [AI Workflows & Frameworks](docs/AI_WORKFLOWS.md).

### Design decisions and rejected alternatives

- **Verification-First and Thin Adapters over Heavy Runtimes**: We rejected incorporating heavy autonomous multi-agent orchestration frameworks (such as BMad or Superpowers' default runtime) into the shared core. These introduce unwanted assumptions (e.g., hardcoded `npm install` or destructive `rm -rf` operations) that violate our project safety constitution and package manager baselines. Instead, we keep the core AWM skills purely text-based and zero-dependency, adhering to the Agent Skills specification.
- **Pragmatic Borrowing from pstack**: Rather than taking on pstack as an all-or-nothing external plugin dependency, we adopt its core engineering tenets—specifically "Go deep first, then fast", the Laziness Protocol (minimal blast radius), and rigorous verification against real running environments (Prove It Works). This directly informs our `awm-debugging` and `awm-review-evidence` methods.
- **Borrowing Role Review from gstack and Graph Navigation from gbrain**: Garry Tan's `gstack` models an end-to-end engineering team (e.g. founder/CEO reviews with `/plan-ceo-review`, security reviews with `/cso`), while `gbrain` models persistent cross-session memory and call graph traversal (`code-callers`). We embrace these conceptual checks in our review and debugging skills, but reject requiring external database daemons (Postgres/PGLite) or a heavy suite of 20+ custom slash commands for core operations. Instead, we use Git receipts and Markdown records (`TECHNICAL.md`) as our zero-infrastructure persistent memory.
- **Spec Kit Lean Trial Conclusions**: As confirmed in Dance Stamp #249 / PR #250, structured spec-driven development (`spec.md` -> `plan.md` -> `tasks.md`) has high documentation overhead for small patches without measurable speed or token savings. We reserve formal spec-driven workflows for major multi-component features or cross-team interfaces, keeping native lightweight workflows for everyday defect resolution.
