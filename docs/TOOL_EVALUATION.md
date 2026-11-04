<!-- 檔案用途：先比較現成方案，再以可重跑證據決定是否補工具。所在層：選型研究與試用計畫，非安裝規則。主要關聯：ADOPTION.md、AI_WORKFLOWS.md、VALIDATION.md、../TECHNICAL.md。 -->
# 評估現成流程並驗證兩產品採用可行性

規劃、拆任務、執行、測試、審查與交接已有現成流程。像先比較三本工作手冊，再挑一本用小作業試試看；專案原本的規矩仍算數。此階段以既有 Codex 工作方式作基準，比較 Superpowers、BMad Method 與 Spec Kit 如何容納既有 AGENTS.md、測試與 PR 規則。產品有自己的規則，只能推導出需要核對設定與驗收，不能直接推導成需要新流程、共用契約或 Adapter。

**2026-11-03（Asia/Taipei）收斂狀態：來源比較後，已在 Dance Stamp 完成官方 Lean 的一項小任務試用；局部設定與顯式載入可用，這類小修正建議維持原生流程，沒有更快或更省的證據。** jia-jian-log 尚未試用，Superpowers／BMad 尚未執行；不正式擴大採用、不新增共用層或遷移副本。既有五個 skills 與 v0.1.0 套件不變；先前未驗證的自建草稿不納入交付或預定成果。

本文件對應 [共用主票 #3](https://github.com/sunpochin/agent-work-methods/issues/3)；產品試用分別由 [Dance Stamp #246](https://github.com/sunpochin/dance-stamp/issues/246) 與 [jia-jian-log #1399](https://github.com/sunpochin/jia-jian-log/issues/1399) 追蹤。這些關聯是維護計畫，不會安裝到個別 skill 或成為其他專案的政策。

## 第一項試用結果與後續決策

像先借一本新手冊做一題小作業：照著做能完成，但為了一小題多寫好幾頁紀錄，還不能說比較划算。因此同類小修正先沿用原本做法；是否值得用於較大的規劃任務，需要另一項獨立試驗。

- **來源與任務：** [Dance Stamp #249／PR #250](https://github.com/sunpochin/dance-stamp/pull/250) 只修正 AWM 固定副本漂移提示，不再暗示可就地修改指紋。實際使用 Spec Kit CLI v1.2.6／來源 `9eacc24ffe47eadf035a3af601e4dabfb15b8fde`、官方 Lean preset v1.0.0；未啟用 Git／agent-context extensions。constitution 只指向產品權威，生成的四份指示以顯式讀檔載入，依序產生 spec／plan／tasks 並執行；未驗證 UI 自動發現。
- **版本與結果：** 程式／測試 commit `e26f476d518d72ec606ef004f27c332b74041ef6`，最終文件 head `809ce22d1f585e63e4b52173e8b1e2099da5d818`，原 base `acea4b9d52ad1b7aaa7db2ba1e5b8c070a567b74`。[repo 內試用紀錄](https://github.com/sunpochin/dance-stamp/blob/809ce22d1f585e63e4b52173e8b1e2099da5d818/docs/evidence/issue-249-spec-kit-lean.md) 保存設定、雜湊、步驟與失敗；[最終收據](https://github.com/sunpochin/dance-stamp/pull/250#issuecomment-6593946972) 記錄 Bun 1.4.4 完整 check／正常 hook 的 761 pass、0 fail，以及[最終 head CI](https://github.com/sunpochin/dance-stamp/actions/runs/41566576656) success。最初測試曾因繼承 Git hook 環境誤改共同 `core.bare`；已還原並隔離 fixture 環境，失敗與返工仍留在紀錄，不能宣稱全程無副作用。
- **採用結論：** 局部設定可容納此任務的既有分支、Bun、測試與 PR 流程；這些仍靠產品既有工具與人工核對，不是 Lean 自動強制。額外三份文件與試用證據多於修正本身；單一樣本、非因果對照，費用 unknown。同 session 接手不代表跨聊天／重啟恢復；錯工作區、他人髒檔、完整負向矩陣及兩產品相容性仍未證實。不推導為需要 Adapter 或 framework。
- **目前狀態：** 生成的啟用檔已停用，只保留證據，產品 AWM 副本未改。GitHub 記錄 #250 已由 `sunpochin` 帳號於 2026-11-03 04:50:09 UTC 合併，merge SHA `d77cea14d8c75f2af0b1e3868d7ba0dd4009ca27`；與試用當次「停在 PR」的歷史交付分開。本次收斂未執行合併或部署，也未代簽合併後／真機／真人驗收。

下列候選比較、產品基線與負向情境清單保留為**試用前的來源評估快照**；「本輪未安裝／未試跑／未重跑」指該來源評估階段，現行執行結果以上節及產品精確版本證據為準。清單不是整套通過報告，不能由這一項試用推成所有情境已完成。

## 暫定建議與未選其他方案的原因

**先試官方 Lean，保留既有工作區、測試、push、PR 與審查入口。** 理由是該版已有精簡的 spec → plan → tasks → implement 檔案流程，Git 管理與 agent-context 同步又是選用擴充，靜態看來需改動的既有流程較少。這是根據下列來源的推論，不是已測試相容、必然較好或已獲准安裝。constitution 應引用各產品 AGENTS.md 作權威，不抄出第二份競爭政策。實際小任務、工時／費用預算與停止條件仍待各產品另定與授權。

| 候選 | 本輪試用順序與取捨 |
| --- | --- |
| **Spec Kit v1.2.6／官方 Lean** | 優先提議一項單線小任務。額外 `spec.md`／`plan.md`／`tasks.md` 與 feature 指標仍有維護成本；若不能減少接手、返工或審查負擔，維持現狀即可。 |
| **Superpowers v7.0.1** | 暫緩優先試用。已有本地指示優先與同 session 執行路徑，但依賴安裝、隔離失敗回退、最終 reviewer 及暫存清理預設需逐一對應產品限制；不能只切 inline 就宣稱符合單線／保全要求。 |
| **BMad Method v6.12.4** | 暫緩優先試用。現成覆寫較完整，適合另有完整規格／審查需求時再考慮；目前 default full／oneshot 的派工、審查與 no-push 行為需處理，尚無證據顯示其設定及文件成本值得。 |

Conductor／Agent Orchestrator 不在本輪優先三者，也不是必裝配件；只有實測顯示另需協作介面或調度才重開評估。本次沒有重新審它們的完整來源。既有 Codex 工作方式只作基準，本輪未測用戶端工作區／Handoff 功能。

## 不預設 AWM 必須新增一層

外部方案是候選清單，**不需要全部接上**。先看選定方案已有的設定、範本、專案指示與擴充方式；沿用其紀錄及現有 issue／PR 證據，不預先建立 AWM 的任務格式、狀態機或派工入口。

AWM 可能只需保存選型結果、實際固定版本與少量專案補充，也可能完全不需要新增共用流程。評估結果允許四種，按實際證據選擇：

1. **直接採用：** 現成流程已能容納本地規則，保留必要的版本與驗收紀錄。
2. **只需設定：** 用工具既有設定、範本或專案指示完成，記錄差異與回復方式。
3. **自建少量補充：** 僅限反覆出現、設定與上游改善路徑仍無法解決的具體缺口；另外審查最小範圍、成本與授權。
4. **維持現狀：** 沒有足夠收益、成本過高或不相容時，保留現有流程也是完整的決策成果。

產品直接提供規則給選定流程。例如一般 PR 的目標在兩產品分別是 main 與 staging，應核對工具是否能透過既有設定遵守，而不是先在兩者之間加入自建轉接層。

Adapter、Strategy、Facade 都不是本票預定架構或完成條件。即使第二個工具需要使用、出現相似設定，也不足以直接證明要抽共用程式。先能設定就設定，適合由上游解決就整理可重現回報；只有反覆發生且確實無法解決的缺口才考慮少量自建。本輪未向上游發文。

## 固定來源與證據分層

2026-11-03 已從官方 GitHub tag 物件解參照至下列 commit；只把來源當研究資料，未執行其中指令。release／commit 是閱讀基準，**不是實際安裝版本**；之後另記 App／CLI／plugin、設定及環境，不以 marketplace 或移動中的 main 代替固定來源。

| 方案 | 官方 release | 本輪來源 commit |
| --- | --- | --- |
| Superpowers | [v7.0.1](https://github.com/obra/superpowers/releases/tag/v7.0.1) | [`2ce8aa15d05bd57213e6f746f953aafb7ded7a8b`](https://github.com/obra/superpowers/tree/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b) |
| BMad Method | [v6.12.4](https://github.com/bmad-code-org/BMAD-METHOD/releases/tag/v6.12.4) | [`bab9082c3e884e0d72c759bcd1a6d90bcc01be84`](https://github.com/bmad-code-org/BMAD-METHOD/tree/bab9082c3e884e0d72c759bcd1a6d90bcc01be84) |
| GitHub Spec Kit | [v1.2.6](https://github.com/github/spec-kit/releases/tag/v1.2.6) | [`9eacc24ffe47eadf035a3af601e4dabfb15b8fde`](https://github.com/github/spec-kit/tree/9eacc24ffe47eadf035a3af601e4dabfb15b8fde) |

四類證據分開：**靜態指示**只證明來源要求什麼；**可用設定**只證明有該覆寫入口；**執行證據**須有實際受測版本、環境與結果；**未驗證**不得由前三類外推。「AGENTS.md 優先」不是遵守規則的實證，文件沒提也不代表不支援。以下只查相關流程片段，沒有完整審完安裝、更新、hooks、scripts 或 imports；獲准安裝前仍須按產品既有外部工具流程檢查。

### Superpowers：本地優先有文字依據，inline 仍有收尾要求

- [using-superpowers](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/using-superpowers/SKILL.md) 明列使用者與 AGENTS.md 等專案指示優先於 skills，也有廣泛自動啟用要求。可先以本地指示對應限制，但未證明在執行中能限制派工、安裝或發布。
- [using-git-worktrees](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/using-git-worktrees/SKILL.md) 先辨識既有隔離、優先原生工具；同檔預設遇到 `package.json` 執行 `npm install`，worktree 建立遇權限錯誤則回原目錄繼續。兩產品使用 Bun，jia-jian-log 當前 staging 強制 linked worktree，這些預設需核對／覆蓋；沒有實際違規執行或「無法設定」的結論。
- [executing-plans](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/executing-plans/SKILL.md) 可在同 session 依任務執行，仍要求最終全分支 reviewer（有 subagent 工具時另派，無時記為自查），並在收尾刪除該 plan 的暫存 workspace。[final-review](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/subagent-driven-development/references/final-review.md) 更明寫 `rm -rf <workspace>`。這裡的 workspace 是 plan 暫存資料夾，不等於整個 Git worktree；仍須處理證據保留、目錄歸屬與刪除授權。本輪沒有執行清理。
- [恢復指示](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/subagent-driven-development/references/resuming.md) 依 plan 身分與 ledger 完成行續做；未證明獨占認領、舊 owner 失效或程序停止。試用時仍要比對當下工具 schema／模型限制，不能從來源文字推定所有客戶端可用。

### BMad：使用 release 既有覆寫，不能把設定入口當解決證據

本版 Build 來源在 [`src/bmm-skills/ship/bmad-build/`](https://github.com/bmad-code-org/BMAD-METHOD/tree/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build)，不是其他版本的路徑。[SKILL.md](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/SKILL.md) 以 `uv` renderer 載入 workflow；本輪只讀來源，未跑 renderer。

[`customize.toml`](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/customize.toml) 已提供 `_bmad/custom/bmad-build.toml` 與 `.user.toml` 覆寫：`persistent_facts` 可放 `file:` 指向本地權威，`activation_steps_prepend`／`activation_steps_append` 可放開工要求，`implementation_handoff` 可改實作交接，`review_layers`／`oneshot_review_layers` 可按 id 替換或以空 instruction 停用；另有 `on_complete`／`open_spec`。來源合併規則是字串取代、list 附加、table 逐鍵、table array 依 id。這些是可設定入口，尚未建立設定或驗證優先順序；未將後來 main 的 route／review 自訂欄位誤列為本 release 功能。

[full 實作](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/step-03-implement.md) 預設交給 subagent，要求不 push／不做遠端操作；[review](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/step-04-review.md) 派多個審查層，[present](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/step-05-present.md) 禁止自動 push。[oneshot](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/ship/bmad-build/step-oneshot.md) 雖直接實作，仍要求審查 subagents，除非使用者要求否則不 push。需核對單線授權、review 身分與兩產品的交付節奏；加入 persistent fact 或 on_complete 並不等於已化解步驟衝突。[project-context skill](https://github.com/bmad-code-org/BMAD-METHOD/blob/bab9082c3e884e0d72c759bcd1a6d90bcc01be84/src/bmm-skills/plan/bmad-project-context/SKILL.md) 會提議管理 AGENTS.md 區塊並要求寫入前核准；本輪沒有啟用它。

### Spec Kit：推薦只限官方 Lean，core 與擴充另看

[官方 Lean README](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/README.md) 說明它是內建 preset，直接覆寫五個命令，不需另造 Adapter。[specify](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/commands/speckit.specify.md) 要求使用者提供 feature 目錄，寫入 `.specify/feature.json` 與 `spec.md`；[plan](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/commands/speckit.plan.md)、[tasks](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/commands/speckit.tasks.md)、[implement](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/commands/speckit.implement.md) 依序讀檔、產生計畫／任務、順序執行，失敗就停並回報。這些精簡命令未要求派工；它們也不是工作區鎖或產品測試／review gate，feature 指標與三份文件要計入維護及接手成本。

[Git extension](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/extensions/git/README.md) 將初始化、分支、驗證、auto-commit 放在選用模組；[agent-context extension](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/extensions/agent-context/README.md) 明寫 opt-in，`specify init` 不安裝它，不安裝便不修改 AGENTS.md 等 context 檔案。**後續試用提案是先不加這兩項擴充**，沿用產品既有工作區與 Git 規則；本輪沒有進行安裝或設定。[Lean constitution](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/presets/lean/commands/speckit.constitution.md) 仍會建立／更新 `.specify/memory/constitution.md`；應在試用中核對它只引用 owning AGENTS.md 與必要脈絡、不產生第二套政策，這是待驗設定要求，非預設保證。

[完整 core plan](https://github.com/github/spec-kit/blob/9eacc24ffe47eadf035a3af601e4dabfb15b8fde/templates/commands/plan.md) 明列派發 research agents，另有較多研究／設計產物及 hook 處理。不能把 Lean 的精簡／順序特性外推到 core、其他 preset、已安裝擴充或未來版本。三套候選均未試跑；成本、規則遵守與收益仍未知。

## 產品規則與現有共用副本：唯讀快照

以下是 2026-11-03 從 owning source 核對的版本，供本次比較使用；實際開工要重查。不是向產品安裝的新規則，也不是這些產品在該版本已跑過測試的宣告。

| 產品／當時基線 | 必須容納的本地規則與來源 |
| --- | --- |
| Dance Stamp／main `acea4b9d52ad1b7aaa7db2ba1e5b8c070a567b74` | [AGENTS.md](https://github.com/sunpochin/dance-stamp/blob/acea4b9d52ad1b7aaa7db2ba1e5b8c070a567b74/AGENTS.md)：一般 PR → main，單件完成後 commit／push，`bun run check` 加受影響既有測試；共用 checkout 有其他任務時隔離，專用新 clone 可在 feature branch 工作；不自動派平行 Agent。保留媒體成檔、取消與資料保全，review／真機／發布分開。 |
| jia-jian-log／staging `7b15efdf20d429e95757333458de090e1956f3c0` | [AGENTS.md](https://github.com/sunpochin/jia-jian-log/blob/7b15efdf20d429e95757333458de090e1956f3c0/AGENTS.md)、[Git 流程](https://github.com/sunpochin/jia-jian-log/blob/7b15efdf20d429e95757333458de090e1956f3c0/docs/agents/git-workflow.md)：一般非 Draft PR → staging，Bun unit 含 `--isolate`，任務 commit／檢查點 push，保留 review／merge gates、照護資料與三語限制。當前基線仍要求 linked worktree；#1401 的 clone 替代方案尚未合併生效。 |

兩產品的 [Dance Stamp 固定清單](https://github.com/sunpochin/dance-stamp/blob/acea4b9d52ad1b7aaa7db2ba1e5b8c070a567b74/docs/ai/work-methods-lock.json) 與 [jia-jian-log 固定清單](https://github.com/sunpochin/jia-jian-log/blob/7b15efdf20d429e95757333458de090e1956f3c0/docs/ai/work-methods-lock.json) 文字完全相同，記錄 AWM v0.1.0／commit `938619f5472ff4475f702d51e2a466ab0cc63f60`、33 檔指紋。兩邊的 [採用說明（Dance Stamp）](https://github.com/sunpochin/dance-stamp/blob/acea4b9d52ad1b7aaa7db2ba1e5b8c070a567b74/docs/agents/work-methods.md)／[採用說明（jia-jian-log）](https://github.com/sunpochin/jia-jian-log/blob/7b15efdf20d429e95757333458de090e1956f3c0/docs/agents/work-methods.md) 已要求完整固定副本、共用修正回上游、各自 PR 升版。本輪只比對清單與規則，**沒有重新逐檔比對上游、重跑產品完整性檢查或改動副本**。

## 工作區與 submodule：已有證據及不能外推的部分

像測過一個獨立抽屜能放固定版本的手冊，不代表另一種共用抽屜也能用，更不代表三本新流程手冊已試過。

### jia-jian-log #1401 的精確範圍

2026-11-03 重查 [PR #1401](https://github.com/sunpochin/jia-jian-log/pull/1401) 仍 open、未合併；head `91669d59deab3bdc20dfe03a716cae7a050ccd82`，base staging／merge-base `7b15efdf20d429e95757333458de090e1956f3c0`。該 PR 支援外部確認歸屬的新任務專用 clone，保留 linked worktree、共用目錄與跨路徑防護；不是允許任意現有 clone 自行宣告可寫，也不會自動認領舊工作區。

本輪唯讀查閱 [驗證文件](https://github.com/sunpochin/jia-jian-log/blob/91669d59deab3bdc20dfe03a716cae7a050ccd82/docs/agents/task-workspace-verification.md) 與 [taskCloneSubmodule.test.ts](https://github.com/sunpochin/jia-jian-log/blob/91669d59deab3bdc20dfe03a716cae7a050ccd82/tests/unit/taskCloneSubmodule.test.ts)，**未重跑產品測試**。該單檔僅用暫存合成 repo，驗證獨立 clone 初始化、gitlink 固定 v1、提交升 v2、回父 repo 舊 pin，再偵測未初始化、錯 commit 與髒檔且保留原內容；file transport 僅單次測試開放，global config 也用暫存替代。

- **本機既有結果：** [前棒作者紀錄](https://github.com/sunpochin/jia-jian-log/pull/1401#issuecomment-6591184649) 報告該 head 四份直接相關測試共 97 pass、0 fail。聊天交接另報告上述單檔獨立重跑 1 pass，非本輪重跑或獨立整包複審。本機 macOS／Git 2.54.0（Apple Git-157）／Bun 1.4.2／Node 26.8.1，不能冒充 repo 指定 Bun 1.4.4／Node 24.x。
- **已重新核對的 CI：** [app-ci 41545966344](https://github.com/sunpochin/jia-jian-log/actions/runs/41545966344) success，含指定 runtime、ESLint、完整 unit／coverage；其 checkout 為 PR merge ref，是該 head 與 staging 基線的整合檢查，與本機直接 head 結果分開。[security-ci 41545966249](https://github.com/sunpochin/jia-jian-log/actions/runs/41545966249) success，Gitleaks／Semgrep 成功，OSV 因原條件 skipped，不算已跑。
- **審查仍有缺項：** [bot 摘要](https://github.com/sunpochin/jia-jian-log/pull/1401#issuecomment-6591165926) 對完整 head 明列 completed／no findings；但重查 `codex-review/current` 仍 pending。[gate run 41545985170](https://github.com/sunpochin/jia-jian-log/actions/runs/41545985170) 的 job 已 success，這表示處理流程完成，不能代替該 commit status。作者交接記錄了摘要格式／事件的採計差異，本輪沒有重驗 gate 根因。不能宣告可合併；本輪沒有改 gate、手動寫成功、豁免或重複請審。
- **未驗證：** linked worktree＋submodule、任意 clone 的桌面 app 附加、舊 session 自動重新載入、Mission Control 派工／原生 canary、真實遠端來源可取得性。guard 是可信 host 設定下的日常防誤操作，非任意 shell／MCP 的完整 OS 隔離。這些結果不是三套候選的執行證據，也不是產品 submodule 遷移。

### 是否改用 submodule：先保留固定副本

[Git 官方](https://git-scm.com/docs/gitsubmodules) 說明 gitlink 記錄父 repo 期待的子模組 commit；原生 pin 可省去手動維護逐檔版本清單。[submodule 文件](https://git-scm.com/docs/git-submodule) 仍要求初始化／取得缺少 commit；[`git-worktree` 的 BUGS](https://git-scm.com/docs/git-worktree#_bugs) 仍明列 submodule 支援不完整。因此獨立 clone 測試通過不能外推 linked worktree＋submodule；放寬工作區規則只供另一種 clone 路徑，不會修好該組合。

| 可減少的工作 | 採用前仍要處理 |
| --- | --- |
| Git 直接保存整個上游 commit，升降版有 gitlink diff；可減少逐檔版本清單維護 | 新 clone／CI 的初始化、上游來源與固定 commit 可取得性、來源授權、離線／封裝內容與技能入口。 |
| 父 repo 可顯示子模組 commit 差異 | 同 commit 不等於乾淨；合成測試中 `submodule status` 的空白仍可伴隨髒檔。仍須檢查父／子 status、來源與未提交工作，不靠強制清理。 |
| 可改以 Git pin 表達版本完整性 | 兩產品現有 33 檔完整性檢查、CI checkout、公開內容掃描及發行包仍須調整與重驗，不能直接刪掉既有防線。 |

**目前不遷移兩產品。** 先確認選型後 AWM 還需保留多少共用內容，再決定分發方式；避免為固定版本另造管理系統。若未來仍有實際收益，另經授權提出最小遷移與回復計畫。本輪不改產品完成條件、不升版、不關票。

## 差距驗證順序與通過證據

1. **審閱 Lean 優先試用提案。** 根據上述固定來源比較，核對如何容納現有 AGENTS.md、測試與 PR 規則及設定／範本／擴充方式；另定實際版本、單項任務、工時／費用預算、停止條件與現有基準。候選試用不等於正式採用，也不因本文件而取得安裝或派工授權。
2. **兩產品各試一項小任務。** 各自取得授權，選無競爭 PR、可獨立驗收且有真實維護價值的一項；先單線，使用現有測試。先做設定，記錄真正做不到、衝突或成本過高的情況；兩邊可接受不同決策。必要的危險／失敗情境先在可拋棄合成資料上驗證，不把自建測試框架當前提。
3. **依結果決策。** 能設定就設定；適合上游改善的問題先整理可重現證據。只有反覆出現且確實無法解決的缺口，才另提少量自建。結果可為直接採用、只需設定、自建少量補充或維持現狀；不要求 AWM 必須增加內容或角色。

下列情境是試用前的驗證計畫；後續僅有上節所列 Lean 小任務證據，**完整矩陣尚未執行**，且與 #1401 的合成工作區證據分開。這是依選定工具與任務風險取用的清單，不是另造完整流水線的規格；不適用項要寫理由。每次紀錄結果須區分：工具直接處理、經設定處理、既有人工 gate 處理、無法處理或未驗證；人工核對不能報成工具自動拒絕。

| 情境 | 預期結果與需留證據 |
| --- | --- |
| 正常任務，兩種分支／push／check 規則 | 每組使用指定入口與目標；附實際分支、命令、結果、PR target，不能從範例猜本地規則 |
| 候選切換或升級，既有任務／證據入口 | 只由指定流程派工；任務紀錄與證據引用可追溯，沒有第二套競爭的 ledger／狀態或重複執行。升級重跑受影響案例，記錄前後工具版本與設定 |
| 錯 repo、cwd、worktree、分支，或隔離建立失敗 | 寫入前發現並停下；以前後狀態證明原工作區沒有被錯改，不可靜默退回共用 checkout |
| 既有 tracked／untracked／ignored 合成檔、越界 diff、rename | 保全非本任務內容；辨識改名兩端及 scope 外變更，留下前後清單／內容指紋 |
| 同任務重複指派、舊 owner、重啟與失聯 | 不覆蓋已有工作；先查程序／來源／PR，再由授權者接手。過期活動不代表程序已死；記錄實際誰能續寫及人工步驟 |
| 提交未推送、推送未登記、PR／CI 缺項或取消 | 明列缺項；區分本機、遠端、PR 與 CI 實際狀態，pending／cancelled 不算通過 |
| 測試／審查後 head、相關 base 或衝突解法改變 | 舊證據保持原版本；依本地政策重驗，不把舊綠燈或審查無條件套到新內容 |
| 缺政策、未知任務格式、惡意任務文字、借用他人資源 | 未知明列並停止依賴操作；不執行任務中的 shell，不動他人 port／profile／worktree。若工具不使用結構格式，記不適用及理由，不為測試強加 schema |
| 超預算、未獲准合併／發布／清理 | 停止新工作並保留可接手資訊；綠燈與自動化功能不擴張授權 |

## 兩產品的試用邊界

- **Dance Stamp：** 第一項已選純工具提示修正 #249，結果見上節；未改播放／時間線。後續若碰媒體，仍須保留既有行為、影片／音訊成檔、取消與資料保全要求；使用產品現有分支、push、CI 與審查入口。未執行的原生 Safari、真相機、人工、手機與跨裝置驗收保持未驗證。
- **jia-jian-log：** 第一項限低風險純工具、測試支援或文件接線；保留 staging／promotion、檢查點 push、既有審查與證據 gate、三語與照護資料隔離。排除正式資料、憑證、migration、RLS、照護授權、用藥及健康判讀；staging 結果不是 production 或真人驗收。

這裡只列追蹤責任；產品規則以開工時的 owning source 為準。本文件的收斂只保存已完成試用與原始比較，不修改兩產品 repo、不升版既有 vendor 副本、不執行新試用。兩產品不必等待對方完成，也不需要先建立 AWM 契約或 Adapter；**不依賴自建工具發布**。

## 最小回報範本

以下只供缺乏既有回報格式時參考；若選定流程已能保存相同證據，就引用其紀錄，不另維護一份 AWM 表格或工作契約。

```text
任務／試驗、負責人、當次授權、嘗試輪次：
方案／App／CLI／plugin 版本、固定來源 commit、設定差異：
本地政策入口、允許範圍、保留行為、共享資源與停止條件：
base／head／tested／reviewed／integration SHA、環境與證據連結：
實際情境與結果（工具／設定／人工／不支援／未驗證）：
既有未提交內容的保全、失聯接手與尚待處理項：
設定時間、接手時間、審查時間、首輪完整 CI、重試／衝突／返工：
模型費用與 CI 分鐘（未知填 unknown）、失敗／放棄成本：
結論：直接採用／只需設定／自建少量補充／維持現狀：
依據、限制、下一步與負責人：
```

公開回報去除私人絕對路徑、帳號／profile、媒體、照護資料與秘密。成本以每個已驗收任務比較，失敗與放棄也計入；先看設定、接手與審查負擔，不以 LOC、PR 數或模型品牌代替結果。若後續另獲准合併，追蹤每個 PR 合併後七日的回歸／revert／緊急修補；樣本不足只作方向判斷。

## 何時才新增程式

新增前必須有固定版本／環境下反覆發生的最小重現、預期與實際差異、影響範圍，以及已試過的工具設定／範本／擴充、既有檢查及上游改善路徑與限制。記錄為何仍無法解決，而非只記「與我們不同」。文件未提某功能、尚未安裝、產品有自己的規則、或偏好統一格式，都不足以證明需要自建。

只有上述條件成立，才提出能解決該問題的最小補丁、可重跑驗證、維護成本、來源授權與回復方式；確認授權後才實作。現成方案足夠或維持現狀較合理時，#3 可以只留下決策與版本紀錄，不新增共用流程、契約、Adapter、helper 或框架。

本階段保存比較與一項 Lean 小任務的受限結論；同類小修正維持現狀。#3 的跨產品決策仍缺 jia-jian-log 試用與較大任務收益證據，不宣告兩產品驗收完成；兩產品採用、獨立審查、合併及發布各自記錄，不能由本文件或封裝測試代簽。
