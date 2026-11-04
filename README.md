<!-- 檔案用途：讓第一次使用的人能選取與採用共用方法。所在層：公開入口。主要關聯：docs/ADOPTION.md、docs/AI_WORKFLOWS.md、TECHNICAL.md、skills/。 -->
# Agent Work Methods

把接手專案、找 bug、審查和檢查介面的方法，裝成可以各自取用的小工具箱。選一個需要的 skill，連同整個資料夾放進你的工具支援的位置；它先看你的專案規則，再協助完成工作。

每個方法都交代「什麼時候用、要看什麼證據、哪裡不能直接下結論」。你的分支、測試命令、語言、產品與發布規則仍由自己的專案決定。

| Skill | 用途 / Purpose |
| --- | --- |
| [awm-onboarding](skills/awm-onboarding/SKILL.md) | 找到入口與檢查 / Repository orientation |
| [awm-debugging](skills/awm-debugging/SKILL.md) | 重現問題並檢查根因 / Root-cause investigation |
| [awm-review-evidence](skills/awm-review-evidence/SKILL.md) | 審查與證據對應版本 / Review and evidence |
| [awm-frontend-review](skills/awm-frontend-review/SKILL.md) | 實際操作與失敗恢復 / User-journey verification |
| [awm-skill-safety](skills/awm-skill-safety/SKILL.md) | 外部 skill 的完整影響 / External skill inspection |

## 開始使用

1. 取得本 repo 的已審查 commit 或版本，閱讀需要的 skill。
2. 複製**整個 skill 資料夾**，包含 `SKILL.md`、`references/`、`LICENSE` 與 `NOTICE.md`。
3. 按所用 agent 的文件放到可發現的位置，或直接提供 `SKILL.md` 路徑要求使用。第一次確認工具實際讀到了它；本 repo 不自動更改工具設定。
4. 專案規則留在專案。更新時先查看差異，再以固定版本更新。

完整步驟見 [採用說明](docs/ADOPTION.md)。不需套件安裝、帳號、付費服務或另一個產品的 checkout；使用文字方法需要能讀檔的 agent，自動發現能力依所用工具而定。

## English quick start

Choose a reviewed revision and copy one complete directory from `skills/` to a location your agent supports, or ask the agent to read its `SKILL.md`. Each skill includes its references and MIT notices, with no links into another product or skill.

These skills supply methods, not project authority. They do not select your framework, package manager, language, branch model, reviewer vendor, push policy, or release permissions. Instructions are in English; guides also introduce their purpose in plain Traditional Chinese.

Read [adoption and updates](docs/ADOPTION.md), [design decisions](TECHNICAL.md), [AI workflows and frameworks](docs/AI_WORKFLOWS.md), and [validation and limits](docs/VALIDATION.md). Format follows the [Agent Skills specification](https://agentskills.io/specification); structural compatibility does not establish integration with every client.

## AI 工作流程、Skills 與框架紀錄

本專案體系所採用、評估與借鑑之各類 AI 工作流程、Skills 與框架（包含 AWM 五大 Skills、GitHub Spec Kit、pstack、Superpowers、BMad Method 等），已統整於 [AI 工作流程與框架清單](docs/AI_WORKFLOWS.md)，提供架構總覽、評估結論與任務選型指引。

## 後續選型研究

固定版本比較後，先以 **Spec Kit v1.2.6 的官方 Lean preset** 做了 Dance Stamp 小任務試用。局部設定與顯式載入可用，但額外文件成本高，尚無更快或更省的證據；這類小修正建議維持原生流程。見 [比較、試用結果與限制](docs/TOOL_EVALUATION.md)。未正式擴大採用，jia-jian-log 尚未試用；獨立 clone＋submodule 的合成證據不代表候選相容。不新增 AWM 流程或 Adapter、不遷移產品副本；既有五個 skills 不受影響。

## 維護與驗證 / Maintenance

Python 3.10 or later runs repository checks without additional packages; Python is not needed just to read or copy a skill.

```sh
python3 scripts/check.py
python3 -m unittest discover -s tests -v
```

`bun run check` is an optional maintainer shortcut for the same commands. Checks validate packaging and representative failures; they do not measure agent quality or certify a skill as safe.

## 授權 / License

[MIT](LICENSE). Origin is documented in [NOTICE.md](NOTICE.md) and [provenance.json](provenance.json). This independent collection does not change any source product's license or behavior.
