# Cloudflare Pages 部署指南

本專案為純前端的 React + Vite 應用程式，專為 **Cloudflare Pages** 進行了最佳化配置（包含 SPA 路由重定向 `_redirects`、安全與快取標頭 `_headers`、以及 `wrangler.jsonc` 設定檔）。

你可以透過以下 **3 種方式** 輕鬆部署到 Cloudflare：

---

### 方法一：連結 GitHub 自動部署（最推薦，每次 push 自動更新）

1. 將本專案代碼推送到你的 GitHub 儲存庫（Repository）。
2. 前往 [Cloudflare 控制台 (Cloudflare Dashboard)](https://dash.cloudflare.com/)。
3. 點擊左側選單的 **「Workers & Pages」** -> **「Create application」** -> 選擇 **「Pages」** 分頁。
4. 點擊 **「Connect to Git」** 並選擇你的 GitHub 儲存庫。
5. 在「Build settings」設定：
   - **Framework preset**: `Vite`
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
6. 點擊 **「Save and Deploy」**，Cloudflare 即會在 1 分鐘內自動完成建置並提供專屬網址（例如：`https://suica-card-maker.pages.dev`）！

---

### 方法二：使用 Wrangler 命令列部署

本專案已內建 Cloudflare 官方的 `wrangler` 工具與預設指令：

1. **登入 Cloudflare 帳號**（只需執行一次）：
   ```bash
   npx wrangler login
   ```
2. **一鍵建置並部署**：
   ```bash
   npm run deploy
   ```
   *或者手動執行：*
   ```bash
   npm run build
   npx wrangler pages deploy dist --project-name=suica-card-maker
   ```
3. 部署完成後，命令列終端機將立即顯示可訪問的 Cloudflare Pages 網址！

---

### 方法三：Cloudflare 後台拖曳上傳（無需 Git、無需命令列）

1. 在本機或專案終端機執行打包：
   ```bash
   npm run build
   ```
   這會在專案根目錄產生 `dist` 資料夾。
2. 開啟 [Cloudflare Dashboard](https://dash.cloudflare.com/)。
3. 點擊 **「Workers & Pages」** -> **「Create application」** -> 選擇 **「Pages」**。
4. 選擇 **「Upload assets」**（直接上傳檔案）。
5. 設定 Project Name（例如 `suica-card-maker`），將 `dist` 資料夾直接拖曳進上傳區域。
6. 點擊 **「Deploy site」** 即可立即上線！

---

### 專案內建的 Cloudflare 配置說明

- **`public/_redirects`**：設定 `/* /index.html 200`，確保任何頁面重整都不會出現 404 錯誤。
- **`public/_headers`**：為靜態資源自動啟用長期快取（Cache-Control: immutable）並增強 HTTP 安全標頭。
- **`wrangler.jsonc`**：Cloudflare 官方標準配置檔，指定靜態輸出目錄為 `dist`。
