# Reviewer 路徑與委派證據／Reviewer routes and dispatch evidence

本文件是 [#38](https://github.com/jeffery777/engineering-workflow-core/issues/38) 與 [#40](https://github.com/jeffery777/engineering-workflow-core/issues/40) 的非權威伴讀。規則以 [review-required-read-only](../../contracts/review-and-security.md#review-required-read-only)、[wf-capability](../../contracts/workflow.md#wf-capability) 及 [wf-delegation](../../contracts/workflow.md#wf-delegation) 為準。以下均是假設情境，不是實測、接受紀錄或 runtime 資格證據；案例編號只供本文件對照，不是新規則或 gate。

## 繁體中文

### #38：區分路徑、位置與環境

reviewer 路徑描述審查實際如何執行；檔案位置可能是環境綁定的一項資料，不能單獨證明工具、權限、資源或接受範圍仍相同。以下判讀保留 [#23 的完整接受機制](../../contracts/review-and-security.md#review-required-read-only)，不提供任何環境的接受。

| 案例 | 假設情境 | 判讀 |
| --- | --- | --- |
| 38-A | repository 目錄沒變，但替代 reviewer 多了可寫工具 | 核對新的有效通道及接受範圍；目錄相同不足以沿用接受或證明技術唯讀。 |
| 38-B | reviewer 的模型名稱改變，其他條件看似相同 | 核對模型／資格及接受是否仍適用；不因名稱改變一律重取接受，也不推定其他條件真的未變。環境或規則實際改變時仍依原文處理。 |

### #40：各次核對不等於各次重新探測

來源層次應清楚：requested 是請求設定，recorded 是介面或 host 的記錄值，effective 是實際生效值。來源支持哪一層，就只作該層的判定；記錄或自述不自動證明實際生效。

| 案例 | 假設情境 | 判讀 |
| --- | --- | --- |
| 40-A | 本次沿用 parent；已有適用且仍有效的繼承機制與設定證據 | 核對本次綁定及重用條件，可重用充分的證據，不必另跑探測。 |
| 40-B | 只覆寫 model，agent 定義仍有 effort 設定 | 依該介面的有效繼承／覆寫機制核對 effort 來源，不能假定它隨 model 或 parent 改變。 |
| 40-C | 介面、profile、設定或證據假設有影響判定的漂移 | 補查受影響部分；舊 PASS 不能跨越未核對的變更。 |
| 40-D | 合法可取得的必要證據未讀，只因想省成本 | 如實記未讀，不能稱沒有證據或不可觀察，也不能用 unknown 表示必要核對完成。 |
| 40-E | 介面沒有支援的觀察方式，或必要讀取受限／失敗 | 分別記明限制與未確認範圍；不能虛構探測或把失敗記成通過。 |
| 40-F | host 記錄只反映 requested 值 | 可確認其 recorded 值；未有相稱佐證時，effective 仍未確認。 |
| 40-G | 必要 reviewer 資格仍無法確認 | 依既有 fallback／停止條件處理，停止相依 gate；不以作者自審、成本或其他環境的接受補足。無相依安全工作可續。 |
| 40-H | 仍有效的充分證據已涵蓋本次判定，但還有重複記錄可讀 | 可說明適用性後重用，不要求為重複而讀取每一筆記錄；新反證或漂移須納入重評。 |

這些判讀不新增通用探測器、固定 model／effort、每次 host record 讀取、新 gate、通用 receipt 或必要資格豁免。實際接口採用、固定版本、完整清冊／digest／引用閉包及驗證仍由各 consumer 另行處理。本包不納入 #39；跨接口條文仍待 M1 PoC 證據，不由本文件啟用資料傳送或其他機制。

## English

This is a non-authoritative companion for Issues #38 and #40. The linked contracts govern. Every case is hypothetical, not a measurement, acceptance record or runtime qualification. Case IDs are local references, not new rules or gates.

### #38: Route, location and environment

A reviewer route describes how the review runs. A file location can help bind an environment, but does not alone prove unchanged tools, permissions, resources or acceptance scope. Keep the complete #23 acceptance mechanism; this document supplies no acceptance.

| Case | Hypothetical condition | Interpretation |
| --- | --- | --- |
| 38-A | The repository directory stays the same; a substitute reviewer has added write tools. | Check effective channels and acceptance scope. The directory alone proves neither applicable acceptance nor technical read-only control. |
| 38-B | The model name changes; other conditions appear unchanged. | Check model qualification and acceptance applicability. A name change alone does not require renewed acceptance or prove other conditions unchanged. Apply the original rule when the environment or rules actually change. |

### #40: Check each dispatch; reuse applicable evidence

Requested means the settings sent in the request. Recorded means values reported by the interface or host. Effective means the settings actually in effect. Keep each conclusion within the evidence's supported layer; a record or self-report does not automatically prove effective settings.

| Case | Hypothetical condition | Interpretation |
| --- | --- | --- |
| 40-A | The dispatch inherits parent settings, with valid applicable evidence of the mechanism and settings. | Check the current binding and reuse conditions. Sufficient evidence can be reused without another probe. |
| 40-B | Only the model is overridden; the agent definition still sets effort. | Check the effort source under that interface's effective inheritance/override mechanism. Do not assume effort follows the model or parent. |
| 40-C | Interface, profile, settings or evidence assumptions drift in a way that affects the decision. | Recheck the affected part. An old PASS does not cover unchecked changes. |
| 40-D | Necessary evidence can lawfully be read, but is left unread to save cost. | Record it as unread, not absent or unobservable. Unknown does not complete the necessary check. |
| 40-E | The interface has no supported observation method, or a necessary read fails or is restricted. | Distinguish these limits and the unverified scope. Do not invent a probe or report success. |
| 40-F | The host record only reflects requested values. | It can establish recorded values. Effective settings remain unconfirmed without sufficient support. |
| 40-G | Required reviewer qualification remains unconfirmed. | Use existing fallback/stop rules and stop the dependent gate. Author self-review, cost or another environment's acceptance cannot fill the gap. Independent safe work may continue. |
| 40-H | Valid sufficient evidence covers this dispatch, while duplicate records are also available. | Explain applicability and reuse it. Reading every duplicate record is not required; reassess new counter-evidence or drift. |

These cases add no general detector, fixed model/effort, per-dispatch host-record read, gate, receipt or qualification exemption. Consumer adoption still needs its own fixed revision, complete inventory/digests/reference closure and verification. Issue #39 remains outside this packet, pending M1 PoC evidence; this document enables no cross-interface data transfer or mechanism.

English technical text uses ASD-STE100 principles. Full conformance has not been verified. Traditional Chinese uses natural Taiwan wording without claiming an official Chinese ASD standard.
