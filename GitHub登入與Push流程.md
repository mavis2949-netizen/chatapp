# GitHub 登入與 Push 流程筆記

這份筆記說明如何把本機專案上傳到 GitHub。

## 1. 登入 GitHub 網站

1. 開啟 <https://github.com>。
2. 點選右上角 **Sign in**。
3. 輸入 GitHub 帳號、密碼，並依畫面完成驗證。
4. 登入後可在右上角頭像確認目前帳號。

## 2. 建立空白 Repository

1. 開啟 <https://github.com/new>。
2. 輸入 Repository name，例如 `chatapp`。
3. 選擇 Public 或 Private。
4. 如果本機已經有專案，請不要勾選 **Add a README file**、`.gitignore` 或 License。
5. 點選 **Create repository**。
6. 複製 repository 的 HTTPS 網址，例如：

   ```text
   https://github.com/你的帳號/chatapp.git
   ```

## 3. 安裝與確認 Git

在 PowerShell 執行：

```powershell
git --version
```

如果顯示 Git 版本，表示已安裝。若沒有，請先到 <https://git-scm.com/downloads> 安裝 Git，安裝後重新開啟終端機。

## 4. 設定 Git 作者資訊

第一次使用 Git 時，設定 commit 顯示的名稱與 email：

```powershell
git config --global user.name "你的 GitHub 名稱"
git config --global user.email "你的 GitHub email"
```

確認設定：

```powershell
git config --global --get user.name
git config --global --get user.email
```

> 若不想公開個人 email，可在 GitHub 的 Email settings 開啟 noreply email，再使用 GitHub 提供的 noreply email。

## 5. 初始化本機專案

在專案根目錄開啟 PowerShell，執行：

```powershell
git init
git add .
git status
```

`git status` 會列出準備上傳的檔案。請確認 `.venv/`、`.env`、密碼或 API key 沒有被加入；應透過 `.gitignore` 排除它們。

## 6. 建立第一次 Commit

```powershell
git commit -m "Initial project commit"
git branch -M main
```

## 7. 連結 GitHub Repository 並 Push

將網址替換成自己的 repository HTTPS 網址：

```powershell
git remote add origin https://github.com/你的帳號/你的-repository.git
git push -u origin main
```

第一次 push 時可能會要求登入 GitHub。請依畫面選擇瀏覽器登入並按 **Authorize**，授權 Git 或 GitHub CLI 存取 repository。

## 8. 確認 Push 成功

執行：

```powershell
git status
git remote -v
```

成功時通常會看到：

```text
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

接著重新整理 GitHub repository 頁面，就能看到上傳的檔案。

## 9. 後續修改後再次 Push

每次修改後重複以下三步：

```powershell
git add .
git commit -m "說明這次修改"
git push
```

## 常見問題

### `remote origin already exists`

表示 repository 已經連結過。先確認網址：

```powershell
git remote -v
```

需要更換網址時：

```powershell
git remote set-url origin https://github.com/你的帳號/你的-repository.git
```

### Push 時要求登入或被拒絕

請確認登入的是擁有該 repository 寫入權限的 GitHub 帳號。若使用 HTTPS，依 Git 的登入提示完成瀏覽器授權即可。

### 不小心把密碼或 API key 加入 Git

立刻停止推送，將敏感資料移到 `.env`，並將 `.env` 加入 `.gitignore`。已經推送的金鑰應立即到服務商網站撤銷並重新產生。
