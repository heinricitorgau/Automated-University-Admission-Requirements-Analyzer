# University Ranking Crawler - 開發與架構日誌

本文件紀錄 TopUniversities Web Crawler 專案的開發歷程、架構演進與系統狀態。

---

## 1. 系統架構簡介 (v2.0)

本專案於 2026/02/17 完成模組化重構，採用分層架構以提升可測試性與可維護性。

### 目錄結構

```text
clawer/
├── clawer_main.py         # 程式入口 (Entry Point)
├── constants/             # 常量定義 (Data Layer)
│   ├── presets.py         # 排名 ID 與 URL 預設值
│   ├── countries.py       # 國家代碼與名稱對照
│   └── regions.py         # 地區分組定義
├── ui/                    # 使用者介面 (Presentation Layer)
│   ├── cli.py             # 命令行參數解析
│   ├── interactive.py     # 交互式選單邏輯
│   └── validators.py      # 輸入驗證與處理
├── utils/                 # 通用工具 (Utility Layer)
│   ├── logging.py         # 日誌設定
│   ├── retry.py           # 重試機制裝飾器
│   ├── formatters.py      # 數據格式化函數
│   └── cache.py           # 簡單快取實作
├── crawler.py             # 核心控制器 (Controller)
├── fetcher.py             # 網路傳輸 (Network Layer)
├── extractor.py           # 資料解析 (Parsing Layer)
├── exporter.py            # 資料輸出 (Output Layer)
├── config.py              # 配置管理 (Configuration)
└── models.py              # 資料模型 (Model)
```

### 核心模組職責
* **clawer_main.py**: 負責判斷與啟動 CLI 或交互模式。
* **crawler.py**: 總指揮 (Orchestrator)。負責初始化設定，協調整體下載、解析與輸出流程。
* **fetcher.py**: 負責 HTTP 請求，處理 Headers、Cookies、SSL 驗證與錯誤重試。
* **extractor.py**: 從 HTML / JSON 格式中提取結構化資料。
* **exporter.py**: 支援 Console, CSV, Excel, JSON 多種輸出格式。
* **config.py**: 集中管理所有系統與運行設定。

> **歷史軌跡 (Legacy Notes):** 
> 早期單檔腳本架構 (`clawer1_updated_patched.py`) 與混合型工具檔 (`utils.py`) 皆已於 v2.0 模組化過程中拆分或棄用。

---

## 2. 開發日誌 (Development Diary)

### [2026-02-19] Performance Boost
* **核心更新**: 預設啟用 Async 模式，顯著提升並發抓取數量並降低 Request 延遲。

### [2026-02-17] 模組化重構里程碑
* **核心更新**: 完成專案結構重構 (v2.0)。
* **實作細節**: 
  - 建立 `ui`, `constants`, `utils` 子目錄。
  - 將核心邏輯從 `clawer_main.py` 抽離，成功瘦身入口檔案並驗證無 Regression 問題。

### [2026-02-15] 錯誤處理與穩定性修正
* **修正項目**:
  - 修復 Brotli 解碼問題。
  - 實作 API 呼叫的 Retry 機制與 SSL 驗證修正。
  - 針對 QS API 偶發的 404 進行例外排除。

### [2026-02-14] Code Cleanup & UI Refinements
* **UI 優化**: Console 表格顯示優化，對齊 QS 指標欄位並實作自動隱藏空欄位。
* **穩定性**: 修正 Subject Ranking 的分頁終止條件與 Timeout 處理，暫停該模式的 Async。

### [2026-02-11 ~ 13] 排名邏輯與國家屬性擴充
* **2/13**: 排名邏輯重構 (Overall Ranking 改為 Optional Mode)，減少不必要的 API 呼叫。
* **2/12**: 調整預設行為：未指定國家時預設為 World TOP 100；指定則進入 National Ranking 模式。
* **2/11**: 於 Overall Ranking 實作 Country (國家) 欄位，並同步更新各類匯出格式與 Console UI。

### [2026-02-05] 環境除錯與升級盤點
* **環境修復**: 釐清 `crawler`, `config`, `utils` 模組載入失敗問題（與 Python 執行路徑有關），並移除了對內建標準庫 `asyncio` 的誤依賴。
* **相依性更新**: 在 `requirements.txt` 中補齊 HTML 解析所需之 `beautifulsoup4` 與 `lxml`。
* **藍圖建立**: 盤點針對舊版 `clawer1_updated.py` 的重構計畫 (導向 v2.0 模組化架構)。

### [2026-02-04] Admission Requirements Crawler 初期實作
* **核心更新**: 完成初版 US Computer Science Master 入學門檻爬蟲。
* **實作細節**:
  - 鎖定 Master 資料區段，排除 Bachelor 與 Location 資訊。
  - 使用 Regex 擷取並驗證 GMAT、GRE、GPA、IELTS、TOEFL 等各類分數（無資訊預設帶入 `N/A`）。

---

## 3. 系統狀態與未來展望

### 系統穩定度評估 (v2.0)

| 運行模式 | 穩定度 | 評估備註 |
| :--- | :---: | :--- |
| **World Ranking** | 高 | API 狀態穩定，資料結構規律。 |
| **Subject Ranking** | 中 | 由於資料量與層級網頁特性，偶發 Timeout。 |
| **National Ranking** | 中 | 針對大國（如美國、英國）因資料龐大易遇瓶頸。 |
| **Async 模式** | 中低 | 極需良好控制並發數，否則易觸發伺服器阻擋。 |

### 未來升級方向 (Roadmap)

- [ ] **流量管控**: 引入 Semaphore 機制來精確控制 Async 模式下的並發數量。
- [ ] **穩定性提升**: 實作 Exponential Backoff (指數退避) 以優化失敗重試邏輯。
- [ ] **效能優化**: 加入 SQLite 進行本機端網頁快取，大幅降低重複 Request。
- [ ] **進階應用**: 探索並建立研究所錄取難度預測模型。

---

## 4. 專案開發對話紀錄索引 (AI Conversation Index)

以下為本專案保留之重要 ChatGPT/AI 對話紀錄，可做為後續接手開發與除錯之脈絡補充：

- **[2026-02-06] Display University Country**: 於主表與次順位表中加入大學所屬國家資訊。
- **[2026-02-05] Refactor Python Crawler Code**: 舊版爬蟲重構規劃與冗餘註解清理。
- **[2026-02-05] Analyzing Crawler Script & Requirements**: 解析套件相依性與環境隔離問題。
- **[2026-02-05] Updating Requirements File**: 補齊網頁解析 (`bs4`, `lxml`) 相關依賴。
- **[2026-02-05] Upgrading Web Crawler Script**: 架構重構前的效能優化藍圖探討。
- **[2026-02-05] Refining Admission Data Extraction**: 精煉各類考試分數 (GPA, TOEFL 等) 之正則解析邏輯。
- **[2026-02-04] Refining Admission Requirements Crawler**: 建立鎖定研究所 (Master) 層面之入學能力分數擷取機制。
