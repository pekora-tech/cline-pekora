# Cline 客製化指南

本指南旨在協助你深入了解 Cline 的運作方式，並為你客製化 Cline 提供更全面的建議。

## 1. 深入了解 Cline 的核心架構

Cline 採用模組化的架構，分為核心擴展和 Webview UI 兩個主要部分。

### 1.1 核心擴展

核心擴展負責處理任務的生命週期、API 請求、工具執行和狀態管理。

*   **主要檔案：**
    *   `src/extension.ts`: 擴展的啟動入口點。
    *   `src/core/Cline.ts`: 核心類別，負責處理任務的生命週期、API 請求、工具執行和狀態管理。
    *   `src/core/webview/ClineProvider.ts`: WebviewViewProvider，負責提供 Webview UI 的內容和管理擴展的狀態。
*   **主要功能：**
    *   **任務管理：** 啟動、恢復和中止任務。
    *   **API 請求：** 發送 API 請求，處理 API 的回應，管理 API 的上下文視窗。
    *   **工具執行：** 執行命令列工具和瀏覽器動作，檢查工具的自動批准設定。
    *   **狀態管理：** 管理任務的狀態，包括 API 的對話歷史、UI 訊息和檢查點。
    *   **環境資訊：** 收集環境資訊，例如可見檔案、開啟的標籤頁、活動終端機和 VS Code 工作區錯誤。
    *   **檔案操作：** 處理 `.clineignore` 檔案，限制對某些檔案的存取，顯示檔案的差異，允許使用者編輯檔案。

### 1.2 Webview UI

Webview UI 負責呈現使用者介面和與使用者互動。

*   **主要檔案：**
    *   `webview-ui/src/App.tsx`: Webview UI 的主要結構。
    *   `webview-ui/src/context/ExtensionStateContext.tsx`: 管理 Webview UI 的狀態。
*   **主要功能：**
    *   **呈現使用者介面：** 顯示不同的視圖，例如歡迎視圖、設定視圖、歷史視圖和聊天視圖。
    *   **與使用者互動：** 接收使用者的輸入，並將其傳遞給核心擴展。
    *   **管理 UI 狀態：** 儲存和讀取 UI 的狀態，例如設定、歷史記錄和聊天訊息。

## 2. 客製化 Cline 的步驟

### 2.1 準備工作

1.  **安裝必要的工具：** 確保你已安裝 Node.js、npm 和 VS Code。
2.  **下載 Cline 的原始碼：** 從 GitHub 倉庫下載 Cline 的原始碼。
3.  **建立自己的分支：** 在開始修改 Cline 的程式碼之前，請先建立自己的分支，以避免影響原始程式碼。
4.  **安裝依賴：** 在 Cline 的根目錄下執行 `npm install` 命令，安裝所有必要的依賴。

### 2.2 修改 Cline 的程式碼

1.  **從小型修改開始：** 從小型修改開始，例如修改 UI 的外觀或新增一個簡單的功能。
2.  **逐步擴展：** 在熟悉 Cline 的程式碼後，可以逐步擴展其功能，例如新增對其他 API 供應商的支援或整合其他 VS Code 功能。
3.  **遵循 Cline 的程式碼風格：** 在修改 Cline 的程式碼時，請務必遵循其程式碼風格，以保持程式碼的一致性。

### 2.3 測試

在修改 Cline 的程式碼後，請務必進行測試，以確保其功能正常。

1.  **執行單元測試：** 執行 Cline 的單元測試，以確保你的修改沒有破壞現有的功能。
2.  **進行整合測試：** 進行整合測試，以確保你的修改與 Cline 的其他部分能夠正常協同工作。
3.  **進行使用者測試：** 邀請其他使用者測試你的修改，以確保其易於使用且符合使用者的需求。

### 2.4 部屬

在完成測試後，你可以將你的修改部署到 VS Code 擴展市場。

1.  **建立 VS Code 擴展套件：** 使用 `vsce package` 命令建立 VS Code 擴展套件。
2.  **發布到 VS Code 擴展市場：** 使用 `vsce publish` 命令將擴展套件發布到 VS Code 擴展市場。

## 3. 客製化 Cline 的具體建議

### 3.1 修改 UI 的外觀

你可以修改 Webview UI 的 CSS 檔案，以改變 Cline 的外觀。

*   **主要檔案：**
    *   `webview-ui/src/index.css`: Webview UI 的主要 CSS 檔案。
    *   `webview-ui/src/components/`: 包含各種 UI 組件的 CSS 檔案。

### 3.2 新增對其他 API 供應商的支援

你可以新增對其他 API 供應商的支援，例如 Google Gemini 或 Microsoft Azure OpenAI。

1.  **建立新的 API 供應商檔案：** 在 `src/api/providers/` 目錄下建立新的 API 供應商檔案。
2.  **實作 API 供應商的介面：** 在新的 API 供應商檔案中，實作 `ApiHandler` 介面。
3.  **更新 `buildApiHandler` 函數：** 在 `src/api/index.ts` 檔案中，更新 `buildApiHandler` 函數，以支援新的 API 供應商。
4.  **更新 UI：** 在 Webview UI 中，新增對新的 API 供應商的支援。

### 3.3 整合其他 VS Code 功能

你可以整合其他 VS Code 功能，例如程式碼格式化或程式碼檢查。

1.  **使用 VS Code API：** 使用 VS Code API 來存取和操作 VS Code 的功能。
2.  **新增命令：** 在 `src/extension.ts` 檔案中，新增命令來觸發 VS Code 功能。
3.  **更新 UI：** 在 Webview UI 中，新增按鈕或選單項目來觸發新的命令。

## 4. Cline 的文件

Cline 提供了詳細的文件，可以幫助你了解其運作方式和如何進行客製化。

*   **README.md**: Cline 的主要說明文件。
*   **CONTRIBUTING.md**: Cline 的貢獻指南。
*   **docs/**: 包含 Cline 的架構、客製化和 MCP 相關的文件。

## 5. 注意事項

*   **保持程式碼的一致性：** 在修改 Cline 的程式碼時，請務必遵循其程式碼風格，以保持程式碼的一致性。
*   **進行測試：** 在修改 Cline 的程式碼後，請務必進行測試，以確保其功能正常。
*   **參考 Cline 的文件：** Cline 提供了詳細的文件，可以幫助你了解其運作方式和如何進行客製化。

希望本指南能幫助你成功客製化 Cline，打造一個屬於你的 VS Code 客製程式碼。
