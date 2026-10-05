# Essential × Protégé 研究 v1.0（第3部分／共3部分）

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

例子只用公開銳電3C。CoS案件狀態只作欄位素材，不重新宣稱現況。這是新研究v1.0，不代表已融合、已部署或已批准上架。

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

- [I2] catalog v0.2。查證：完整MD/JSON下載；693項，現用v0.8。

- [I3] 13條件溯源。查證：完整JSON讀取；整體組合13筆未解，未轉述條件內容。

- [I4] TOGAF v4 README。查證：完整README；未重新驗證1753筆全文。

- [I5] 六璧合一API原型。查證：完整程式碼讀取；固定回傳，未執行。

- [I6] CoS決策／議題／pipeline。查證：完整JSON；映射素材，不把舊狀態當現況。

- [I7] BMC v1。查證：完整Doc文字。

- [I8] 基線與部署狀態。查證：內部工作紀錄v0.9.1與Drive catalog v0.8不同；私有GitHub本輪未能查證。

- [I9] 準備度模板包。查證：完整發佈修訂讀取，瀏覽器視覺檢視首屏及全文；全部為虛構案例。
