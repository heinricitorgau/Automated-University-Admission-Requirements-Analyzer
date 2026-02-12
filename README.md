# Automated University Admission Requirements Analyzer

An ongoing personal project.

This repository represents a work-in-progress system under active development.
Details regarding design, methodology, and implementation are intentionally withheld at this stage.

Limited testing is currently conducted in a private setting.
Further disclosure will be made after the project reaches completion.
flowchart TB
  %% ============ User / CLI ============
  U[使用者\n(互動式 CLI)] --> CLI[clawer1_updated_patched.py\n選榜單/科目/地區/限制/排序/Next Steps]

  %% ============ Config ============
  CLI --> CFG[Config\n(config.py)\n- ranking_id / ranking_page_url\n- region_name / country\n- limit / sort / async\n- timeout / headers / params]

  %% ============ Orchestration ============
  CFG --> RUN[run_crawler()\n(crawler.py)\n初始化核心元件與流程]
  RUN --> CR[UniversityCrawler\n(crawler.py)\n同步/非同步爬取控制]

  %% ============ Fetch Layer ============
  CR -->|Sync| F1[UniversityFetcher\n(fetcher.py)\nrequests]
  CR -->|Async| F2[AsyncUniversityFetcher\n(fetcher.py)\naiohttp + SSL(certifi)]

  %% ranking list
  F1 --> RID[Resolve Ranking ID\n(從 ranking_page_url 解析 nid)]
  F2 --> RID
  RID --> API[QS Ranking API\n/rankings/api/ranking/{nid}\n取得 score_nodes]

  %% ============ Data Processing ============
  API --> NODES[score_nodes\n(排名清單節點)]
  NODES --> FILT[Filter & Normalize\n(crawler.py)\n- limit\n- sort direction\n- (optional) region/country filter]
  FILT --> MAP[Node → University\n(models.py)\n統一欄位 rank/name/path/country]

  %% details fetch
  MAP --> PATHS[paths 清單]
  PATHS -->|Sync| F1
  PATHS -->|Async batch| F2
  F1 --> HTMLS[University Detail HTML]
  F2 --> HTMLS

  %% extractor
  HTMLS --> EXT[Extractor\n(extractor.py)\n解析 admission requirements\n(GRE/GMAT/GPA/IELTS/TOEFL/DET...)]
  EXT --> UNI[Universities List\n(models.py)\nUniversity + requirements]

  %% ============ Export Layer ============
  UNI --> EXP[Exporter\n(exporter.py)\nConsole / CSV / JSON / Markdown\n(表格、排序、secondary metric)]
  EXP --> OUT[輸出結果\n檔案或終端機表格]

  %% ============ Utilities ============
  subgraph UTILS[utils.py (共用工具)]
    RETRY[retry/backoff]
    CACHE[cache (TTL/避免重抓)]
    LOG[logging helpers]
  end

  UTILS -.-> F1
  UTILS -.-> F2
  UTILS -.-> CR
