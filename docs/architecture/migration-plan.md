# 純文件核心的分階段遷移計畫

本計畫依使用者本次澄清，只規劃共用 Markdown 文件抽取與接口改接；本包仍只有四份設計草稿，沒有程式搬移或安裝。邊界見 [project-split](project-split.md)，來源與相依見 [dependency-inventory](dependency-inventory.md)。本包範圍依 Issue #1 與使用者本次澄清；核心定位以純 Markdown 為準。

## 目標與固定來源

共用核心只承載工作流、規範、約束、授權、獨立 review、必要 scan、exact-head、證據、驗收與停止條件的 Markdown。兩個接口可由協調對話同步安排唯讀準備，實作待核心契約定稿並固定 revision；目前維持 Codex 行為，Grok runtime 資格驗證延後。來源為 `codex-dev-skills@993597561881d6ed8c552f9a18c59315015ad245`，核心起始為 `a323567cfe838582d0be749343830b81aac20bc8`；每個新包重新核對 local/remote branch、upstream、scope/ownership、HEAD/dirty diff 與正式指引。

本包與拆分期間不部署、不更新 EdgeInstaller 使用的既有技能、不執行 Grok Build、不啟用 memory/hooks/schedulers，不連線公司環境。來源專案唯讀；四文件之外不新增 AGENTS、程式、validator、installer、catalog、CI 或套件。後續階段是提案，不授權提前開始。

## 最小切片與順序

| 階段 | 產物／責任專案 | 前置與最小 DoD |
| --- | --- | --- |
| P0 本次設計 | Core 的四份 Markdown | 官方六面向比較／文件與實測區分、固定來源盤點、單向依賴、純文件下一包；links/references/scope/LICENSE invariant；獨立 docs review |
| P1 共用文件契約抽取 | Core 只新增／修改 Markdown：工程流程、授權與證據、review/scan、exact-head、停止／延續、來源 notices | P0 dispositions；新包 scope/Issue/branch；逐條來源對照、義務不減、relative links 閉合、固定 revision、獨立文審；無 executable／validator／schema file／installer／程式套件 |
| P2 兩端唯讀接口準備（可與 P0/P1 並行） | Codex／Grok 各自的相依盤點、官方能力研究、接口設計／遵循矩陣 | 協調者指定有界 scope/ownership 與來源；可引用標明版本／假設的核心草稿。核心定稿後核對固定 revision/digest 與設計漂移；不實作、不安裝、不執行 Grok Build |
| P3 Codex 有界改接（另包） | Codex 自己實作文件 lock/digest/allowlist/provenance 組裝與既有入口改接；程式仍留 Codex | 核心契約已定稿並固定 immutable revision/digest，P2 設計對齊並經審查／新包授權；每次完整 producer/consumer/test family；source/plugin/temp-filesystem parity、必要 validators/evals/tests、review／scan/gate；維持 Codex 行為，不因共享文件宣稱 runtime 合格 |
| P4 Codex 遵循驗證 | Codex 各 surface 的工程契約遵循紀錄 | CLI/CLI-TUI/Desktop/bundled CLI 各自 identity/capability／權限／readback／負面案例；正式 exact-head 與 project profile另驗；不承接舊 repo/head receipt |
| P5 Grok 實作與 runtime 資格（延後） | Grok repo 自行實作技能、模型／effort、工具、權限/session、validator/installer/組裝；core 不變成 API | 唯讀設計在 P2 可先進行；實作仍須核心契約定稿、固定 revision 與另包審查／授權。runtime 驗證待另行授權執行 Grok Build；核對 session 歧義、review/scan/權限與失敗恢復證據 |
| Consumer rollout（不屬拆分包） | 各使用專案精確版本／安裝／部署 | 另行選 consumer/environment、preview、backup/readback、rollback、授權／gate；EdgeInstaller 不自動更新 |

P1 只抽文件；P2 只有兩端唯讀準備，P3/P4 的程式與遵循驗證在 Codex repo，Grok 的對應實作在 P5 延後安排。Core 不新增 `src/`、Python 判定、router、state machine、runtime API、schema/validator、installer 或程式 package。現有 loop／graph／profile／session 等可執行來源不移入 core；保留延後功能不因階段轉換被啟用。

<a id="parallel-preparation"></a>

## 並行準備與實作前置

P2 是準備工作的分類，不是必須等 P1 結束才能開始的時間順序。「評估 codex-dev-skills 專案拆分」對話可同步安排兩個接口的唯讀盤點、官方研究與接口設計，與 P0/P1 核心文件工作並行；各工作包保留來源 revision、假設、ownership、輸出與未測能力。本對話仍只修改四份核心設計文件，不自行修改或派工至接口專案。

任何接口實作開始前，都須由協調者核對核心契約已定稿、引用完整 immutable revision/digest、接口設計與最終契約一致，以及該包的審查與授權。定稿前的接口設計是準備證據，不能當作已改接或 runtime 合格；契約漂移時重查受影響部分。先維持 Codex 行為，Grok runtime 驗證延後，部署與 EdgeInstaller 既有技能更新仍不在拆分範圍。

子代理可沿用 parent 的 sandbox 與核准模式，不要求逐一建立獨立技術隔離。主代理按任務需求選擇模型／effort，由各接口查實際生效的繼承或覆寫設定、有效權限與必要資格；作者／reviewer 獨立、唯讀約束及主代理整合責任保留。模型選擇與設定程式不搬入純 Markdown 核心。

## 固定文件版本與接口組裝機制

下表為各接口未來必須實作的建置義務；核心以 Markdown 描述要求，不提供 manifest 程式／machine-readable schema 或組裝器。

| 接口的鎖定與產物 | 必須保留的資訊／行為 |
| --- | --- |
| Core 文件來源 | exact version（若已發布）、immutable revision、每份 Markdown path+digest、定義清楚的文件集合 digest；commit 不等於 source/package/publication 的全部真相 |
| 接口身分 | adapter repo/revision/version、使用的核心契約章節與revision、組裝器版本、layout 與驗證環境 |
| Provenance／notices | 原 repo/revision/path/digest、抽取／修改說明、derived 位置、來源 MIT notices；機器 manifests 與資料 schema 留接口 |
| 建置完整性 | 先驗 immutable revision/digest／allowlist／完整 dependency closure，再組裝固定本地佈局；bytes/modes/inventory／非 symlink/path safety／duplicate-skill safeguards |
| Runtime | 只使用已組裝固定文件；不追蹤 core `main`，不在執行時下載可變規範，不悄悄改資料目的地或權限 |
| 更新 | Core revision/digest 或文件義務變更觸發接口的受影響遵循驗證與review；不能用 old receipt或文案重排證明新內容通過 |

Generated copies 保持唯一 source；Codex 上層來源與 `sync-plugin-package.py` 的 allowlist/逐檔驗證仍由 Codex 負責，不能手改 plugin copies。Core 文檔 lock、Codex catalog/version、plugin manifest、filesystem installer 手寫 lists 的一致性與 source/plugin/temporary filesystem 三佈局在接口驗證。[E18](dependency-inventory.md#e18) [E19](dependency-inventory.md#e19) [E30](dependency-inventory.md#e30)

待接口實作時需有 missing/tampered document、wrong revision/digest、漏必讀文檔、broken relative link、未知契約 revision、來源混淆、duplicate skill、permission widening 與載入錯誤的負面案例。這些測試／validator 不放核心，也尚未在本包執行。

## 兩端各自證明契約遵循

| 共用文件義務 | Codex 接口的驗證規劃 | Grok 接口（延後） |
| --- | --- | --- |
| 適用契約載入 | 核對實際技能、sibling references、固定文件 bytes/digest；source/plugin/temp-filesystem 三佈局 | 自己核對發現／載入順序、frontmatter 未套用欄位、references 與完整契約 |
| 正常工具與授權 | 用當次公開 schema/permissions/host 查工具，核對 precise operation/approval/readback；保持原工具與策略 | 重新確認自己的 toolsets/permissions/sandbox/model/data destination；不能複製 Codex payload |
| 模型／effort 與子代理設定 | 按任務選擇；符合需求時可沿用 parent model/effort、sandbox／核准模式。接口查實際繼承／覆寫設定，不用 role prompt 假定生效，不要求每個子代理另建 sandbox | 自己研究設定優先序與公開查核方式；實際生效與必要資格待另包驗證，不能借 Codex 設定／證據宣稱通過 |
| 獨立 review／必要 scan | 角色／scope/tier/profile preflight、作者獨立、coverage/完成與finding disposition | 自建合適獨立 review/scan 接口及資格；工具存在與 child context 不等於通過 |
| 證據／exact-head | 固定來源/diff/range、必要 validators/tests/CI、code/docs/coherence，changed-head 全 range重審 | 同樣工程義務、自己的完整結果與信任來源；Grok session/goal summary不是repo驗收 |
| 停止與恢復 | missing capability/evidence、ownership conflict、timeout/unknown effects、true human gate；驗 native/runtime fallbacks | 各自 negative/recovery cases；先處理官方 session 表述差異再設計 mutation |

共用 Markdown 只統一義務，不證明動態行為、tool coverage、成本、模型品質、OS isolation 或結果等價。本包官方查讀屬於文件證據；兩端 runtime 資格都未由此建立。[官方比較](project-split.md#official-comparison)

來源 `verify-engineering-workflow.py` 只接受固定 Codex/Hermes synthetic labels，輸出 false-readiness；它與所有既有 tests/evals仍由接口專案持有，不因分享規範變成 core executable，也不宣稱 Grok 支援。[E33](dependency-inventory.md#e33)

## 下一最小工作包：P1 純 Markdown 契約抽取

建議只做六份候選契約與來源對照，保持 Codex 程式、技能入口、installer、plugin 與現有安裝完全不改接。協調者可同時安排兩端唯讀接口設計；核心契約定稿並固定 revision 後，才進入接口實作。

| 項目 | 具體候選／驗收 |
| --- | --- |
| 可抽文件來源 | `policies/engineering-workflow-contract.md`、`reusable-workflow-contract.md`／`reusable-workflow-details.md`、`exact-head-merge-review-contract.md`；按義務抽取，保留原來源與Codex特定範例分界，不搬 source executables |
| Core 新檔提案（全 Markdown） | `contracts/workflow.md`、`contracts/authorization-and-stops.md`、`contracts/review-and-security.md`、`contracts/exact-head-and-evidence.md`、`docs/provenance/source-map.md`、`docs/provenance/upstream-notices.md`；README／本次架構入口視需要同步，既有 LICENSE不變 |
| 前置 | 新包明確 scope/Issue/branch與current source/target readback；P0 findings有disposition；單一 writer；官方對照與來源 revision；原 copyright/permission notices |
| DoD | 每項共用義務逐條對照來源 file/section/lines；保留授權、破壞性 safeguards、獨立 review、必要 scan、exact-head、DoD/證據與停止；明定子代理可沿用 parent sandbox／核准模式、按任務選 model/effort 並由接口查生效；不載入 Codex/Grok API 或模型配置；引用與 notices 完整，契約定稿並固定 revision 後才安排接口實作 |
| 驗證 | 只用本機／接口外部檢查做 Markdown links/anchors、固定source revision/line/symbol、義務對照、diff/scope/LICENSE；來源只讀；獨立 docs review。檢查程式可以由接口或有界臨時工具執行，不能新增至核心 |
| 延後 | Codex文件 lock/validator/assembler/install/package/runtime 改接，所有可執行程式搬移；Grok實作/資格、memory/Hermes/provider/索引/hook/scheduler、tag/Release/deploy |

候選路徑為下一包提案，本包沒有新增它們。該包完成也只證明文件契約經審查，不能說接口已經遵循或已抽離程式。實作、平台與發布權仍由協調者／使用者在該包另行界定。

## Source notices、回復與非部署界線

抽取或組裝 substantial portions 時隨附來源 `Copyright (c) 2026 YANG CHUN CHIH` 與 MIT permission/warranty notice；目的 `Copyright (c) 2026 jeffery777` 不能取代來源 notices。Core 可以在 Markdown provenance/notices 記錄原文與來源，接口在產物保留完整license。新的第三方內容先查授權，不因兩repo都MIT略過provenance。[E20](dependency-inventory.md#e20)

未部署階段保留原來源與接口 last verified document revision/digest。新文件／接口組裝驗收失敗就不 promotion；在臨時目錄以舊固定契約重建。已經受託改 source 的包以可審revert commit恢復，不 force push/覆寫歷史/自動刪資料；回復同樣核對授權/ownership。上述是計劃，不是已測rollback。

Consumer install/deploy 另案先有精確目標、preview、資料影響、backup/readback、原版本/digest與復原路徑，再核對授權/gate；拆分或文件發布不自動授權更新既有技能。EdgeInstaller 保持原限制。

## 本包驗證與審查

四文件一致性／純 Markdown責任、local links/anchors、固定來源permalink／檔案行號／符號、53 scripts/97 個 tests/62 個 eval與資源盤點、繁體中文、`git diff --check`／新增文件whitespace、exact four-file scope 與LICENSE bytes/digest；必要Python查核使用來源 `./scripts/project-python` 和 `PYTHONDONTWRITEBYTECODE=1`，不安裝、不寫source cache。

獨立唯讀docs review檢核本次澄清與當前內容digest、官方引用與來源代碼。純設計未改實際trust/permissions/executable/dependencies/installation，Security Diff Scan適用性須記錄scope與理由，不能把未執行scan記為passed。來源全測/eval、installer/package/lifecycle均不執行，不宣稱其pass或runtime合格。[E15](dependency-inventory.md#e15)

完成後停止寫入並交回來源協調者。正式commit/PR/merge gate、新head的complete range review、平台comment/tag/Release/deploy由協調者依當前證據執行，不復用舊repo receipt作新repo readiness。

## 未決／未驗證事項

- 核心契約尚未正式抽取或發布；接口引用/lock/digest/組裝還未實作。P1/P2路徑與接法是提案。
- 官方Grok session文檔有表述差異；其實際行為與live工具/權限/隔離/review/scan資格延後，不以文檔互換schema。
- Codex各surface的契約遵循尚未因本包重新資格化；歷史／installed/profile/status不是當前完成證據。
- 使用專案forge profile/CI/consumer環境尚未選定，來源repo專用App/ruleset不默套。
- 本包以用戶最新澄清為範圍；若協調者後續修改Issue/body須另依平台權限。來源／ownership衝突或需擴大scope時停止相依修改、先完成安全查讀。
