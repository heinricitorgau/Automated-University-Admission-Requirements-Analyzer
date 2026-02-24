# University Ranking Crawler

## Project Description / 專案說明

### English

#### Project Status

This project is under active development.
This repository serves as both a code workspace and a development record.

#### What This Project Does

This is a personal learning project focused on:

- Understanding ranking website data structures
- Practicing modular Python architecture
- Experimenting with synchronous and asynchronous HTTP requests
- Handling unstable external APIs
- Building reliable parsing and formatted output pipelines

This project is for learning and research only.
It is not affiliated with QS or any ranking organization.

#### Performance Notes

1. Async crawling is enabled by default; installing `aiohttp` is recommended.
2. Tune `max_concurrent_requests` (default: 32) and `request_delay` (default: 0.01) in `config.py`.
3. If you hit blocks or HTTP 429, increase delay or reduce concurrency.
4. Under stable conditions, async mode is usually much faster than sync mode.
5. You can force async mode with `--async`.

#### Current Scope

- Entry script (`clawer_main.py`)
- Controller (`crawler.py`)
- Network layer (`fetcher.py`)
- Parsing layer (`extractor.py`)
- Output layer (`exporter.py`)
- Configuration module (`config.py`)
- Data models (`models.py`)

#### Known Issues

- API may occasionally return 404 or HTML instead of JSON
- Some Subject Ranking datasets can be inconsistent
- Async mode may timeout on heavy workloads
- SSL verification may fail in some macOS virtual environments
- API parameter changes may break compatibility

#### Future Plans

- Continue modular refactoring
- Improve stability and fallback logic
- Enhance logging and diagnostics
- Improve CLI and interaction flow

### 中文

#### 專案狀態

本專案持續開發中，README 同時作為程式說明與開發紀錄。

#### 專案內容

這是一個個人學習專案，重點在於：

- 理解排名網站的資料結構
- 練習 Python 模組化架構
- 實作同步與非同步 HTTP 請求
- 提升對不穩定外部 API 的容錯能力
- 建立穩定的資料解析與格式化輸出流程

本專案僅供學習與研究用途，
與 QS 或其他排名機構無關。

#### 效能說明

1. 預設啟用 Async 抓取，建議安裝 `aiohttp`。
2. 可在 `config.py` 調整 `max_concurrent_requests`（預設 32）與 `request_delay`（預設 0.01）。
3. 若遇到封鎖或 HTTP 429，請提高 delay 或降低並發。
4. 在網路穩定條件下，Async 通常明顯快於同步模式。
5. 可使用 `--async` 強制啟用 Async 模式。

#### 目前範圍

- 主程式入口（`clawer_main.py`）
- 流程控制（`crawler.py`）
- 網路請求層（`fetcher.py`）
- 資料解析層（`extractor.py`）
- 輸出層（`exporter.py`）
- 設定模組（`config.py`）
- 資料模型（`models.py`）

#### 已知挑戰

- API 偶發回傳 404 或 HTML
- Subject Ranking 部分資料可能不一致
- 大量資料時 Async 可能 timeout
- 部分 macOS venv 可能遇到 SSL 驗證問題
- API 參數變動可能造成相容性中斷

#### 後續方向

- 持續推進模組化重構
- 強化穩定性與 fallback 策略
- 改善日誌與診斷資訊
- 優化 CLI 與互動流程

---

## Development Notes / 開發說明

### English

#### Architecture Milestone (v2.0)

The project completed a modular refactor on **2026-02-17** with a layered structure:

- `clawer_main.py`: entry point (CLI/interactive mode)
- `crawler.py`: orchestration and flow control
- `fetcher.py`: HTTP requests, SSL, retry behavior
- `extractor.py`: structured data extraction from HTML/JSON
- `exporter.py`: console/CSV/Excel/JSON outputs
- `config.py`: centralized runtime configuration

#### Development Timeline

- **2026-02-04**: Initial Admission Requirements crawler for US CS Master pages
- **2026-02-05**: Environment/module path fixes; added `beautifulsoup4` and `lxml`
- **2026-02-11 ~ 2026-02-13**: Ranking logic and country field expansion
- **2026-02-14**: Console/UI cleanup and Subject timeout handling
- **2026-02-15**: Brotli/SSL/retry stability fixes
- **2026-02-17**: Major modularization milestone (v2.0)
- **2026-02-19**: Async-by-default performance update
- **2026-02-21**: Region/Sustainability alignment, paging/filtering fixes, type-safety improvements
- **2026-02-24**: Added 6 new engineering/data-science subject rankings (Chemical Engineering, Civil & Structural, Data Science & AI, Electrical & Electronic, Mechanical/Aeronautical/Manufacturing, Mineral & Mining); reordered subject list by category (Arts & Humanities → Engineering & Technology → Life Sciences & Medicine → Natural Sciences); added 4 new regional rankings (Asia, Europe, Latin America & The Caribbean, Sub-Saharan Africa 2026); reordered region menu to match QS official order with subregions grouped under parent region

#### Current Stability Snapshot

- World Ranking: High
- Subject Ranking: Medium
- National Ranking: Medium
- Async mode: Medium to Low (requires concurrency tuning)

### 中文

#### 架構里程碑（v2.0）

專案於 **2026-02-17** 完成模組化重構，採分層設計：

- `clawer_main.py`：入口（CLI/互動模式）
- `crawler.py`：流程協調與控制
- `fetcher.py`：HTTP 請求、SSL、重試機制
- `extractor.py`：HTML/JSON 結構化解析
- `exporter.py`：Console/CSV/Excel/JSON 輸出
- `config.py`：集中化執行設定

#### 開發時程

- **2026-02-04**：完成 US CS Master 入學門檻爬蟲初版
- **2026-02-05**：修正環境與模組路徑問題；補齊 `beautifulsoup4`、`lxml`
- **2026-02-11 ~ 2026-02-13**：擴充排名邏輯與 Country 欄位
- **2026-02-14**：整理 Console/UI；修正 Subject timeout 相關問題
- **2026-02-15**：修復 Brotli、SSL 與重試穩定性問題
- **2026-02-17**：完成 v2.0 模組化重構里程碑
- **2026-02-19**：改為預設 Async，提升抓取效能
- **2026-02-21**：完成 Region/Sustainability 對齊，修補分頁/過濾與型別安全問題
- **2026-02-24**：新增 6 個工程/資料科學 Subject Ranking 選項（Chemical Engineering、Civil & Structural、Data Science & AI、Electrical & Electronic、Mechanical/Aeronautical/Manufacturing、Mineral & Mining）；依分類重排 Subject 清單（Arts & Humanities → Engineering & Technology → Life Sciences & Medicine → Natural Sciences）；新增 4 個 Region Ranking 選項（Asia、Europe、Latin America & The Caribbean、Sub-Saharan Africa 2026）；依 QS 官網順序重排地區選單並將子區域歸組至對應主區域下

#### 目前穩定度概況

- World Ranking：高
- Subject Ranking：中
- National Ranking：中
- Async 模式：中低（需搭配並發參數調校）

---

## Source Note / 來源註記

This README integrates the previous development log content from `爬蟲日誌_v2.md`.
本 README 已整合 `爬蟲日誌_v2.md` 的開發紀錄重點。
