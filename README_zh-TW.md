# Context Engineering Template  (Gemini CLI 版本)

> 🌐 **Language**: [English](README.md) | [繁體中文](README_zh-TW.md)

一個全面的範本，用於開始情境工程——為 AI 編碼助理工程情境的學科，使其擁有完成端到端工作所需的資訊。

**情境工程比提示工程好 10 倍，比隨意編碼好 100 倍。**

---

## 🚀 快速開始

```bash
# 1. 複製此範本
git clone https://github.com/google-gemini/context-engineering-gemini.git
cd context-engineering-gemini

# 2. 安裝依賴項 (Gemini CLI)
# 請參閱原始專案以了解安裝方式：https://github.com/google-gemini/gemini-cli

# 3. 建立您的初始功能請求
cp INITIAL.md request.md
# ... 然後編輯 request.md 以包含您的功能需求

# 4. 啟動 Gemini CLI
gemini

# 5. 生成全面的 PRP (產品需求提示)
# 在 Gemini CLI 中，執行：
/PRP:generate-prp request.md

# 6. 執行 PRP 以實作您的功能
# 在 Gemini CLI 中，執行：
/PRP:execute-prp PRPs/request_prp.md
```

## 📚 目錄

* [Context Engineering Template  (Gemini CLI 版本)](#context-engineering-template--gemini-cli-版本)
  * [🚀 快速開始](#-快速開始)
  * [📚 目錄](#-目錄)
  * [什麼是情境工程？](#什麼是情境工程)
  * [範本結構](#範本結構)
  * [逐步指南](#逐步指南)
  * [撰寫有效的 INITIAL.md 檔案](#撰寫有效的-initialmd-檔案)
  * [PRP 工作流程](#prp-工作流程)
  * [有效利用範例](#有效利用範例)
  * [最佳實踐](#最佳實踐)
  * [📚 資源](#-資源)
  * [致謝](#致謝)

---

## 什麼是情境工程？

情境工程代表了從傳統提示工程的典範轉移：

### 提示工程 vs 情境工程

**提示工程：**

* 專注於巧妙的措辭和特定的表達

* 僅限於您表達任務的方式

* 就像給某人一張便利貼

**情境工程：**

* 一個提供全面情境的完整系統

* 包括文件、範例、規則、模式和驗證

* 就像編寫一個包含所有細節的完整劇本

### 為什麼情境工程很重要

1. **減少 AI 失敗：** 大多數代理失敗不是模型失敗——它們是情境失敗

2. **確保一致性：** AI 遵循您的專案模式和慣例

3. **啟用複雜功能：** AI 可以透過適當的情境處理多步驟實作

4. **自我修正：** 驗證循環允許 AI 修正自己的錯誤

## 範本結構

```text
context-engineering-gemini/
│
├── .gemini/                  # 包含所有 AI 相關工具和範本。
│   ├── commands/
│   │   └── PRP/
│   │       ├── execute-prp.toml
│   │       └── generate-prp.toml
│   └── templates/
│       └── prp_template.md
│
├── PRPs/                     # 儲存由 AI 生成的詳細 PRP 藍圖。
│   ├── weather_cli_prp.md
│   └── ...
│
├── examples/                 # 您的程式碼範例供 AI 遵循。
│
├── src/                      # 您的應用程式原始碼位於此處。
│   ├── weather/              # Python 範例
│   │   ├── api.py
│   │   └── cli.py
│   └── linkchecker/          # Go 範例
│       ├── main.go
│       ├── parser.go
│       └── validator.go
│
├── tests/                    # 您的原始碼的單元測試。
│   ├── test_weather.py
│   └── linkchecker_test.go
│
├── .gitignore
├── GEMINI.md                 # AI 助理的全球規則和原則。
├── INITIAL.md                # 用於撰寫新功能請求的空白範本。
├── INITIAL_EXAMPLE.md        # 已完成功能請求的範例。
└── README.md                 # 此檔案。
```

**未來方向：**

此範本為情境工程提供了堅實的基礎。此工作流程的下一個演進可能涉及整合更進階的 AI 技術，例如用於自動文件研究的檢索增強生成 (RAG) 和用於完全自主實作和測試循環的 AI 驅動工具 (函數呼叫)。

## 逐步指南

此框架使用強大、兩步驟的工作流程來使用 Gemini 建構軟體。

### 1. 設定全球規則 (GEMINI.md)

`GEMINI.md` 檔案包含 AI 助理將遵循的專案範圍規則。您可以在此處定義您的架構原則、編碼標準和測試要求，以確保一致性。您可以使用提供的範本或為您的專案自訂它。

### 2. 建立功能請求

要開始一個新功能，您不要直接編輯 `INITIAL.md` 範本。而是：

1. **複製** `INITIAL.md` 到一個名為 `request.md` 的新檔案。
2. **填寫** `request.md` 以包含您的新功能的詳細資訊。請參閱下面的「撰寫有效的 INITIAL.md 檔案」部分以獲取提示。

### 3. 生成 PRP (計畫)

首先，在您的終端機中啟動 Gemini CLI：

```shell
gemini
```

現在，執行 `generate-prp` 命令。此命令將您的功能請求發送給 Gemini，並要求它充當高級工程師，建立一個詳細的技術藍圖，稱為產品需求提示 (PRP)。

```shell
/PRP:generate-prp request.md
```

這將在 `PRPs/` 目錄中建立一個新的、永久的 PRP 檔案。

> **注意：** `/PRP:generate-prp` 和 `/PRP:execute-prp` 命令是定義在 `.gemini/commands/PRP/` 目錄中的自訂命令。您可以檢查和修改它們以適應您的工作流程。

### 4. 執行 PRP (自動化代理)

這就是奇蹟發生的地方。使用新建立的 PRP 的路徑執行 `execute-prp` 命令。

```shell
/PRP:execute-prp PRPs/request_prp.md
```

此命令充當一個 **AI 代理**：

1. 它將詳細的 PRP 發送給 Gemini 以獲取逐步實作計畫。
2. 它解析 AI 的回應，識別要執行的 shell 命令和要建立的程式碼檔案。
3. 它然後會逐步執行此計畫，在執行任何命令或寫入任何檔案之前，**暫停以徵求您的確認**。

這讓您可以坐下來監督 AI 為您建構整個功能，就在您的本地終端機中。

## 撰寫有效的 INITIAL.md 檔案

`INITIAL.md` 檔案是任何新功能的起點。您在此處輸入的品質直接影響 AI 輸出的品質。以下是如何使其有效：

* **🎯 目標：** 具體而明確。不要寫「製作登入頁面」，而是寫「建立一個包含電子郵件/密碼欄位、一個『忘記密碼』連結和 Google OAuth 整合的登入頁面」。細節越多越好。

* **🎨 靈感與範例：** 這是最強大的部分之一。如果您有現有的檔案顯示您如何處理 API 用戶端、資料庫連線或錯誤處理，請在此處引用它。它為 AI 提供了一個具體的模式可遵循，確保一致性。

* **📚 所需知識：** 不要讓 AI 猜測。提供指向它將需要的確切 API 文件、函式庫或 Stack Overflow 討論串的直接連結。這可以節省時間並防止 AI 使用過時或不正確的資訊。

* **⚠️ 潛在陷阱與注意事項：** 思考可能出錯的地方。API 是否有奇怪的速率限制？是否有棘手的身份驗證流程？提前提及這些有助於 AI 避免常見錯誤並從一開始就建構更穩健的程式碼。

## PRP 工作流程

PRP (產品需求提示) 工作流程是一個兩步驟的過程，旨在確保 AI 在編寫任何程式碼之前擁有全面的計畫。

1. **生成 (`generate-prp`)：** 第一步是關於**規劃**。此命令將您的高級 `INITIAL.md` 功能請求發送給 Gemini，並要求它將其擴展為詳細的技術藍圖 (PRP)。此藍圖包括建議的檔案結構、任務分解、偽程式碼和驗證計畫。它強制 AI 首先思考整個實作。

2. **執行 (`execute-prp`)：** 第二步是關於**實作**。此命令將詳細的 PRP 發送回 Gemini，並附帶明確的指令：「建構此功能」。由於所有研究和規劃都已完成，AI 可以專注於編寫遵循藍圖的乾淨、正確的程式碼。

這種規劃與實作的分離是工作流程成功的關鍵。

## 有效利用範例

`examples/` 資料夾是您確保專案一致性的秘密武器。AI 助理擅長模式識別。

### 什麼是好的範例？

* **完整模式：** 顯示一個完整、可運作的模式範例，而不僅僅是一個片段。例如，提供一個完整的 API 用戶端類別，而不僅僅是一個函數。

* **程式碼結構：** 包含您如何建構類別、組織匯入和命名變數的範例。

* **錯誤處理：** 顯示您期望如何捕獲和處理錯誤。這通常被忽略，但對於生產品質的程式碼至關重要。

* **測試：** 提供一個測試檔案 (`test_*.py`) 的範例，顯示您偏好的測試風格，包括如何使用模擬。

您提供的品質範例越多，AI 需要猜測的就越少，最終程式碼就越像您自己編寫的。

### 範例結構

```text
examples/
├── README.md           # 解釋每個範例的用途
├── api_client.py       # 完整、結構良好的 API 用戶端
├── data_models.py      # Pydantic 模型或資料結構
└── tests/              # 測試模式
    └── test_api_client.py # 包含模擬的測試檔案範例
```

## 最佳實踐

* **明確：** 永遠不要假設 AI 知道您的偏好。您在 `INITIAL.md` 和 `GEMINI.md` 檔案中越明確，結果就會越好。

* **迭代過程：** 如果 AI 犯了錯誤，不要只修正程式碼。思考它為什麼會犯錯。`GEMINI.md` 中的規則是否需要更清楚？您是否需要在 `examples/` 資料夾中提供更好的範例？改進過程將防止相同的錯誤再次發生。

* **信任工作流程：** 撰寫詳細的 `INITIAL.md` 和審查 PRP 可能看起來像是額外的工作，但這項前期投資可以節省大量的調試和重構時間。

## 📚 資源

* Gemini CLI Repository:[https://github.com/google-gemini/context-engineering-gemini](https://github.com/google-gemini/context-engineering-gemini)
* Blog: A Practical Guide to Context Engineering with Gemini:[https://aryan-gupta.is-a.dev/blog/2025/context-engineering/](https://aryan-gupta.is-a.dev/blog/2025/context-engineering/)
* Context-Engineering-Intro: [https://github.com/coleam00/context-engineering-intro](https://github.com/coleam00/context-engineering-intro)

## 致謝

此專案的工作流程和情境工程的核心概念受到 coleam00 原始 [Context-Engineering-Intro](https://github.com/coleam00/context-engineering-intro) 儲存庫的啟發。雖然程式碼和範本已針對基於 Gemini 的工作流程進行了重寫，但基本思想來自該出色的專案。
