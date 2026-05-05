# Trip App Generator

填入你的行程資料，自動產出一個可直接部署的旅遊協調 App。

**Live demo**: [trips.claire-cheng.com/generator/](https://trips.claire-cheng.com/generator/)（自訂網域設定中，暫用 [trip-v2.netlify.app/generator/](https://trip-v2.netlify.app/generator/)）

---

## 什麼是 Trip App Generator？

一個 5 步驟的精靈式工具，不需要寫程式，填完表單就能下載一個完整的旅遊 App（單一 HTML 檔）。

產出的 App 功能包含：每日行程、天氣預報、集合倒數、群組留言、費用分帳、打包清單、購物清單、PIN 碼保護。

---

## 使用方式

1. 前往 [生成器頁面](https://trip-v2.netlify.app/generator/)
2. 選擇輸入模式：
   - **AI 解析**：貼上行程文字 + 填入自己的 Claude API Key，AI 自動結構化
   - **手動輸入**：逐天填寫活動
3. 填入基本設定（旅程名稱、日期、人數、PIN 碼）
4. 填入 Firebase Realtime Database 設定（可跳過，略過即時同步功能）
5. 選擇主題色彩
6. 點「下載 App」，取得 `index.html`
7. 上傳到 GitHub Pages / Netlify / Cloudflare Pages 等任何靜態平台

---

## Firebase 設定（選填）

集合倒數、群組留言、費用分帳需要 Firebase。

1. 前往 [console.firebase.google.com](https://console.firebase.google.com) 建立免費專案
2. 建立 Realtime Database（選 Asia-Southeast1）
3. 規則設為 `{ "rules": { ".read": true, ".write": true } }`
4. 將專案設定填入生成器 Step 4

---

## 專案結構

```
trip-app-generator/
├── index.html          ← 首頁 / 導引頁
├── manifest.json       ← PWA manifest
├── sw.js               ← Service Worker
└── generator/
    ├── index.html      ← 生成器主程式
    └── schema-example.json  ← 行程資料格式範例
```

> 注意：此公開 repo 的 Firebase 欄位為示範假值。實際行程 App 請填入自己的 Firebase 設定。

---

## 技術

- 純 HTML / CSS / JavaScript，無框架，無 build 工具
- 生成模板以 Base64 編碼嵌入，避免 `</script>` 解析問題
- AI 解析使用 Anthropic Claude API（使用者自備 Key）
- 天氣預報使用 Open-Meteo（免費，無需 API Key）
