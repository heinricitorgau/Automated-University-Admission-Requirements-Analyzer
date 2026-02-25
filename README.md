# University Ranking Crawler

> 個人學習專案，僅供研究用途，與 QS 或其他排名機構無關。
> Personal learning project. Not affiliated with QS or any ranking organization.

---

## Performance Notes / 效能說明

1. Async crawling is enabled by default; installing `aiohttp` is recommended.
2. Tune `max_concurrent_requests` (default: 32) and `request_delay` (default: 0.01) in `config.py`.
3. If you hit blocks or HTTP 429, increase delay or reduce concurrency.
4. You can force async mode with `--async`.

---

1. 預設啟用 Async 抓取，建議安裝 `aiohttp`。
2. 可在 `config.py` 調整 `max_concurrent_requests`（預設 32）與 `request_delay`（預設 0.01）。
3. 若遇到封鎖或 HTTP 429，請提高 delay 或降低並發。
4. 可使用 `--async` 強制啟用 Async 模式。

---

## Architecture / 架構

| File | Role |
|---|---|
| `clawer_main.py` | Entry point / CLI |
| `crawler.py` | Orchestration & flow control |
| `fetcher.py` | HTTP requests, SSL, retry |
| `extractor.py` | HTML/JSON parsing |
| `exporter.py` | Console / CSV / Excel / JSON output |
| `config.py` | Centralized runtime config |

---

## Development Timeline / 開發時程

| Date | Changes |
|---|---|
| 2026-02-04 | Initial crawler |
| 2026-02-05 | Path fixes; added `beautifulsoup4`, `lxml` |
| 2026-02-11~13 | Ranking logic & country field expansion |
| 2026-02-14 | Console/UI cleanup; Subject timeout fix |
| 2026-02-15 | Brotli / SSL / retry stability |
| 2026-02-17 | v2.0 modular refactor |
| 2026-02-19 | Async-by-default |
| 2026-02-21 | Region/Sustainability alignment; paging & type-safety fixes |
| 2026-02-24 | +6 subject rankings; +4 regional rankings; reordered menus |
| 2026-02-25 | Implemented QS-style table borders, shortened metric headers, and ASCII progress bar |

---

## Stability Snapshot / 穩定度

| Feature | Status |
|---|---|
| World Ranking | High / 高 |
| Subject Ranking | Medium / 中 |
| National Ranking | Medium / 中 |
| Async mode | Medium–Low / 中低 |
