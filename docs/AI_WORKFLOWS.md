<!-- 檔案用途：統整與記錄本專案體系所採用、評估與借鑑的 AI 工作流程 (Workflows)、Skills 與框架 (Frameworks)。所在層：工具與架構盤點清單。主要關聯：README.md、TECHNICAL.md、docs/TOOL_EVALUATION.md、docs/ADOPTION.md。 -->
# AI 工作流程、Skills 與框架紀錄 (AI Workflows, Skills & Frameworks Registry)

本文件統一梳理本專案體系（包含 `agent-work-methods` 以及採用本方法的相關產品專案）所使用、試用、評估或借鑑的各類 AI 工作流程（Workflows）、技能組（Skills）與輔助框架（Frameworks）。

---

## 1. 核心哲學與採用原則 (Philosophy & Principles)

在 AI 輔助軟體開發（Agentic Coding）中，市面上存在許多不同理念的工作流程與工具箱。本專案體系維持一貫的「**以專案憲法與驗證為本，工具僅為按需選用之手冊（Verification-First & Thin Adapters）**」原則：

1. **專案主權優先**：框架與 Skill 只是工作方法，不凌駕專案既有的分支規範、測試流程、套件管理與審查邊界。
2. **拿證據說話（Verification-First）**：拒絕僅依型別檢查或靜態文本就宣稱完成的「虛浮程式碼（Slop Code）」，所有改動必須在真實環境重現與驗證。
3. **避免過度工程化（No Premature Abstraction）**：小型修復維持輕量原生流程；只有當現成設定無法解決且帶來反覆痛點時，才引入或自建專案適配層。

---

## 2. 工具與框架總覽矩陣 (Frameworks & Workflows Matrix)

| 類別 / 框架 | 來源與代表 | 核心機制與特點 | 採用狀態 | 適用場景與限制 |
|---|---|---|---|---|
| **自研通用技能庫 (AWM)** | `agent-work-methods` (5 Skills) | 遵循 Agent Skills Specification；純文字 Markdown、自足無外部執行期依賴 | **正式採用 (v0.1.0)** | 接手專案、問題重現、客觀審查、介面驗收與安全性檢查 |
| **規格驅動開發 (Spec-Driven)** | **GitHub Spec Kit** (`spec-kit`) | 依序產出 `spec.md` → `plan.md` → `tasks.md`；官方 Lean preset | **已完成試用 (Dance Stamp #249)** | 適合大型跨團隊需求；小型任務額外文件開銷過大，建議維持原生流程 |
| **工程 Playbook 與反 Slop** | **pstack** (Lauren Tan / poteto) | `/poteto-mode` 路由、20+ Playbooks、24 項工程原則、真實環境驗證 | **核心參考典範 / 借鑑原則** | 借鑑其 "Go Deep First, Then Fast"、Laziness Protocol 與真實驗證精神 |
| **子 Agent 驅動規劃** | **Superpowers** (obra) | Subagent-driven、Git Worktree 隔離、Plan 循序執行 | **靜態評估完畢 / 暫緩優先試用** | 預設包含 `npm install` 與 `rm -rf`，與本專案 Bun 及命令安全政策衝突 |
| **多角色全週期體系** | **BMad Method** (BMAD-METHOD) | BMM Skills (`bmad-build`)、多角色分工 (PM/Arch/Dev/QA)、`uv` 渲染 | **靜態評估完畢 / 暫緩優先試用** | 框架過於龐重、配置與派工成本高於帶來的效益 |
| **雙層 Agent 協作體系** | **Project Constitution** | 主刀醫師 (Claude Code) + 實習探路員 (Antigravity) | **核心專案憲法實施中** | 生產代碼與架構由主刀負責；UI 原型/探路/驗證由實習生負責 |
| **語意導航與代碼理解** | **Serena** (`oraios/serena`) | LSP 語意導航、代碼記憶體庫、符號精準定位 | **本機輔助工具** | 提供代碼結構精確定位與語意分析，輔助 Agent 避免盲猜 |

---

## 3. 各框架與工作流詳細剖析 (Deep Dive)

### 3.1 GitHub Spec Kit (`spec-kit`)

- **來源與版本**：GitHub 官方開源工具 (`github/spec-kit`)，評估版本為 v1.2.6，使用官方 Lean preset v1.0.0。
- **核心流程**：
  1. `spec.md`：定義清晰的需求規格、使用者故事與驗收標準。
  2. `plan.md`：規劃架構影響、技術選型與檔案修改範圍。
  3. `tasks.md`：拆解為具體可勾選執行的原子任務清單。
  4. 循序實作、更新勾選並交付。
- **實務試用紀錄與結論**：
  - **試用案例**：於產品端 Dance Stamp #249 / PR #250 執行（修正 AWM 固定副本漂移提示）。
  - **成效與取捨**：Spec Kit 的局部設定與顯式載入能正常運作，順利完成修復並通過測試。但針對此類小型修正，產出與維護三份 Markdown 文件的成本顯著高於修改本身，且無數據證明能節省時間或代幣花費。
  - **處置**：產生的啟用檔案已移除；同類小型修復維持原生精簡流程。詳細評估與證據見 [TOOL_EVALUATION.md](TOOL_EVALUATION.md)。

---

### 3.2 pstack (Lauren Tan / poteto)

- **來源背景**：由前 SpaceX 首席工程師、React Core 成員、Cursor Staff Lauren Tan 開發的 Agent 工程框架與技能體系。
- **核心哲學**：
  - **"Go Deep First, Then Fast"（先深後快）**：傳統 Agent 容易在未理解整體上下文前急躁修改多個檔案，留下大量難以維護的「Slop Code」。pstack 要求 Agent 像嚴謹的資深工程師一樣，在動刀前深入探查根因與邊界。
  - **真機嚴格驗證（Rigorous Verification）**：不能只依賴靜態型別通過或單元測試假設，必須在真實執行的應用程式（Real, running application）中提供可觀察的證據。
- **主要組件與技能**：
  - **智慧路由入口 (`/poteto-mode`)**：使用者給定高層次目標，由 Agent 自行判斷任務型態並調用對應的 Playbook，自動編排並在交付時提供實質證據。
  - **任務手冊 (Playbooks, 20+)**：包含 Bug 修復、功能實作、效能最佳化、自主長期運行等標準化作業路徑。
  - **24 條工程原則 (Design Principles)**：
    - *Laziness Protocol（偷懶協議 / 最小修改原則）*：嚴禁順手重構或碰觸無關代碼，改動越少、越精確越好。
    - *Attack the Premise（質疑前提）*：動手前先挑戰需求假設與重現路徑，避免為錯誤的假設撰寫代碼。
    - *Prove It Works（拿證據說話）*：交付必須包含終端機日誌、測試輸出或真實互動截圖。
  - **獨立實用 Skills**：
    - `/how` / `/why`：唯讀調查指令，用於摸清不熟悉的子系統或回溯架構決策原因。
    - `/architect` / `/arena` / `/swarm`：多方案設計比較、多 Agent 平行探索與架構評審。
    - `/interrogate`：實作前的結構化多 Agent 代碼審查。
    - `/unslop` / `/deslop`：清除 AI 生成的冗餘註解、無效包裝層與死代碼。
- **在專案體系中的啟發與定位**：
  - 本專案的 `awm-debugging`（先重現與根因調查，再行最小修改）與 `awm-review-evidence`（用客觀收據對齊版本）深受 pstack 的「反 Slop、重視真實證據」理念啟發。

---

### 3.3 Agent Work Methods (AWM) 通用技能組

- **規範相容**：遵循 [Agent Skills 規範](https://agentskills.io/specification)，各技能皆為獨立資料夾，內含 `SKILL.md`、`references/`、`LICENSE` 與 `NOTICE.md`。
- **五大核心 Skills**：
  1. [`awm-onboarding`](../skills/awm-onboarding/SKILL.md)：新環境與新代碼庫快速定位，尋找入口與既有驗證命令。
  2. [`awm-debugging`](../skills/awm-debugging/SKILL.md)：重現問題並確認根因，嚴禁未經驗證的猜測修改。
  3. [`awm-review-evidence`](../skills/awm-review-evidence/SKILL.md)：審查標準與版本證據留存，以真實 Commit / CI 收據為準。
  4. [`awm-frontend-review`](../skills/awm-frontend-review/SKILL.md)：端到端使用者旅程檢查、介面驗收與失敗情境恢復。
  5. [`awm-skill-safety`](../skills/awm-skill-safety/SKILL.md)：第三方 Skill 與腳本之安全邊界審查，防止破壞性命令與機密外洩。
- **採用方式**：請參閱 [採用說明](ADOPTION.md)。各產品專案採「固定版本拷貝」或「Git Commit 鎖定（如 `work-methods-lock.json`）」管理，確保獨立自足。

---

### 3.4 Superpowers & BMad Method (評估與借鑑)

- **Superpowers (obra, v7.0.1)**：
  - 核心特點：子 Agent 驅動規劃、利用 Git Worktree 進行空間隔離 (`using-git-worktrees`)、Plan 循序執行 (`executing-plans`)。
  - 取捨與限制：其預設行為包含在暫存工作區執行 `npm install`，並在收尾時直接 `rm -rf <workspace>`。這與我們專案採用的 Bun 環境以及嚴禁未授權刪除目錄的憲法政策相違背，故暫緩直接引入。
- **BMad Method (bmad-code-org, v6.12.4)**：
  - 核心特點：完整的敏捷角色拆分（PM、架構師、開發者、QA），使用 `uv` 載入工作流。
  - 取捨與限制：流程架構龐重，且包含強制性的 oneshot/no-push 假設；若引入需維護大量覆寫設定，維護成本遠高於其帶來的規格效益，故維持現狀。

---

### 3.5 雙層 Agent 協作體系 (Two-Tier Agent Constitution)

本專案體系規範了清晰的雙層 Agent 職責分工與最高憲法原則：

1. **主刀醫師 (Primary Engineer - Claude Code / Codex)**：
   - 負責核心架構決策、生產環境代碼修改、資料庫遷移、安全政策與最終 PR 審查。
2. **實習生 / 探路員 (Secondary Assistant - Antigravity / Gemini)**：
   - 負責擬定實作計畫、UI 原型構建、瀏覽器實機測試驗證、低風險修復與進度報告。
3. **最高憲法 (Prime Directive 四步驟)**：
   - **ELI5 解說**：每次回報皆附白話淺顯、無技術門檻的說明。
   - **Why-Not-What 繁中註解**：代碼中加入註解說明「為什麼這樣做」，特別標註非直覺決策與潛在坑點。
   - **技術文件更新**：架構或功能變更時同步更新 `TECHNICAL.md`。
   - **自動提交與開立 PR**：在專屬任務分支工作，完成後立即推送並自動使用 `gh pr create` 開立非 Draft PR。
4. **安全防線 (Destructive Command Guard)**：
   - 嚴格禁止破壞性命令（`rm -rf`、`git reset --hard`、`git clean -fd` 等）。
   - 產品端（如 Dance Stamp）透過 `destructive-guard.ts` 及 ReviewLatch 攔截危險操作。

---

## 4. 決策指引：不同任務該選用哪種工作流程？ (Decision Guide)

```
                            [新任務開始]
                                 │
                 ┌───────────────┴───────────────┐
                 ▼                               ▼
          【小型修復 / Patch】           【大型新功能 / 跨系統】
                 │                               │
        使用原生輕量流程                         │
        搭配 awm-debugging 根因調查              │
        堅持 Laziness Protocol 最小修改          │
                 │                               │
                 │                ┌──────────────┴──────────────┐
                 │                ▼                             ▼
                 │        【需嚴格規格化】              【需多架構比較】
                 │         啟動 Spec 檔案鏈              借鑑 pstack /architect
                 │        (spec → plan → tasks)          進行方案評審與多視角審查
                 │                │                             │
                 └────────────────┼─────────────────────────────┘
                                  ▼
                         【程式修改與實作】
                                  │
                 ┌────────────────┴────────────────┐
                 ▼                                 ▼
           【純邏輯 / 後端】                 【前端 / 互動畫面】
        單元測試與型別檢查驗證               啟動 awm-frontend-review
                 │                        瀏覽器實機操作、錄影或截圖佐證
                 └────────────────┬────────────────┘
                                  ▼
                         【落實憲法 4 步驟】
                  ELI5 + Why 註解 + 更新文件 + 開立 PR
```

- **小型修復與問題排查**：原生流程 + `awm-debugging`。先定位可重現根因，落實最小修改，不產出額外的冗長文件。
- **涉及使用者互動之前端變更**：必備 `awm-frontend-review`，堅持真實操作檢驗。
- **外部資源與第三方工具引入**：必備 `awm-skill-safety`，確認無惡意腳本、環境污染或機密外洩。
- **複雜系統規劃**：視需求借鑑 Spec Kit 的精簡任務拆解或 pstack 的架構探勘模式。
