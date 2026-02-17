# University Admission Requirements Crawler

## Usage

### 1. Installation

```bash
pip install -r requirements.txt
```

### 2. Interactive Mode (Recommended)

Simply run the script without arguments to use the interactive menu:

```bash
python3 clawer_main.py
```

Follow the on-screen prompts to:
1. Select ranking type
2. Choose specific subjects
3. Filter by country or region
4. Set ranking limits

### 3. Command Line Interface (CLI)

Run with arguments for direct execution:

```bash
# Default: World Top 100 universities, console output
python3 clawer_main.py

# specific country (e.g., US, UK, TW)
python3 clawer_main.py --country us
python3 clawer_main.py --country uk --limit 20
python3 clawer_main.py --country tw

# Export to file (CSV, Excel, JSON)
python3 clawer_main.py --country ca --format excel --output canada_data.xlsx
python3 clawer_main.py --country au --format csv --output australia_data.csv

# Multi-country selection (CLI only supports single country code alias, use interactive for complex filters)
python3 clawer_main.py --country "us" --limit 10

# Show full help message
python3 clawer_main.py --help
```

## Supported Countries (Partial List)

| Code | Country | Code | Country |
|------|---------|------|---------|
| `us` | United States | `sg` | Singapore |
| `uk` | United Kingdom | `hk` | Hong Kong |
| `ca` | Canada | `cn` | China |
| `au` | Australia | `jp` | Japan |
| `de` | Germany | `tw` | Taiwan |
| `fr` | France | `kr` | South Korea |

*Use interactive mode to see the full list of available countries.*

---

# 大學入學要求爬蟲 (QS Ranking Crawler)

## 使用方法

### 1. 安裝

```bash
pip install -r requirements.txt
```

### 2. 交互模式（推薦）

直接執行腳本，無需參數即可使用交互式選單：

```bash
python3 clawer_main.py
```

按照螢幕提示操作：
1. 選擇排名類型
2. 選擇特定學科
3. 根據國家或地區篩選
4. 設定排名數量限制

### 3. 命令行介面 (CLI)

使用參數直接執行：

```bash
# 預設：世界前 100 大學，主控台輸出
python3 clawer_main.py

# 指定國家（例如：美國、英國、台灣）
python3 clawer_main.py --country us
python3 clawer_main.py --country uk --limit 20
python3 clawer_main.py --country tw

# 匯出到檔案（CSV, Excel, JSON）
python3 clawer_main.py --country ca --format excel --output canada_data.xlsx
python3 clawer_main.py --country au --format csv --output australia_data.csv

# 多國選擇（CLI 僅支援單一國家代碼別名，複雜篩選請使用交互模式）
python3 clawer_main.py --country "us" --limit 10

# 顯示完整幫助訊息
python3 clawer_main.py --help
```

## 支援國家（部分列表）

| 代碼 | 國家 | 代碼 | 國家 |
|------|------|------|------|
| `us` | 美國 | `sg` | 新加坡 |
| `uk` | 英國 | `hk` | 香港 |
| `ca` | 加拿大 | `cn` | 中國 |
| `au` | 澳洲 | `jp` | 日本 |
| `de` | 德國 | `tw` | 台灣 |
| `fr` | 法國 | `kr` | 南韓 |

*使用交互模式可查看完整可用國家列表。*
