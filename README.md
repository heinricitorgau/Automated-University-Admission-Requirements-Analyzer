# Automated-University-Admission-Requirements-Analyzer

## Project Status

This project is currently under active development.
The repository serves as both code workspace and development record.

## Project Description

This is a personal learning project focused on:

- Understanding ranking website data structures
- Practicing modular Python architecture
- Experimenting with synchronous and asynchronous HTTP requests
- Handling unstable external APIs
- Building robust parsing and formatted output pipelines

This project is for learning and research purposes only.
It is not affiliated with QS or any ranking organization.

## Performance Notes

1. Async crawling is enabled by default; installing `aiohttp` is recommended.
2. You can tune `max_concurrent_requests` (default: 32) and `request_delay` (default: 0.01) in `config.py`.
3. If you hit blocks or HTTP 429, increase `request_delay` or reduce concurrency.
4. Under stable network/server conditions, async mode is significantly faster than sync mode.
5. You can force async mode with `--async`.

## Current Scope

The project is modularized into:

- Entry script (`clawer_main.py`)
- Controller (`crawler.py`)
- Network layer (`fetcher.py`)
- Parsing layer (`extractor.py`)
- Output layer (`exporter.py`)
- Configuration module (`config.py`)
- Data models (`models.py`)

## Known Issues

- API may occasionally return 404 or HTML instead of JSON
- Some Subject Ranking datasets remain inconsistent
- Async mode may hit timeout in heavy scenarios
- SSL verification may fail in some macOS virtual environments
- API parameter changes can break compatibility

## Learning Objectives

- Python project structuring
- Retry and error-handling patterns
- Asynchronous programming with `aiohttp`
- Layered design and separation of concerns

## Future Plans (Tentative)

- Continue modular refactoring
- Improve stability and fallback logic
- Enhance logging and diagnostics
- Improve CLI and interaction flow

---

## 中文說明

### 專案狀態

本專案持續開發中，README 同時用於說明與記錄開發歷程。

### 專案目標

- 理解排名網站資料結構
- 練習 Python 模組化設計
- 實作同步/非同步請求流程
- 提升不穩定 API 的容錯能力
- 建立可維護的解析與輸出流程

### 已知挑戰

- API 偶發 404 或回傳 HTML
- Subject Ranking 部分資料不一致
- 大資料量下 Async 可能 timeout
- macOS venv 可能出現 SSL 憑證問題
- 參數變動可能造成 API 相容性問題

### 後續方向

- 持續優化重試、fallback 與穩定性
- 持續整理 CLI 體驗與錯誤訊息
- 強化可維護性與型別安全

---

## 開發日誌（併入自 `爬蟲日誌_v2.md`）

# University Ranking Crawler 開發日誌（v2）

本文件整理 TopUniversities Web Crawler 專案的開發歷程、架構演進與當前系統狀態。

---

## 1. 系統架構概覽（v2.0）

專案於 **2026-02-17** 完成模組化重構，採分層架構以提升可維護性與可測試性。

### 目錄結構

```text
clawer/
├── clawer_main.py         # 程式入口（Entry Point）
├── constants/             # 常量定義（Data Layer）
│   ├── presets.py         # 排名 ID 與 URL 預設值
│   ├── countries.py       # 國家代碼與名稱對照
│   └── regions.py         # 地區分組定義
├── ui/                    # 使用者介面（Presentation Layer）
│   ├── cli.py             # 命令列參數解析
│   ├── interactive.py     # 互動選單邏輯
│   └── validators.py      # 輸入驗證與處理
├── utils/                 # 通用工具（Utility Layer）
│   ├── logging.py         # 日誌設定
│   ├── retry.py           # 重試機制裝飾器
│   ├── formatters.py      # 資料格式化函式
│   └── cache.py           # 簡易快取
├── crawler.py             # 核心控制器（Controller）
├── fetcher.py             # 網路傳輸（Network Layer）
├── extractor.py           # 資料解析（Parsing Layer）
├── exporter.py            # 資料輸出（Output Layer）
├── config.py              # 設定管理（Configuration）
└── models.py              # 資料模型（Model）
```

### 核心模組職責

- `clawer_main.py`：判斷並啟動 CLI 或互動模式。
- `crawler.py`：流程協調（Orchestrator），統籌下載、解析與輸出。
- `fetcher.py`：負責 HTTP 請求、Headers/Cookies、SSL 驗證與重試。
- `extractor.py`：自 HTML / JSON 提取結構化資料。
- `exporter.py`：支援 Console、CSV、Excel、JSON 輸出。
- `config.py`：集中管理系統與執行設定。

---

## 2. 開發日誌（Development Diary）

### 2026-02-04｜Admission Requirements Crawler 初版

- 完成 US CS Master 入學門檻爬蟲初版。
- 鎖定 Master 區段，排除 Bachelor 與 Location。
- 以 Regex 擷取 GMAT、GRE、GPA、IELTS、TOEFL；缺值統一填 `N/A`。

---

### 2026-02-05｜環境除錯與升級盤點

- 釐清 `crawler`、`config`、`utils` 模組載入失敗（與 Python 執行路徑相關）。
- 在 `requirements.txt` 補齊 `beautifulsoup4` 與 `lxml`。
- 盤點舊版 `clawer1_updated.py` 的重構計畫，確立 v2.0 模組化方向。

---

### 2026-02-11 ～ 2026-02-13｜排名邏輯與國家屬性擴充

- **2026-02-11**：在 Overall Ranking 新增 Country 欄位，並同步更新各輸出格式與 Console UI。
- **2026-02-12**：調整預設行為：未指定國家時預設 World Top 100；指定國家則進入 National Ranking。
- **2026-02-13**：重構 ranking 邏輯（Overall Ranking 改為 optional mode），減少不必要 API 呼叫。

---

### 2026-02-14｜Code Cleanup 與 UI Refinements

- 優化 Console 表格對齊與 QS 指標欄位顯示，空欄自動隱藏。
- 修正 Subject Ranking 分頁終止條件與 timeout 處理，並暫停該模式的 Async。

---

### 2026-02-15｜錯誤處理與穩定性修正

- 修復 Brotli 解碼問題。
- 實作 API Retry 機制與 SSL 驗證修正。
- 針對 QS API 偶發 404 增加例外處理。

---

### 2026-02-17｜模組化重構里程碑

- 完成 v2.0 結構重整。
- 建立 `ui`、`constants`、`utils` 子目錄。
- 將核心邏輯自 `clawer_main.py` 拆出，入口檔瘦身並確認無 regression。

---

### 2026-02-19｜Performance Boost

- 預設啟用 Async 模式，提升並發抓取能力並降低 request 延遲。

---

### 2026-02-21｜本輪整合：QS Region / Sustainability 對齊修復與流程收斂

- 完成 Region / Sustainability 模式對齊。
- 修正 QS API 404 fallback、分頁跨頁收集與過濾邏輯。
- 收斂主表 5 指標欄位策略與 secondary metric 規則。
- 強化型別安全與靜態檢查修補。
- 驗證 World / Subject / Region / Sustainability 模式穩定運行。
