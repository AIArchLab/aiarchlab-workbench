# Essential × Protégé：AIArchLab 的知識與提案骨架

研究定稿 v1.0 | 2026-10-05，Asia/Taipei | 內部研究，供董事長與 CTO 討論

## 結論

**Essential 管「企業如何運作、改動會影響誰」；Protégé 管「概念如何定義、關係與推論是否一致」。** 不是兩套互相替代的AI工具。

對我們的價值，是把評估模板、治理規則、標準摘要、來源、決策紀錄用共同ID串起來。日後提案能從同一份事實底稿產生，評估也能接成可維護的企業架構知識庫。

推薦 A：先定最小共同模型和驗收問題，沿用既有私有資產，以銳電3C示範映射。之後先用Protégé驗證知識，再決定是否部署Essential作企業架構展示。不先買平台，不把建模工具當成RAG後端。

本輪只有讀取研究與檔案檢視，沒有安裝、啟動服務、匯入外部平台、修改原檔或購買。以下匯入與提案方案都是設計推論，未冒充實測。

## 1. 官網實際是什麼

### Enterprise-architecture.org：The Essential Project

這次入口顯示的是 Enterprise Architecture Solutions Ltd 的 The Essential Project，不能只稱為「Enterprise Architecture Center of Excellence」。它提供Essential企業架構工具、Essential University、meta-model、建模教學及開源程式。[S1-S4]

核心是企業架構本體：目標、能力、流程、組織、應用、資料、技術互相關聯，再由repository產生視圖。

- 四層：Business、Application、Information、Technology。
- 三種抽象層：Conceptual、Logical、Physical。
- 支援策略、變更、標準、治理決策、控制、績效、成本、生命週期等。
- 官網說可對映TOGAF、FEAF、MODAF；不是替代TOGAF，也不是所有映射都算官方認證。[S3]

| 版本 | 已查證的能力／界線 | 我們的選擇 |
| --- | --- | --- |
| Open Source | 免費、自行維運、約140種視圖、Excel匯入；使用Essential維護的Protégé fork | 零軟體費的試驗候選，本輪不部署 |
| Cloud | 付費託管、較完整REST API、企業編輯介面 | 不符合本輪零支出 |
| Docker | 官網列商業授權 | Docker不等於開源免費版 |

首頁商業年費不能用來否定免費版。[S1,S2,S4,S6]

**相容性重點：** Essential有Protégé Frames淵源；Stanford現行Desktop則是OWL 2。官方《What about OWL?》明說選Frames，但文章首發於2010年，需搭配現行Overview的「維護中的fork」一起看，不能拿舊文代替今天的全部相容性驗證。不能承諾v9 Turtle直接匯入Essential就保留全部OWL語意。[S4,S7]

### Stanford Protégé

免費開源OWL本體編輯器。Desktop支援OWL 2、reasoner介面（HermiT、Pellet等）、推論說明、重構及外掛；WebProtégé支援協作、權限、討論、變更歷史、Turtle/RDF/XML等格式交換。[S13-S16]

適合我們用來定義class、individual、property，檢查知識模型，review FIBO對應，管理本體模組。它不自動提供向量檢索、正式SPARQL服務、多agent存取介面、提案流程或生產級API。reasoner一致性也不等於內容真實或來源完整。[S13,S20]

## 2. 挖出的開源工具與AI整合

| 專案 | 能力 | 授權查證／採用界線 |
| --- | --- | --- |
| Essential Viewer | 架構視圖、XSL報表與儀表板 | 官方repo列GPL-3.0；官網核心元件按版本為GPLv3或AGPLv3 |
| Essential Import Utility | 試算表→匯入規格→測試→repository | 官方開源專案；精確元件版本授權仍要核，官網另列ZK EE/ZOL |
| Essential View Builder MCP | 產生XSL/API scaffold、檢查欄位、參考視圖程式 | 官方公開repo；本次未找到獨立LICENSE。它是視圖開發助手，不是通用企業知識查詢MCP |
| Essential widgets / contributions / viewer-i18n | 編輯器widget、視圖與修補、翻譯檔 | 官方公開repo；本輪未逐一核對元件LICENSE，先當研究素材 |
| Protégé Desktop / WebProtégé | OWL編輯、協作、reasoner介面 | 兩個repo的license.txt均為BSD 2-Clause |
| Cellfie | Excel→OWL axioms、保存轉換規則；自Protégé 5.0.0起隨安裝包提供 | 官方repo證實功能，獨立license檔本次未查得 |
| OntoGraf / OWLViz | OWL關係互動圖／class階層圖 | 官方repo；本次未逐一核對LICENSE |
| SWRLTab | SWRL規則與SQWRL查詢環境 | 官方wiki證實功能，但授權欄為not available；不當正式政策引擎承諾 |
| OntoGPT / SPIRES | LLM抽取結構化內容、ontology grounding；支援Ollama本地模型路徑 | 獨立第三方專案，BSD 3-Clause；不是Stanford官方外掛 |

來源：[S6,S8-S12,S15-S19,S23-S25]。授權只做技術清單，不展開法律討論；免費原始碼不代表不用維運。

兩個需要保留的差異：

1. Essential免費版產品表寫API「No」，University Overview又寫有simple API。可確定的是不應承諾免費版有Cloud約80個REST API；實作要按版本確認。[S2,S4]
2. Essential官方AI文章展示ontology/MCP的價值，但「降低幻覺」是供應商主張，不是我們已做的效果驗證。公開View Builder MCP的README支持的是視圖開發能力。[S5,S10]

## 3. 方法論：不是先把所有文件塞進去

### Essential方法：先定決策，再補企業事實

- 先問這個模型要支援什麼：試點能否做？退掉系統影響哪些流程？
- 四層×三抽象層分清楚：「客服能力」「客服作業」「LINE系統」不是同一件事。
- 用既有meta-model建立instances，真的不夠才擴充class。
- Launchpad由既有Excel建立基礎視圖，再擴到策略、控制框架、供應商、KPI。
- Import Utility分資料來源、轉換規格與目標repository，先測試視圖再套入。[S3,S7,S9,S11]

### Ontology Development 101

Noy與McGuinness的七步：界定領域與範圍 → 重用既有本體 → 列術語 → 定classes與階層 → 定properties → 定限制 → 建instances。用competency questions驗收，不用class數量驗收。這是基礎方法，不是最新產品操作手冊。[S22]

第一批驗收問題：

1. AI情境支持什麼目標與流程？
2. 讀什麼資料，哪些不能進模型？
3. 誰能產生、核准、對外送出？
4. 哪個控制處理哪個風險，證據在哪？
5. 判斷是標準、內部決策、虛構案例或AI自關聯？
6. 來源支持條件的一部分，還是整個組合？
7. 改模型、系統或欄位，影響哪些試點及交付？
8. 未決、核准、執行、驗收、暫停如何區分？誰決定、何時決定？

### 四種檢查要分開

| 檢查 | 管什麼 |
| --- | --- |
| OWL推論 | 概念分類、已宣告語意的邏輯一致性與推論 |
| SHACL | RDF實際資料是否滿足欄位、關係與限制 |
| JSON Schema | JSON交換結構，沿用我們已有schema |
| 執行政策／人工核准 | 行動能不能發生，上線與回滾誰決定 |

OWL採開放世界，沒寫不能直接推成不存在；OWL必要property也不等於檔案必填欄位被檢查。SHACL與JSON Schema才處理資料門檻，但同樣不能證明來源事實為真。[S20,S21]

## 4. 與AI、未來提案的關聯

建議路徑（設計推論）：

`文件/訪談 → 結構化候選 → 來源/版本 → 本體/資料驗證 → 正式知識層 → 受控檢索 → LLM回答/提案草稿 → 人工核准`

**Ontology-grounded RAG**：不只找相似段落，還查同一情境的流程、資料、責任、控制與來源。

**變更影響**：例如換模型時，列出受影響的資料邊界、控制、驗收與負責人，回答附路徑。

**多agent共同詞彙**：使用相同URI，不再各自解釋「完成」「核准」「可送」。但共用讀取服務還需另建，不因開過Protégé就算部署。

**提案**：從已確認需求、缺口、試點、驗收及排除項生成草稿，不把別案或虛構案例套成客戶事實。

OntoGPT是本體約束抽取的可參考實作，Ollama方向可不花API費；Allen機器上的中文品質、速度與顯存仍未測。不能由「有本體」推成「零幻覺」。[S19]

對外服務可以保持五份交付，但後台讓同一份評估可產生：

- 問題→流程→資料→風險→控制→責任→試點的路徑。
- 改動影響表、證據清單與後續導入scope。
- 有EA成熟度的客戶，再延伸能力／應用／AI治理與roadmap視圖。
- 金融保險用FIBO/BIAN/ACORD作語意參照，標準與客戶現況逐項驗收，不聲稱匯入標準就完成治理。

提案主張：**先把企業事實、責任與邊界接起來，再決定AI做什麼；每個試點留下可重用的模型，未來改動看得出影響。** 本輪不另定價、不發布服務、不承諾量化效果。

## 5. 現有資產已讀到哪裡，如何放

Drive帳號：braincat@gmail.com。已讀原檔，不改原檔。[I1-I9]

| 既有資產／查證 | Protégé／OWL | Essential |
| --- | --- | --- |
| v9 v0.8：下載358筆完整JSONL及TTL；已有URI/source_ids/provenance/relations，TTL含propertiesJson封裝 | 保留URI；把需要查詢的JSON欄位升成typed properties，分核心/治理/證據模組 | 映射企業與治理概念，用轉換表，不直接灌整份TTL |
| catalog v0.2：完整MD/JSON，693項資產；仍標現用v0.8、未部署 | KnowledgeAsset、AssetVersion、Source、Checksum、supersedes與驗收狀態 | Supporting Documentation／External Reference；693檔不是693應用 |
| 13條件溯源：讀audit與followup JSON；13筆整體組合仍未完整追到，原RAG未改 | Claim→Evidence→SourceLocator；partiallySupports、supportsWholeCondition、verificationStatus分開 | 只接溯源／控制紀錄；不把奇門六壬條件內容放客戶或公開repository |
| TOGAF v4 FINAL：讀README；1753筆=1627 TOGAF+126 Open Footprint；目錄標未併v9 active | StandardConcept/SourceEdition，保留章節edition與evidence。FINAL不是全部Library已完整 | Architecture Standards與reference，標準和客戶現況分開 |
| 六璧合一原型：讀FastAPI程式，query固定回示範值；註解BM25/Qdrant/Neo4j不是實作證據 | 素材放設計候選層，程式標SoftwareArtifact/demo | 原型元件與技術評估，不當已部署服務或成功GraphRAG案例 |
| CoS decision-log v0.2：11筆 | Decision→decidedBy/source/status/affects，缺選項仍來源缺 | Governance decisions/policies與角色專案；slot再按版本映射 |
| CoS conflict-list v0.2：6項 | Issue→Option→Recommendation→Decision；意見與核准分開 | Issue catalogue/change governance；待Allen不是已准 |
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

## 7. A／B／C選單與推薦

| 選項 | 下一步 | 驗收 |
| --- | --- | --- |
| **A. 模型與映射先行（推薦）** | 鎖最新基線，定核心詞彙、8個驗收問題、來源/版本欄位；一個銳電3C流程做兩邊映射規格 | 每問能用ID/關係/來源回答；假設不混實測，不改原檔 |
| B. 本體工作台先行 | A後用Protégé本地副本檢查，少量FIBO對應，另設SHACL | 語法/一致性、缺欄位、樣本問答、checksum差異 |
| C. EA展示先行 | A後試Essential Open Source，Launchpad匯入銳電3C，產生架構/影響視圖 | 能力→流程→應用→資料→控制路徑、匯入差異及回復方法 |

推薦A→B→C。A後也可因提案需求先選C，但不跳過模型與來源。B/C尚未啟動，部署/query engine仍是另一個待決題。

CTO討論應聚焦：OWL→Frames哪些語意要保留；class/slot映射；需不需要少量擴充；現有propertiesJson哪些拆欄位。用具體欄位、版本、原始來源回答，不再交泛泛工具介紹。

## 8. 剩下的查證／實測

免費版API、版本相容性、完整TTL語法/一致性、OWL→Frames、中文本地抽取尚未實測。MCP與部分外掛獨立LICENSE未查得，保留未確認。沒有把「有本體」當成「來源真實」「零幻覺」「政策已執行」。

本文件不含奇門／六壬內部條件內容，例子只用公開銳電3C。CoS案件狀態只作欄位素材，不重新宣稱現況。這是新研究v1.0，不代表已融合、已部署或已批准上架。

## 來源與內部原件

- [S1] Essential官網入口：https://enterprise-architecture.org/#。用途：產品身份；商業首頁與免費版須分開。

- [S2] Essential Open Source：https://enterprise-architecture.org/products/essential-open-source/。用途：免費版、版本比較、視圖/API差異。

- [S3] Essential Meta Model Overview：https://enterprise-architecture.org/university/essential-meta-model-overview/。用途：四層×三抽象層；標準對映與治理。

- [S4] Open Source Overview：https://enterprise-architecture.org/university/open-source-overview/。用途：維護中的Protégé fork；simple API。

- [S5] AI and Essential：https://enterprise-architecture.org/about/thought-leadership/ai-and-essential/。用途：供應商AI與上下文主張，非效果實測。

- [S6] Essential Licensing：https://enterprise-architecture.org/about/licensing/。用途：GPL/AGPL、ZK、商業Docker。

- [S7] What about OWL?：https://enterprise-architecture.org/about/thought-leadership/what-about-owl/。用途：2010文章，Frames選擇與instance-first方法。

- [S8] Essential Viewer repository：https://github.com/essentialproject/essential_viewer。用途：GPL-3.0；視圖源碼。

- [S9] Import Utility Guide：https://enterprise-architecture.org/university/using-the-essential-import-utility/。用途：試算表、匯入規格、測試/套入流程。

- [S10] View Builder MCP：https://github.com/essentialproject/essential-view-builder-mcp。用途：視圖/XSL/API scaffold，不是通用知識查詢MCP。

- [S11] Essential Launchpad：https://enterprise-architecture.org/products/essential-launchpad/。用途：由資料建立基礎與進階視圖。

- [S12] Essential ecosystem：https://github.com/essentialproject。用途：Viewer/import/widgets/contributions/i18n；已讀各repo。

- [S13] Protégé入口：https://protege.stanford.edu/。用途：OWL本體編輯器身份。

- [S14] Protégé Software：https://protege.stanford.edu/software/。用途：Desktop/Web；reasoners/協作/格式。

- [S15] Desktop license：https://github.com/protegeproject/protege/blob/master/license.txt。用途：BSD 2-Clause。

- [S16] WebProtégé license：https://github.com/protegeproject/webprotege/blob/master/license.txt。用途：BSD 2-Clause。

- [S17] Cellfie：https://github.com/protegeproject/cellfie-plugin。用途：Excel→OWL與規則。

- [S18] OntoGraf：https://github.com/protegeproject/ontograf。用途：OWL關係圖；附於Desktop。

- [S19] OntoGPT：https://github.com/monarch-initiative/ontogpt。用途：LLM抽取、SPIRES、Ollama；第三方。

- [S20] OWL 2 Primer：https://www.w3.org/TR/owl2-primer/。用途：OWL語意、開放世界、非schema必填檢查。

- [S21] SHACL：https://www.w3.org/TR/shacl/。用途：RDF資料限制與驗證。

- [S22] Ontology Development 101：https://protege.stanford.edu/publications/ontology_development/ontology101-noy-mcguinness.html。用途：七步/competency questions；Noy與McGuinness。

- [S23] OWLViz：https://github.com/protegeproject/owlviz。用途：class階層圖。

- [S24] SWRLTab：https://protegewiki.stanford.edu/wiki/SWRLTab。用途：SWRL/SQWRL；舊wiki授權未列。

- [S25] OntoGPT license：https://github.com/monarch-initiative/ontogpt/blob/main/LICENSE。用途：BSD 3-Clause。

- [S26a] Business_Capability：https://metamodel.enterprise-architecture.org/EA_Class/Business_Layer/Business_Conceptual/Business_Capability.html。用途：Essential 6.20 class定義。

- [S26b] Business_Process：https://metamodel.enterprise-architecture.org/EA_Class/Business_Layer/Business_Logical/Business_Process_Type/Business_Process.html。用途：Essential 6.20 class定義。

- [S26c] Application_Provider：https://metamodel.enterprise-architecture.org/EA_Class/Application_Layer/Application_Logical/Application_Provider_Type/Application_Provider.html。用途：Essential 6.20 class定義。

- [S26d] Information_Concept：https://metamodel.enterprise-architecture.org/EA_Class/Information_Layer/Information_Conceptual/Information_Concept.html。用途：Essential 6.20 class定義。

- [I1] v9 v0.8 records + TTL。查證：完整下載358筆及TTL；未跑parser/reasoner。
  - https://drive.google.com/file/d/1DBiPZousix3ZgumOjpg6qOgopkYJOPlb/view?usp=drivesdk&authuser=braincat%40gmail.com
  - https://drive.google.com/file/d/1Pts9RS-whqhBC1bW3njhvsJWApBeBk58/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I2] catalog v0.2。查證：完整MD/JSON下載；693項，現用v0.8。
  - https://drive.google.com/file/d/186COGGYMGNaUrbBZWOpsoTazBi1BNvnz/view?usp=drivesdk&authuser=braincat%40gmail.com
  - https://drive.google.com/file/d/1ppGPqibsiO_Dls0sX4Ll9goC7vhMlp0K/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I3] 13條件溯源。查證：完整JSON讀取；整體組合13筆未解，未轉述條件內容。
  - https://drive.google.com/file/d/1icLqveAEjLrxw7-SN9zJZRE4sEL5PVTU/view?usp=drivesdk&authuser=braincat%40gmail.com
  - https://drive.google.com/file/d/1S7cy9jNOSoaaAwIspFcZtsdAeOKrNkkJ/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I4] TOGAF v4 README。查證：完整README；未重新驗證1753筆全文。
  - https://drive.google.com/file/d/1eGUSkZBAVxOhlDN7S_CdTJj32AqI7YcG/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I5] 六璧合一API原型。查證：完整程式碼讀取；固定回傳，未執行。
  - https://drive.google.com/file/d/1py7xeQBkJWF9HHRLpiZAdQJdPScMo0e0/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I6] CoS決策／議題／pipeline。查證：完整JSON；映射素材，不把舊狀態當現況。
  - https://drive.google.com/file/d/1ShT-f_vwUvMT6JCVnGs0iNPJDWdJMgOy/view?usp=drivesdk&authuser=braincat%40gmail.com
  - https://drive.google.com/file/d/1h5bDL5Z_Lnl-S1K5Fxv9rNpRhd7Ep7Bz/view?usp=drivesdk&authuser=braincat%40gmail.com
  - https://drive.google.com/file/d/1mKSICl0mcjQM8ZZdfEzaIpiThaUExbzR/view?usp=drivesdk&authuser=braincat%40gmail.com

- [I7] BMC v1。查證：完整Doc文字。
  - https://docs.google.com/document/d/1IE0nQ9eMTqmhRQTHKTgzd9nDGwFBElExXCTtKxU3XHg/edit?usp=drivesdk&authuser=braincat%40gmail.com

- [I8] 基線與部署狀態。查證：內部工作紀錄v0.9.1與Drive catalog v0.8不同；私有GitHub本輪未能查證。

- [I9] 準備度模板包。查證：完整發佈修訂讀取，瀏覽器視覺檢視首屏及全文；全部為虛構案例。
  - https://files.instinct.com/file-01M3PH1F5E33QM5MYH6F869086
