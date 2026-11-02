<!-- 檔案用途：先比較現成方案，再以可重跑證據決定是否補工具。所在層：選型研究與試用計畫，非安裝規則。主要關聯：ADOPTION.md、VALIDATION.md、../TECHNICAL.md。 -->
# 評估現成流程並驗證兩產品採用可行性

規劃、拆任務、執行、測試、審查與交接已有現成流程。此階段以既有 Codex 工作方式作比較基準，評估 Superpowers、BMad Method 與 Spec Kit 如何容納既有 AGENTS.md、測試與 PR 規則，再選一套作小規模試用。產品有自己的規則，只能推導出需要核對設定與驗收，不能直接推導成需要新流程、共用契約或 Adapter。

**2026-11-03 狀態：官方文件與來源文字已查閱；安裝、合成情境執行、產品試用、效益及相容性均未驗證。** 本文件是候選研究與差距驗證計畫，不是採用決議或完成的實驗報告。既有五個 skills 與 v0.1.0 套件不變；先前的本機核對工具草稿未納入交付、未驗證，也不作預定成果。

本文件對應 [共用主票 #3](https://github.com/sunpochin/agent-work-methods/issues/3)；產品試用分別由 [Dance Stamp #246](https://github.com/sunpochin/dance-stamp/issues/246) 與 [jia-jian-log #1399](https://github.com/sunpochin/jia-jian-log/issues/1399) 追蹤。這些關聯是維護計畫，不會安裝到個別 skill 或成為其他專案的政策。

## 不預設 AWM 必須新增一層

外部方案是候選清單，**不需要全部接上**。先看選定方案已有的設定、範本、專案指示與擴充方式；沿用其紀錄及現有 issue／PR 證據，不預先建立 AWM 的任務格式、狀態機或派工入口。

AWM 可能只需保存選型結果、實際固定版本與少量專案補充，也可能完全不需要新增共用流程。評估結果允許四種，按實際證據選擇：

1. **直接採用：** 現成流程已能容納本地規則，保留必要的版本與驗收紀錄。
2. **只需設定：** 用工具既有設定、範本或專案指示完成，記錄差異與回復方式。
3. **自建少量補充：** 僅限反覆出現、設定與上游改善路徑仍無法解決的具體缺口；另外審查最小範圍、成本與授權。
4. **維持現狀：** 沒有足夠收益、成本過高或不相容時，保留現有流程也是完整的決策成果。

產品直接提供規則給選定流程。例如一般 PR 的目標在兩產品分別是 main 與 staging，應核對工具是否能透過既有設定遵守，而不是先在兩者之間加入自建轉接層。

Adapter、Strategy、Facade 都不是本票預定架構或完成條件。即使第二個工具需要使用、出現相似設定，也不足以直接證明要抽共用程式。先能設定就設定，適合由上游解決就整理可重現回報；只有反覆發生且確實無法解決的缺口才考慮少量自建。本輪未向上游發文。

## 候選與已知範圍

以下「文件／來源」表示可追溯的描述或指示，**不表示執行成功**。「待驗」也不等於工具不支援。

| 候選 | 文件／來源可確認的範圍 | 待驗問題 | 本輪定位 |
| --- | --- | --- | --- |
| Codex 原生工作流程 | 獨立 worktree、選擇起點、Local／Worktree Handoff、分支與 PR 操作；見 [官方 Worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees) | 實際客戶端版本下的指定分支、未提交／ignored 檔案保全、交接、受測與受審版本記錄 | 優先作現有基準，先不增加另一套工作區管理 |
| Superpowers | 設計／計畫、工作區選擇、逐任務執行與審查、進度 ledger 與恢復指示；見 [固定來源 README](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/README.md) 與下表 | 本地規則優先是否在實際執行中成立；安裝、重試、審查與清理是否遵守邊界；增加的設定與審查成本 | 優先比較的方法層候選，可與 Codex 配合，尚未選定採用 |
| BMad Method | [官方 Method](https://bmadcode.com/method) 描述分析、規劃、實作、驗證，以 repo 文件交接、追溯決策／需求／測試，並提供模組與團隊／個人覆寫 | 既有指示與覆寫優先順序、PR／檢查規則是否能直接設定；文件負擔與升級後行為 | 納入流程候選；本輪只核對官方描述，未審完整安裝鏈或執行 |
| GitHub Spec Kit | 原則、規格、計畫、任務、一致性檢查、實作與收斂；見 [官方 Agentic SDD](https://github.github.com/spec-kit/reference/agentic-sdd.html) | 現有 AGENTS.md 與 constitution 的責任對應；工具既有範本／設定能否容納本地工作方式 | 納入完整流程比較；不把規格工具當工作區鎖 |
| Conductor | 每項工作可有獨立 worktree／分支／聊天／終端，提供連接埠範圍、diff 與 checks／PR 介面；見 [官方 Codex 並行指南](https://www.conductor.build/docs/guides/parallel-agents/run-multiple-codex-sessions) | setup scripts、Files to copy、資源隔離與清理是否符合政策；介面收益是否值得額外設定 | 需要更多協作介面時再評估；文件明示工作區隔離不是安全邊界 |
| Agent Orchestrator | 描述按工作區啟動 Agent、將 CI／review／衝突回交 worker；[固定 README](https://github.com/OrchestratorInc/agent-orchestrator/blob/25bc9b148f76438a117b930608a4a19d60e32fab/README.md) 與 [架構文件](https://github.com/OrchestratorInc/agent-orchestrator/blob/25bc9b148f76438a117b930608a4a19d60e32fab/docs/architecture.md) 涵蓋常駐程序與持久化狀態 | 自動重試、恢復、權限、服務成本、停止與資料邊界；本輪未審完整執行鏈 | 只有實測證明需要調度時另評估，初期不啟用常駐服務 |

這些方案所處層次不同，不能只用功能數量排總分，也不能據此推定需要搭配。若確實選用多個元件，先劃清責任；同一任務不得同時由兩套流程派工或維護互相競爭的狀態。

## 優先候選的具體核對點

Superpowers 的來源固定在 `2ce8aa15d05bd57213e6f746f953aafb7ded7a8b`，是本次閱讀版本，不是已測試或已安裝版本。Agent Orchestrator 同理，固定在 `25bc9b148f76438a117b930608a4a19d60e32fab`。官方網站為 2026-11-03 閱讀的可變文件；試用時另記錄實際 App／CLI／plugin 版本與設定，不推定 marketplace 套件等於 repo HEAD。

| 來源觀察 | 對差距驗證的影響 |
| --- | --- |
| Superpowers [using-superpowers](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/using-superpowers/SKILL.md) 指出使用者與專案指示優先，但也有廣泛的自動 skill 啟用要求 | 測試明確授權範圍能否限制自動工作流程；不能因載入 skill 就推定獲准派工或發布 |
| [using-git-worktrees](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/using-git-worktrees/SKILL.md) 優先辨識既有隔離與原生工具；同檔包含依檔案類型安裝依賴及 worktree 權限失敗後在原目錄工作的指示 | 核對實際套件管理器、安裝授權，以及本地要求隔離時會不會錯誤退回原 checkout；這是候選衝突，尚未重現 |
| [subagent-driven-development](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/subagent-driven-development/SKILL.md) 使用每個 plan 的 ledger；[恢復指示](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/subagent-driven-development/references/resuming.md) 依 plan 身分及完成紀錄接續 | 可以優先試既有接手方法；ledger 描述不能證明獨占認領、舊 owner 失效或程序已停止，這些需求仍需分別驗證 |
| [final-review](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/subagent-driven-development/references/final-review.md) 包含刪除 plan 工作目錄的指示；[分支收尾](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/finishing-a-development-branch/SKILL.md) 則區分 PR 保留與合併後清理 | 保留進度與證據的期限、目錄所有權及刪除授權要映射到本地；測試只可使用可拋棄合成資料，不執行來源中的清理命令 |
| [Codex 對接指示](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/using-superpowers/references/codex-tools.md) 有工具參數與模型路由假設 | 試用前比對當下工具 schema 與限制；本次環境的完整歷史分支不接受模型覆寫，與該來源文字不同。此為靜態介面差異，未執行派工，也不外推所有 Codex 版本 |
| Codex [官方 Worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees) 描述預設 detached HEAD、Handoff、ignored 檔案複製及清理快照 | 測試需包含分支命名、只移動本任務修改、未提交／ignored 合成檔案及恢復；不能把 worktree 存在當作所有內容已備份。不要為試用自動複製真實秘密檔案 |

以上是閱讀結果與待驗假設，不是漏洞報告、完整安全審查或已確認無法設定的缺陷。未讀完的 hooks、scripts、imports、安裝與更新行為，仍需在獲准安裝前按既有外部工具審查流程檢查。遠端 skill 文字在本輪只作研究資料，未作執行指令。

## 差距驗證順序與通過證據

1. **先選一套待試流程。** 比較如何容納現有 AGENTS.md、測試與 PR 規則，核對設定／範本／擴充方式；記錄選它而非其他候選的理由、實際版本與現有基準。候選試用不等於正式採用，也不因本文件而取得安裝或派工授權。
2. **兩產品各試一項小任務。** 各自取得授權，選無競爭 PR、可獨立驗收且有真實維護價值的一項；先單線，使用現有測試。先做設定，記錄真正做不到、衝突或成本過高的情況；兩邊可接受不同決策。必要的危險／失敗情境先在可拋棄合成資料上驗證，不把自建測試框架當前提。
3. **依結果決策。** 能設定就設定；適合上游改善的問題先整理可重現證據。只有反覆出現且確實無法解決的缺口，才另提少量自建。結果可為直接採用、只需設定、自建少量補充或維持現狀；不要求 AWM 必須增加內容或角色。

下列情境目前**全部未執行**，是依選定工具與任務風險取用的驗證清單，不是另造完整流水線的規格；不適用項要寫理由。每次紀錄結果須區分：工具直接處理、經設定處理、既有人工 gate 處理、無法處理或未驗證；人工核對不能報成工具自動拒絕。

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

- **Dance Stamp：** 第一項從有需求的播放／時間線等小任務選擇。保留既有行為、影片／音訊成檔、取消與資料保全要求；使用產品現有分支、push、CI 與審查入口。未執行的原生 Safari、真相機、人工、手機與跨裝置驗收保持未驗證。
- **jia-jian-log：** 第一項限低風險純工具、測試支援或文件接線；保留 staging／promotion、檢查點 push、既有審查與證據 gate、三語與照護資料隔離。排除正式資料、憑證、migration、RLS、照護授權、用藥及健康判讀；staging 結果不是 production 或真人驗收。

這裡只列追蹤責任；產品規則以開工時的 owning source 為準。本輪不修改兩產品 repo、不升版既有 vendor 副本、不執行試用。兩產品不必等待對方完成，也不需要先建立 AWM 契約或 Adapter；**不依賴自建工具發布**。

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

本階段完成表示比較與試驗設計可供審閱。#3 的最終選型仍待實驗與產品回饋；兩產品採用、獨立審查、合併及發布各自記錄，不能由本文件或封裝測試代簽。
