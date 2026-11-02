<!-- 檔案用途：先比較現成方案，再以可重跑證據決定是否補工具。所在層：選型研究與試用計畫，非安裝規則。主要關聯：ADOPTION.md、VALIDATION.md、../TECHNICAL.md。 -->
# 先選型，再決定要補什麼

先試現有工具箱，再決定是否需要自己做工具。此階段以既有 Codex 工作流程為基準，優先比較 Superpowers 的方法增益；只有重現的缺口無法由設定、既有測試或少量接線處理，才提出新增程式的設計。

**2026-11-03 狀態：官方文件與來源文字已查閱；安裝、合成情境執行、產品試用、效益及相容性均未驗證。** 本文件是候選研究與差距驗證計畫，不是採用決議或完成的實驗報告。既有五個 skills 與 v0.1.0 套件不變；先前的本機核對工具草稿未納入交付、未驗證，也不作預定成果。

本文件對應 [共用主票 #3](https://github.com/sunpochin/agent-work-methods/issues/3)；產品試用分別由 [Dance Stamp #246](https://github.com/sunpochin/dance-stamp/issues/246) 與 [jia-jian-log #1399](https://github.com/sunpochin/jia-jian-log/issues/1399) 追蹤。這些關聯是維護計畫，不會安裝到個別 skill 或成為其他專案的政策。

## AWM 負責什麼

四個外部方案是候選清單，**不需要全部接上**；原生 Codex 是現有基準。每次只選實際需要的能力，明確指定唯一的任務紀錄與派工責任歸屬。採用文件引用既有 issue、聊天、測試與 PR 證據，不另造一套同步狀態的任務系統。

AWM 的維護範圍是三件事：

1. **共用工作契約：** 任務範圍、測試／審查證據、失敗交接需要交代什麼；優先使用文字範本對應現有紀錄，不強制機器格式。
2. **工具接線與採用方法：** 讓選定工具使用產品既有 issue、工作區、檢查與 PR 流程；記錄來源、實際版本、設定與回復方法。
3. **相容性驗證：** 採用或升級時重跑相關案例；把可重現缺口整理成上游回報材料，必要時才提出小補丁。本輪未向上游發文。

產品提供規則與驗收 → AWM 提供契約與接線 → 選定工具執行任務、測試與 PR 流程。例如一般 PR 的目標在兩產品分別是 main 與 staging，這是各產品提供的輸入，不能由 AWM 猜測或統一。

**Adapter 是主要設計思路**，用來對應既有流程；真的需要切換執行方式才考慮 Strategy；操作分散已造成困難時才考慮選用的 Facade。這些名稱不要求新增介面、類別、統一 CLI 或框架。設定、文件、範本與驗證案例足夠時，維持這個形式。只有第二個工具實際需要接入，且出現重複接線後，才評估抽成共用程式；單一工具的具體缺口則只提最小修補。

## 候選與已知範圍

以下「文件／來源」表示可追溯的描述或指示，**不表示執行成功**。「待驗」也不等於工具不支援。

| 候選 | 文件／來源可確認的範圍 | 待驗問題 | 本輪定位 |
| --- | --- | --- | --- |
| Codex 原生工作流程 | 獨立 worktree、選擇起點、Local／Worktree Handoff、分支與 PR 操作；見 [官方 Worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees) | 實際客戶端版本下的指定分支、未提交／ignored 檔案保全、交接、受測與受審版本記錄 | 優先作現有基準，先不增加另一套工作區管理 |
| Superpowers | 設計／計畫、工作區選擇、逐任務執行與審查、進度 ledger 與恢復指示；見 [固定來源 README](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/README.md) 與下表 | 本地規則優先是否在實際執行中成立；安裝、重試、審查與清理是否遵守邊界；增加的設定與審查成本 | 優先比較的方法層候選，可與 Codex 配合，尚未選定採用 |
| GitHub Spec Kit | 規格、計畫、任務、澄清與文件一致性檢查；見 [官方 Agentic SDD](https://github.github.com/spec-kit/reference/agentic-sdd.html) | 是否解決實際需求拆解痛點；新增 constitution／規格文件能否引用現有規則而不形成第二份政策 | 有需求模糊或跨文件漂移證據時再試；不把規格工具當工作區鎖 |
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

1. **凍結範圍與基準。** 從目前已授權的工作流程開始，記錄工具版本、本地規則入口、來源 SHA、分支／工作區與未提交狀態。先量單線成本；不得由文件比較推定已獲准安裝、啟動 Agent 或變更全域設定。
2. **先做兩組合成情境。** 獲准後使用匿名、無憑證、可拋棄 repo；甲使用 `trunk`、單件完成推送、check-A，乙使用 `integration`、檢查點推送、check-B。名稱是測試輸入，不是共用規定。比較原生流程與加入候選方法後的行為；不要為測試而寫一套新 runner。
3. **再做兩產品各一項小任務。** 各自取得授權，選無競爭 PR、可獨立驗收且有真實維護價值的一項；先單線，使用現有測試。候選方式與基準的工作量需可比較；不把熟悉同一答案後的加速歸功於工具。
4. **依結果選擇。** 記錄直接採用、薄接線、暫不採用或最小補工具的理由。共用 repo 保存經驗、固定來源紀錄與必要範本；產品接線、資料規則與驗收留在產品。

下列情境目前**全部未執行**。每次紀錄結果須區分：工具直接處理、經設定處理、既有人工 gate 處理、無法處理或未驗證；人工核對不能報成工具自動拒絕。

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

這裡只列追蹤責任；產品規則以開工時的 owning source 為準。不修改兩產品 repo、不升版既有 vendor 副本、不執行試用。兩產品不必等待對方完成；只依賴可審查的候選與試驗計畫，**不依賴自建工具發布**。

## 最小回報範本

以下是可填入既有 issue／PR 的文字欄位，不新增強制 JSON schema、服務或第二個合併入口。

```text
任務／試驗、負責人、當次授權、嘗試輪次：
方案／App／CLI／plugin 版本、固定來源 commit、設定差異：
本地政策入口、允許範圍、保留行為、共享資源與停止條件：
base／head／tested／reviewed／integration SHA、環境與證據連結：
實際情境與結果（工具／設定／人工／不支援／未驗證）：
既有未提交內容的保全、失聯接手與尚待處理項：
設定時間、接手時間、審查時間、首輪完整 CI、重試／衝突／返工：
模型費用與 CI 分鐘（未知填 unknown）、失敗／放棄成本：
結論：直接採用／薄接線／暫不採用／提出最小補工具：
依據、限制、下一步與負責人：
```

公開回報去除私人絕對路徑、帳號／profile、媒體、照護資料與秘密。成本以每個已驗收任務比較，失敗與放棄也計入；先看設定、接手與審查負擔，不以 LOC、PR 數或模型品牌代替結果。若後續另獲准合併，追蹤每個 PR 合併後七日的回歸／revert／緊急修補；樣本不足只作方向判斷。

## 何時才新增程式

新增前必須有固定版本／環境的最小重現、預期與實際差異、影響範圍，以及已試過的設定／既有檢查／人工 gate／薄接線及其限制。文件未提某功能、尚未安裝、或偏好統一格式，都不足以證明需要自建。

若差距確實存在，先提出能解決該問題的最小補丁、可重跑驗證、維護成本、來源授權與回復方式；確認授權後才實作。現成方案足夠時，#3 可以只交付採用方法、版本紀錄與必要範本，不要求 helper、排程器或框架。

本階段完成表示比較與試驗設計可供審閱。#3 的最終選型仍待實驗與產品回饋；兩產品採用、獨立審查、合併及發布各自記錄，不能由本文件或封裝測試代簽。
