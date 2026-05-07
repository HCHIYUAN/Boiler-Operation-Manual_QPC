# SE-APG ボイラー SOP Portal

> 國精化學股份有限公司 ‧ QUALIPOLY CHEMICAL CORP.
> SE-APG 系列小型貫流瓦斯鍋爐標準操作程序網站

中文 / 日本語 雙語標準操作程序（SOP）入口網站，純靜態 HTML/CSS/JS，可一鍵部署到 Vercel。

---

## 📋 文件清單

| 文件 | 說明 | 紙張 |
|---|---|---|
| **SOP-01a** | 開機與啟動運轉 / 起動と運転開始 | A3 海報 |
| **SOP-01b** | 巡檢與停機作業 / 巡視と停止作業 | A3 海報 |
| **SOP-02** | 全排放作業 / 全ブロー作業 | A3 海報 |
| **SOP-03** | 異常顯示速查卡 / 異常表示クイックカード | A4 雙面 |
| **SOP-04** | 操作面板燈號圖 / 操作パネルランプ対照図 | A3 海報 |

每份文件提供 **中文（繁體）** + **日本語** 雙語版本。

---

## 🚀 部署到 Vercel

### 一鍵部署（最快）

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)

把這個 repo 連到 Vercel：

1. 推到 GitHub（請看下方「初次推送」）
2. 在 [vercel.com/new](https://vercel.com/new) 點 **Import Git Repository**
3. 選擇你的 repo
4. **Framework Preset** 選 **Other**（純靜態）
5. **Build Command** 留空
6. **Output Directory** 留空
7. 點 Deploy ✅

### Vercel CLI

```bash
npm i -g vercel
cd sop-website
vercel --prod
```

---

## 🛠 初次推送到 GitHub

```bash
# 1. 在這個資料夾初始化 git
cd sop-website
git init
git add .
git commit -m "feat: initial SOP portal"

# 2. 在 GitHub 建立 repo（建議名稱：sop-portal 或 boiler-sop）
#    然後連結 remote：
git branch -M main
git remote add origin https://github.com/你的帳號/repo名稱.git
git push -u origin main
```

之後每次更新：

```bash
git add .
git commit -m "fix: 修正 SOP-02 排版"
git push
```

---

## 🌐 部署後網址

主頁：
```
https://你的專案.vercel.app/
```

支援 hash 深層連結（可貼給同事直接開特定文件）：

| 連結 | 開啟內容 |
|---|---|
| `/#zh/SOP-01a-startup` | 中文 ‧ 開機海報 |
| `/#jp/SOP-01a-startup` | 日文 ‧ 起動ポスター |
| `/#zh/SOP-03-fault-quickref` | 中文 ‧ 異常速查卡 |
| `/#jp/SOP-02-full-blowdown` | 日文 ‧ 全ブロー作業 |

---

## 📁 資料夾結構

```
sop-website/
├── index.html              # 入口頁（左側導覽 + 上方語言切換）
├── vercel.json             # Vercel 部署設定（cleanUrls + 安全 headers）
├── .gitignore              # Git 排除清單
├── README.md               # 本文件
│
├── zh/                     # 中文版 SOP 內容
│   ├── SOP-01-manual.html         # 操作手冊版（A4 9頁，輔助下載）
│   ├── SOP-01a-startup.html       # 開機海報
│   ├── SOP-01b-shutdown.html      # 停機海報
│   ├── SOP-02-full-blowdown.html  # 全排放海報
│   ├── SOP-03-fault-quickref.html # 異常速查卡
│   └── SOP-04-panel-lights.html   # 操作面板燈號圖
│
└── jp/                     # 日本語版 SOP 內容（同上 6 份）
    └── （與 zh/ 相同檔名）
```

---

## ⚙️ 自訂

### 切換預設語言

編輯 `index.html`，搜尋 `parseHash()` 函式：

```js
function parseHash() {
  const hash = window.location.hash.replace('#', '');
  if (!hash) return { lang: 'zh', doc: null };  // ← 改 'zh' 為 'jp'
  ...
}
```

### 加入新 SOP 文件

1. 把 HTML 放到 `zh/` 與 `jp/` 對應目錄
2. 在 `index.html` 的 `<ul class="nav-list">` 加：
   ```html
   <li class="nav-item">
     <a class="nav-link" data-doc="SOP-05-your-doc">
       <div class="nav-row">
         <span class="nav-code">SOP-05</span>
         <span class="nav-tag" data-i18n="tag-poster">POSTER</span>
       </div>
       <div class="nav-title" data-i18n="doc-05">新文件名稱</div>
       <div class="nav-meta">A3 ‧ 1P ‧ DESCRIPTION</div>
     </a>
   </li>
   ```
3. 在 `I18N` 物件加翻譯：
   ```js
   zh: { ..., 'doc-05': '新文件名稱', ... },
   jp: { ..., 'doc-05': '新しい文書', ... },
   ```

---

## 🖨 列印 PDF

點選文件後，工具列右上「**列印 / 存 PDF**」按鈕：
- Chrome / Edge：自動觸發列印對話框
- ⚠️ 重要：**勾選「背景圖形」** 才能保留米色背景與方格底紋

或點「**新分頁開啟**」，在新分頁直接 `Ctrl+P` 列印。

---

## 🔤 字型

HTML 主字型為 `PMingLiU`（新細明體）：

- **Windows / Mac**：自動套用新細明體（最佳效果）
- **Linux** 伺服器：fallback 至 serif（仍可正常閱讀）

---

## 📦 版本資訊

| 項目 | 值 |
|---|---|
| 版本 | REV. A（首版） |
| 發行 | 2026-XX-XX |
| 適用機種 | SE-2000 / SE-2500 / SE-3000 APG |
| 有效期限 | 發行日後 12 個月 |

---

## 📞 緊急聯絡（請於部署後更新）

- 現場主管：________________
- 廠內維修工程師：________________
- 原廠 / 代理商：香昇國際實業 ‧ 02-2278-3636
- 緊急消防：119

---

## License

Internal use only ‧ © 2026 國精化學股份有限公司
