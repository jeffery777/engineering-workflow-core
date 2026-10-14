# engineering-workflow-core

純 Markdown 的共用文件契約庫，承載工程工作流、規範、約束、授權邊界、獨立審查、必要安全掃描、exact-head、證據、驗收與停止條件。

**目前是拆分設計草稿。** 本工作包只新增此 README 與三份架構文件，既有 LICENSE 不變；尚未抽離共用契約或改接任何接口。範圍依 [Issue #1](https://github.com/jeffery777/engineering-workflow-core/issues/1) 與使用者本次澄清；後者將核心明定為純文件庫。

## 三個 repository 的責任

| Repository | 責任 | 本包狀態 |
| --- | --- | --- |
| [engineering-workflow-core](https://github.com/jeffery777/engineering-workflow-core) | 共用 Markdown 契約與文件來源／版本說明；可描述流程狀態、必要輸入輸出及證據要求 | 四份設計草稿；不承載 executable、runtime API、validator、installer 或程式套件 |
| [codex-dev-skills](https://github.com/jeffery777/codex-dev-skills) | Codex 技能入口、判定／路由／狀態程式、工具適配、model/effort/profile/session、驗證器、安裝與套件組裝；依固定核心文件契約驗證遵循程度 | 本包唯讀來源；接口準備可由協調者安排，既有程式與安裝未變 |
| [grok-build-dev-skills](https://github.com/jeffery777/grok-build-dev-skills) | 未來 Grok Build 的對應技能／程式接口、模型與 effort、工具／權限／session、驗證器、安裝與組裝 | 可由協調者與 Codex 同步安排唯讀研究／接口設計；實作與 runtime 資格驗證延後 |

依賴方向為兩端接口各自依賴固定核心文件；核心不反向依賴兩端。兩端各自實作 revision/digest、來源與 license notices 的組裝機制，runtime 不追蹤 core `main`。共享 Markdown 不代表工具、隔離或工程行為等價。

子代理可以沿用 parent 的 sandbox 與核准模式，不要求每個子代理建立獨立技術隔離。模型與思考深度按任務需求選擇，由各接口核對實際生效的模型、effort 與繼承／覆寫結果；作者與 reviewer 的獨立性、唯讀工作約束及必要審查仍保留。

「評估 codex-dev-skills 專案拆分」協調對話可安排兩個接口同步進行唯讀相依盤點、官方能力研究與接口設計，與核心契約整理並行。核心契約定稿並固定 revision 後，再安排接口實作；目前維持 Codex 行為，Grok runtime 驗證延後。詳見 [並行準備與實作前置](docs/architecture/migration-plan.md#parallel-preparation)。

## 文件入口

- [責任邊界與官方文件比較](docs/architecture/project-split.md)
- [來源相依盤點與固定 revision 證據](docs/architecture/dependency-inventory.md)
- [分階段遷移、驗收與下一個純文件工作包](docs/architecture/migration-plan.md)

來源盤點固定於 `codex-dev-skills@993597561881d6ed8c552f9a18c59315015ad245`；官方文件查讀日為 2026-10-14。文件記載、設計推論與尚未實測能力分開；歷史 `shared` 標籤或 synthetic fixture 不代表其他 runtime 合格。

## 操作邊界與來源

本包不開始程式搬移，來源專案唯讀。拆分期間不部署、不更新 EdgeInstaller 使用的既有技能、不執行 Grok Build，不啟用 memory/hooks/schedulers，也不操作公司環境或 Orca。Orca 作為可選 host 入口，其操作技能維持上游 ownership。

Commit、push、PR、merge、平台 comment、tag/Release 與部署由來源協調對話另行核對審查、gate 與授權，本包不執行。核心文件描述契約，不能自行攔截 runtime 操作或授予外部寫入權。

本 repository 採 [MIT LICENSE](LICENSE)。未來抽取／組裝來源文件時，須保留來源 [MIT copyright／permission notice](https://github.com/jeffery777/codex-dev-skills/blob/993597561881d6ed8c552f9a18c59315015ad245/LICENSE#L1-L21) 與 provenance，不能以本 repo 的 LICENSE 取代。
