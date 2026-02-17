# University Ranking & Admission Requirement Crawler

*(Learning Project -- Non-Official API Usage)*

------------------------------------------------------------------------

## ⚠️ Disclaimer

This project is developed for **learning and academic exploration
purposes only**.

It uses publicly accessible ranking pages from QS and attempts to
extract ranking and admission-related information.\
It is **not affiliated with QS** and does not guarantee:

-   Data completeness\
-   Data accuracy\
-   Long-term API stability\
-   Continuous availability

QS may change its internal API or page structure at any time, which can
cause this project to stop functioning.

------------------------------------------------------------------------

# Project Overview

This is a modular Python crawler that:

-   Retrieves QS ranking data
-   Optionally fetches university detail pages
-   Extracts selected academic metrics
-   Outputs results to console or file formats

The project focuses on:

-   Modular architecture design
-   Network handling and retry mechanisms
-   Async vs Sync performance comparison
-   Error handling in unstable external APIs

------------------------------------------------------------------------

# Current Architecture

    clawer/
    ├── clawer_main.py         # Entry point
    ├── constants/             # Static preset data
    ├── ui/                    # CLI and interactive menu
    ├── utils/                 # Logging, retry, cache, helpers
    ├── crawler.py             # Main orchestration controller
    ├── fetcher.py             # HTTP layer (requests + aiohttp)
    ├── extractor.py           # Parsing logic
    ├── exporter.py            # Output layer
    ├── config.py              # Central configuration
    └── models.py              # Data structures

------------------------------------------------------------------------

## Supported Features (Current State)

  -----------------------------------------------------------------------
  Feature                     Status                Notes
  --------------------------- --------------------- ---------------------
  World Ranking               Generally works       Depends on API
                                                    stability

  Subject Ranking             Partially stable      Some subjects may
                                                    return errors

  National Ranking            Works with delay      Large countries may
                                                    cause timeouts

  Async Mode                  Experimental          May trigger rate
                                                    limit

  File Export                 Basic support         CSV/Excel/JSON
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Known Limitations

1.  QS internal API may return 404 or HTML instead of JSON.
2.  Some subject rankings fail intermittently.
3.  Async mode can cause timeout or rate limiting.
4.  Admission requirement extraction is heuristic-based.
5.  No persistent database (in-memory processing only).
6.  No guarantee of long-term compatibility.

------------------------------------------------------------------------

# Installation

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

# Usage

## Interactive Mode

``` bash
python3 clawer_main.py
```

## CLI Mode

``` bash
python3 clawer_main.py --country us
python3 clawer_main.py --country uk --limit 20
python3 clawer_main.py --format csv --output output.csv
```

------------------------------------------------------------------------

# Educational Purpose

This repository is maintained as a learning and experimentation project.

Functionality may break if: - QS changes internal APIs - Ranking
structure changes - Network policies change

Use at your own discretion.
