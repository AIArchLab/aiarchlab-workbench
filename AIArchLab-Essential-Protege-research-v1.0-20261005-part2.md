# Essential × Protégé 研究 v1.0（第2部分／共3部分）

## 4. 與AI、未來提案的關聯

建議路徑（設計推論）：

`文件/訪談 → 結構化候選 → 來源/版本 → 本體/資料驗證 → 正式知識層 → 受控檢索 → LLM回答/提案草稿 → 人工核准`

**Ontology-grounded RAG**：不只找相似段落，還查同一情境的流程、資料、責任、控制與來源。

**變更影響**：例如換模型時，列出受影響的資料邊界、控制、驗收與負責人，回答附路徑。

**多agent共同詞彙**：使用相同URI，不再各自解釋「完成」「核准」「可送」。但共用讀取服務還需另建，不因開過Protégé就算部署。

**提案**：從已確認需求、缺口、試點、驗收及排除項生成草稿，不把別案或虛構案例套成客戶事實。

OntoGPT是本體約束抽取的可參考實作，Ollama方向可不花API費；董事長機器上的中文品質、速度與顯存仍未測。不能由「有本體」推成「零幻覺」。[S19]

對外服務可以保持五份交付，但後台讓同一份評估可產生：

- 問題→流程→資料→風險→控制→責任→試點的路徑。
- 改動影響表、證據清單與後續導入scope。
- 有EA成熟度的客戶，再延伸能力／應用／AI治理與roadmap視圖。
- 金融保險用FIBO/BIAN/ACORD作語意參照，標準與客戶現況逐項驗收，不聲稱匯入標準就完成治理。

提案主張：**先把企業事實、責任與邊界接起來，再決定AI做什麼；每個試點留下可重用的模型，未來改動看得出影響。** 本輪不另定價、不發布服務、不承諾量化效果。

## 5. 現有資產已讀到哪裡，如何放

已讀原檔，不改原檔。[I1-I9]

| 既有資產／查證 | Protégé／OWL | Essential |
| --- | --- | --- |
| v9 v0.8：下載358筆完整JSONL及TTL；已有URI/source_ids/provenance/relations，TTL含propertiesJson封裝 | 保留URI；把需要查詢的JSON欄位升成typed properties，分核心/治理/證據模組 | 映射企業與治理概念，用轉換表，不直接灌整份TTL |
| catalog v0.2：完整MD/JSON，693項資產；仍標現用v0.8、未部署 | KnowledgeAsset、AssetVersion、Source、Checksum、supersedes與驗收狀態 | Supporting Documentation／External Reference；693檔不是693應用 |
| 13條件溯源：讀audit與followup JSON；13筆整體組合仍未完整追到，原RAG未改 | Claim→Evidence→SourceLocator；partiallySupports、supportsWholeCondition、verificationStatus分開 | 只接溯源／控制紀錄 |
| TOGAF v4 FINAL：讀README；1753筆=1627 TOGAF+126 Open Footprint；目錄標未併v9 active | StandardConcept/SourceEdition，保留章節edition與evidence。FINAL不是全部Library已完整 | Architecture Standards與reference，標準和客戶現況分開 |
| 六璧合一原型：讀FastAPI程式，query固定回示範值；註解BM25/Qdrant/Neo4j不是實作證據 | 素材放設計候選層，程式標SoftwareArtifact/demo | 原型元件與技術評估，不當已部署服務或成功GraphRAG案例 |
| CoS decision-log v0.2：11筆 | Decision→decidedBy/source/status/affects，缺選項仍來源缺 | Governance decisions/policies與角色專案；slot再按版本映射 |
| CoS conflict-list v0.2：6項 | Issue→Option→Recommendation→Decision；意見與核准分開 | Issue catalogue/change governance；待董事長不是已准 |
| CoS pipeline v0.2：已讀，部分last_checked=null | Opportunity/Proposal/NextAction/ObservedStatus/checkedAt | 連業務服務與專案；不假定免費版內建完整CRM，不把舊狀態當現況 |
| BMC v1：已讀原Doc，價值/通路/收入/活動/角色 | BusinessModel/ValueProposition/CustomerSegment/Channel/Capability/Role | Business目標、能力、組織、value stream；不預設每格有直接class |
| 準備度模板包：讀公開修訂完整內容，三個流程決策卡、燈號、權限矩陣、試點 | Process/AIUseCase/DataCategory/Control/Risk/Owner/Metric/Pilot/AssessmentResult | 能力→流程→應用→資料/技術，串控制與KPI；虛構示範不是客戶成果 |

**基線落差：** 工作紀錄稱v0.9.1，但本次Drive搜尋未找到v0.9系列，已讀catalog仍寫v0.8，私有GitHub內容本輪未能查證。以「取回的v0.8」判斷格式，不說它是最新。正式匯入前鎖定commit/manifest，不需董事長重述知識。

本輪未啟動Protégé、未跑reasoner、未用RDF parser驗證完整TTL，也未測OWL→Frames。因此沒有「已匯入成功」或「已完整OWL驗證」。

建議repository層（設計語彙，不是全為Essential原生class）：

- core：能力、流程、應用、資料、角色、AI情境。
- governance：風險、控制、評估、決策、議題、例外、KPI、試點。
- evidence：Claim、Evidence、SourceLocator、版本、checksum、映射依據。
- standards：領域標準參照與對應，來源性質分開。
- internal-method：內部融合方法，只留私有層。
- client-{id}：各客戶實際instances與證據。
- demo-retail：銳電3C，假設、目標、量測值分開。

以橋接mapping保持兩邊ID，不要求同一檔滿足所有工具。

## 6. 小例子：銳電3C LINE回覆

已公開模板的事實：一家門市、店長具名公司帳號、去識別、只起草、人工核對及送出，退換貨與金額由人確認；40→15分鐘是示範基準與目標，不是績效。[I9]

```text
目標：改善回覆速度，不擴大錯誤客訴
→ 能力：顧客服務
→ 流程：門市LINE詢問與客訴回覆
→ AI情境：只產生草稿
  ├ reads：去識別客訴、公開商品資料
  ├ excludedInput：姓名、電話、訂單編號、成本底價
  ├ controls：去識別、具名帳號、人工核對、人工送出
  ├ accountableRole：店長
  └ assessment：先修再做
       → requires：20則去識別歷史訊息測試通過
       → plannedIn：第1梯兩週試點
```

已查Essential 6.20概念文件的Business_Capability、Business_Process、Application_Provider、Information_Concept；AI情境/控制/證據仍要橋接，不能冒充現成class與slot。[S26]

```turtle
@prefix a: <urn:aiarchlab:demo:> .
@prefix g: <urn:aiarchlab:proposal-vocab:> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
a:lineReplyPilot a g:Pilot ;
  g:targetsProcess a:lineReply ;
  g:usesAIUseCase a:draftOnly ;
  g:accountableRole a:storeManager ;
  g:hasControl a:deidentify, a:humanReview, a:humanSend ;
  g:hasMetric a:replyTarget ;
  g:assessmentStatus "先修再做" ;
  g:caseType "fictional_demo" ;
  g:evidenceSource a:templatePack .
a:replyTarget a g:Metric ;
  g:unit "minute" ;
  g:targetValue "15"^^xsd:decimal ;
  g:baselineIllustration "40"^^xsd:decimal ;
  g:valueKind "illustrative_target_not_measured" .
```

只作映射說明，不是部署包，未改v9；URN是識別碼不是網頁。
