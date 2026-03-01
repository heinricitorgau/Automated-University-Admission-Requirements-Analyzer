# University Ranking Crawler

> Personal learning project. Not affiliated with THE or any ranking organization.

---

## Performance Notes 

1. Async crawling is enabled by default; installing `aiohttp` is recommended.
2. Tune `max_concurrent_requests` (default: 200) and `request_delay` (default: 0.01) in `config.py`.
3. You can force async mode with `--async`.

---

## Architecture 

| File | Role |
|---|---|
| `clawer_main.py` | Entry point / CLI |
| `crawler.py` | Orchestration & flow control |
| `fetcher.py` | HTTP requests, SSL, retry |
| `extractor.py` | HTML/JSON parsing |
| `exporter.py` | Console / CSV / Excel / JSON output |
| `config.py` | Centralized runtime config |

---

## Development Timeline 

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
| 2026-02-28 | Async speed optimizations (500 items/page, DNS caching, max 200 concurrency) |

---

## Stability Snapshot 

| Feature | Status |
|---|---|
| World Ranking | High |
| Subject Ranking | Medium |
| National Ranking | Medium |
| Async mode | High |
