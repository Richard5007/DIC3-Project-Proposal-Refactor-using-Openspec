# AirGuard AI 提案深度解析報告 (NotebookLM 規範審查版)
**審核基準文件**：
1. `doc/A2Z outline example.pdf` (2020 A-Z SOP 全文結構規範)
2. `doc/期末專題提案作業規範.pdf` (AI Agent + Domain Knowledge + Data Analytics + Real-World Application)
3. 課堂更新要求（Perplexity 最新實證強化 A–F + 300 字重點摘要 + IEEE Transactions Systems 期刊摘要 + OpenSpec SDD 規範轉換）

---

## 一、 摘要 (Abstract) A–F、300 字精華與 IEEE 期刊摘要審查

| 規範區塊 | 對應代號與定義 | AirGuard AI 落實內容與審查結論 | 評核狀態 |
|---|---|---|---|
| **IEEE** | **IEEE Transactions Systems Abstract** | 以 IEEE Transactions on Systems, Man, and Cybernetics: Systems 期刊格式撰寫 `Title—`、`Abstract—` 與 `Index Terms—`，嚴謹收斂背景、缺口、解耦架構與 60 題評估設計。 | **符合規範**<br>(期刊格式對齊) |
| **A** | **Attention Getter**<br>(動機及最新實證引題) | 引用 *State of Global Air 2025*（全球 790 萬人死亡、86% 為非傳染性疾病）、WHO 2025 `B09461`（99% 人口超標），以及台灣環境部 **2025 年 1 月 1 日生效之加嚴標準**（$\text{PM}_{2.5}$ 降至 $12\ \mu\text{g/m}^3$、「站站達標」、午後光化臭氧 $\text{O}_3$ 橘色提醒案例）。 | **符合規範**<br>(2025 權威實證) |
| **B** | **But**<br>(挑戰與痛點) | 條列三大痛點：(1) `AQX_P_488` 實測稽核 970,296 列含 364,146 重複列、哨兵值、4 筆遺失編號及 13 組 (26 筆) 互斥衝突鍵；(2) *TableBench* / *RAGTruth* (2024–2025) 證實 LLM 表格數值忠實度幻覺；(3) *Neuro-Air* (2026) 無法直接適配台灣法定最大副指標算則與列級強制溯源。 | **符合規範**<br>(痛點具象可核) |
| **C** | **Cure**<br>(解藥提案) | 提出 **AirGuard AI** —— 確定性證據型領域智慧代理人，嚴格落實「LLM 負責意圖解析與語意組織，確定性工具負責檢索與計算，法定規則與護欄負責邊界檢查」。 | **符合規範**<br>(定位清晰明確) |
| **D** | **Development**<br>(方法架構與 OpenSpec) | 將 `DESIGN.md` 轉換為 `openspec/specs/` 四大規範契約，整合 Planner、`(SiteId, DataCreationDate)` 複合鍵檢索（606,137 筆）、75% 日覆蓋門檻、Python 確定性引擎、最大副指標規則與列級證據／邊界護欄。 | **符合規範**<br>(SDD 規範完備) |
| **E** | **Experiments**<br>(評估規劃) | 建置 `AirGuard-Eval-60` 固定 60 題基準集（45 題可回答 + 15 題缺值/衝突/因果/醫療邊界），對照 LLM-only、Deterministic Tools Only、AirGuard AI 三組條件。 | **符合規範**<br>(對照設計嚴謹) |
| **F** | **Findings**<br>(預期產出與學術價值) | 嚴守「未實驗者僅列 Expected Outcomes」原則，標明目標數值正確率 >90%、列級回溯 100%、無來源幻覺率 0.0%、拒答精準率 >90%，並條列四大預期學術貢獻與 A–F 強化自評。 | **符合規範**<br>(杜絕數據虛構) |
| **300字** | **300 字精華摘要** | 濃縮 A–F 關鍵脈絡（SoGA 2025、MOENV 2025 $12\ \mu\text{g/m}^3$ 新制、606k 治理庫、解耦架構與 60 題評估規劃）成一段約 330 字精煉摘要，便於提案書與系統註冊使用。 | **符合規範**<br>(精煉高密度) |

---

## 二、 緒論 (Introduction) G–L 論證結構審查

- **G (General - 現況背景)**：涵蓋 WHO 2021/2025 指引、*State of Global Air 2025* 數據、台灣 2025 年元旦起施行之加嚴空品標準與 `AQX_P_488` 全台 88 站逐時資料架構。
- **H (However - 四大核心障礙)**：深度剖析開放資料處理高門檻、9 月份 13 組原生衝突紀錄、LLM 表格算術漂移幻覺，以及「測站讀值誤當個人暴露／下風處濃度誤推工廠因果」之領域誤用風險。
- **I (In Literature - 文獻分類)**：分為官方靜態儀表板、機器學習預測與低成本感測校正（Lee 2020, Tzeng 2023, Dong 2025, Fang 2025, Lekamge 2025）、以及 LLM 異常偵測與多代理決策系統（Lee 2025, Yenkikar 2025, Neuro-Air 2026）。
- **J (Judgement - SWOT 與 Research Gap)**：精確收斂出「缺乏以台灣 `AQX_P_488` 資料品質條件與法定最大副指標為約束、嚴格解耦計算與強制列級溯源之領域代理人與基準集」之研究缺口。
- **K (Keypoint - 設計精神與四大貢獻)**：提煉「語言歸語言、計算歸確定性、結論歸證據」，條列資料治理、OpenSpec 解耦架構、列級護欄與 60 題基準四大貢獻。
- **L (List Organization - 章節導覽)**：清楚引導至相關研究、系統設計、實驗規劃、結論與 18 筆經查核參考文獻。

---

## 三、 相關研究 (Related Work) 與 Deep Research 深度調研審查

### 1. 文獻平衡性審查 (1/2 AI 技術 + 1/2 領域知識)
- **AI 與資料分析面向 (4 篇)**：`[1]` Ma et al. (2026, *npj Clean Air*), `[2]` Lee et al. (2025, *IEEE Access*), `[3]` Yenkikar et al. (2025, *MethodsX*), `[4]` Lee et al. (2020, *Sci. Rep.*)。
- **空品量測與領域規範面向 (4 篇)**：`[5]` Tzeng et al. (2023, *Biometrics*), `[6]` Dong et al. (2025, *STOTEN*), `[7]` Fang et al. (2025, *STOTEN*), `[8]` Lekamge & Oswin (2025, *npj Clim. Atmos. Sci.*)。
- **4x5 綜合比較表**：完整涵蓋研究問題、AI 方法、領域核心概念、資料集規模、核心發現與對本專題之限制差距。

### 2. Deep Research 三大核心問題審查
- **Q1. 5 個核心思維模式**：(1) 多污染物最大副指標原則；(2) 測站空間代表性 vs. 個人暴露解耦；(3) 感測器階級與資料品質分層；(4) 時間尺度對齊與滑動平均規範；(5) 時空相關性與因果歸咎防線。
- **Q2. 3 個重大專業爭論與取捨**：(1) 低成本微感測網路 vs. 國家參考測站；(2) 自主寫碼端到端代理 vs. 確定性工具解耦；(3) 高度個人化風險評估 vs. 通用公衛防護基線。
- **Q3. 10 個深度理解問題**：覆蓋 Why、What-if、Trade-off、Failure Case、Evidence Grounding、Comparison、Design Decision、Real-world Scenario、Domain Rule 與 Evaluation Metric。

---

## 四、 系統架構與 OpenSpec SDD 落地審查 (PA–PM)

- **OpenSpec 規範轉換 (`openspec validate --all --strict`)**：
  - 已將 `DESIGN.md` 轉換為 `openspec/specs/` 下四個標準能力目錄：`data-pipeline/spec.md`、`agent-architecture/spec.md`、`domain-rules/spec.md`、`evaluation-benchmark/spec.md`。
  - 已將 `openspec/changes/proposal-refactor/design.md` 補全為九階段工作流、技術決策表、風險緩解與驗證流程，並通過 `openspec validate --all --strict` 5/5 項目零錯誤驗證。
- **PA–PM 完整性**：`PE. Paper Elements` 已與 `DESIGN.md` 九階段處理流程完全對齊，涵蓋 Mermaid 架構圖、操作判斷流程圖、數學公式（副指標線性內插、最大副指標、75% 日覆蓋率、證據忠實度）與 39 行帶行號演算法虛擬碼。

---

## 五、 綜合審查結論
AirGuard AI 更新後之專題提案完全符合《2020 A-Z SOP》、《期末專題提案作業規範》以及課堂新增之 Perplexity 實證強化、300 字摘要與 IEEE Transactions Systems 期刊格式要求，且所有引用文獻均經查核確認，OpenSpec 規格可透過 CLI 嚴格驗證。
