# Simple Full Stack Demo

這是一個使用 Vanilla HTML、CSS、JavaScript 與 FastAPI 製作的簡易聊天範例。

## 專案結構

```text
frontend/  # 靜態網頁
backend/   # FastAPI API
```

## 本機執行

1. 啟動後端：

   ```powershell
   cd backend
   pip install -r requirements.txt
   uvicorn main:app --reload
   ```

2. 使用 Live Server 或其他靜態網站伺服器開啟 `frontend/index.html`。

前端預設呼叫 `http://127.0.0.1:8000`，因此後端必須在本機執行。

## GitHub

此儲存庫可直接上傳至 GitHub 以備份與分享原始碼。GitHub Pages 僅能發布 `frontend` 的靜態檔案；在沒有另外發布 FastAPI 後端時，GitHub Pages 上的聊天 API 無法連回你的本機電腦。
