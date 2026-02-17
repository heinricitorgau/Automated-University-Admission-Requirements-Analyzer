# Automated University Admission Requirements Analyzer (In Development)

------------------------------------------------------------------------

## ⚠️ Project Status

This project is currently under development.\
Source code has not yet been fully organized or uploaded.

This repository currently serves as documentation of development
progress and project structure planning.

------------------------------------------------------------------------

## Project Description

This is a personal learning project focused on:

-   Understanding ranking website data structures\
-   Practicing modular Python project architecture\
-   Experimenting with synchronous and asynchronous HTTP requests\
-   Handling unstable external APIs\
-   Basic data parsing and formatted output

This project is for learning and research purposes only.\
It is not affiliated with QS or any ranking organization.

------------------------------------------------------------------------

## Current Development Scope

The internal structure is being modularized into:

-   Entry script (main)
-   Crawler controller logic
-   Network request layer (fetcher)
-   Parsing layer (extractor)
-   Output layer (exporter)
-   Configuration module
-   Data models

The structure may change significantly as development continues.

------------------------------------------------------------------------

## Known Development Issues

During experimentation, the following issues were observed:

-   API occasionally returns 404 or HTML instead of JSON\
-   Some subject rankings produce inconsistent outputs\
-   Async requests may cause timeout errors\
-   SSL certificate verification errors on macOS virtual environments\
-   API parameter changes may break compatibility

These are part of the ongoing learning process.

------------------------------------------------------------------------

## Learning Objectives

This project aims to improve understanding of:

-   Python project structuring\
-   Error handling and retry logic\
-   Asynchronous programming (aiohttp)\
-   Separation of concerns in software design

------------------------------------------------------------------------

## Future Plans (Tentative)

-   Further modular refactoring\
-   Improved stability handling\
-   Cleaner CLI interface\
-   Better logging and error reporting

No timeline is guaranteed.

------------------------------------------------------------------------

# 中文說明

------------------------------------------------------------------------

## ⚠️ 專案狀態

本專案目前仍在開發與整理中，\
尚未完整上傳所有程式碼。

本倉庫暫時用於記錄架構規劃與開發過程。

------------------------------------------------------------------------

## 專案說明

這是一個個人學習型專案，主要目的為：

-   理解排名網站的資料結構\
-   練習 Python 模組化專案設計\
-   嘗試同步與非同步 HTTP 請求\
-   學習如何處理不穩定的外部 API\
-   基礎資料解析與輸出

本專案僅供學習與研究用途，\
與 QS 或任何官方機構無關。

------------------------------------------------------------------------

## 目前開發方向

目前正在嘗試將專案拆分為：

-   主程式入口\
-   爬蟲控制邏輯\
-   網路請求層\
-   資料解析層\
-   輸出模組\
-   設定管理\
-   資料模型

架構仍可能大幅調整。

------------------------------------------------------------------------

## 開發過程遇到的問題

-   API 偶爾回傳 404 或 HTML\
-   部分 Subject Ranking 會出現例外\
-   非同步請求可能 Timeout\
-   macOS venv SSL 憑證問題\
-   參數變動導致 API 失效

以上問題仍在研究與調整中。

------------------------------------------------------------------------

## 學習目標

本專案主要用於練習：

-   Python 專案架構設計\
-   錯誤處理與重試機制\
-   非同步程式設計\
-   模組化分層思維

------------------------------------------------------------------------

## 未來規劃（暫定）

-   架構重構\
-   穩定性優化\
-   改善錯誤訊息\
-   CLI 介面整理\
-   程式碼清理

尚無確定時程。
