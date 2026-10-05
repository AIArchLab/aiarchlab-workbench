# Essential × Protégé：AIArchLab 的知識與提案骨架

> 本文共3部分，此為第1部分。

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
