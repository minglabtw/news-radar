# 全自動化n8n新聞發佈平台

你是 AI 程式開發代理，是這個專案的共同開發者。

## 這個專案是什麼

本專案透過 n8n 自動化流程，抓取中文新聞 RSS，交由 MiniMax M2.7 進行分析、總結與評分，最終自動生成靜態 HTML 日報部署至 GitHub Pages，同時推送 Telegram 通知。

---

## 📍 目前狀態 (最後更新：2026-05-28 22:48)

| 項目 | 狀態 |
|------|------|
| 整體進度 | 🟢 **V5.0 全中文聚焦版** — 5 領域 16 個 RSS 來源、純繁體中文精煉、每日 8:00 排程 |
| 目前版本 | `src/workflow-native-v3.json` — Server ID: `1TMNv2FvxSsBAjrm` |
| 部署方式 | `node src/deploy_and_run.js` (原地熱更新 PUT + 觸發) |
| 排程時段 | 每日 **8:00** (Asia/Taipei) |
| 部署目標 | `minglabtw/news-radar` (GitHub Pages via Actions) |
| 執行狀態 | 🟢 運作正常 (最新執行 ID: 549) |
| 主要阻斷 | 🟢 **無** — 所有已知問題已解決 |

---

### 已驗證功能

- ✅ 5 大領域 (科技、綜合、財經、運動、生活) 全 RSS 抓取
- ✅ 雙通道 MiniMax M2.7 分析 (AI+Tech+Gaming+General / Finance+Sports+Health+Entertainment+Food+Travel)
- ✅ 總編輯整合 Briefing + Spotlight 焦點推薦
- ✅ **純繁體中文標題精煉 (非翻譯)** — 已移除所有英翻中邏輯
- ✅ **Prompt 加入「請勿計算字數」防崩潰指令**
- ✅ **部署腳本自動刪除 versionId** — 防部分更新
- ✅ **字體放大 20px** (老花友善)
- ✅ **自動化部署至 GitHub Pages** (index.html + 過刊牆)
- ✅ **Telegram 推播** (sendMessage、無 n8n footer、正確 minglabtw 網址)
- ✅ **LINE 通知** (continueRegularOutput，不卡流程)
- ✅ **GitHub Actions Pages 部署** (Actions 模式，不需 Jekyll)
- ✅ **79+ 篇多領域卡片**、Toolbar 晶片過濾、即時搜尋
- ✅ **Web Speech API 女聲播報** (美佳 Mei-Jia)
- ✅ **10 色 CSS 配色**、深色模式
- ✅ **過刊 archive.html** (前端動態渲染)
- ✅ **排程 8:00 Asia/Taipei** 自動執行

### 待改進 (不影響核心功能)

- [ ] **LINE 通知** — 改用 n8n 原生 HTTP Request 節點但不確定 Token 是否有效，`continueRegularOutput` 避免卡流程
- [ ] **MiniMax 輸出格式穩定性** — 新 prompt 對思考鏈模型偶爾失敗，fallback 到預設值
- [ ] **deploy_and_run.js webhook 觸發** — 6 秒等待可能不夠長，需觀察後調整

---

## ⚠️ 接手備忘錄

### 新手起手式
1. 先讀 `06-HANDOVER.md` (完整交接手冊)
2. 再讀 `04-決策記錄.md` (關鍵技術決策)
3. 再讀 `03-踩坑記錄.md` (已知問題與解法)
4. 再讀 `07-模型選型與MiniMax-M2.7使用守則.md` (MiniMax 使用守則)
5. 再讀 `05-n8n代理開發守則.md` (n8n 開發 SOP)

### 核心檔案

| 檔案 | 用途 |
|------|------|
| `src/workflow-native-v3.json` | **唯一的現行工作流** (勿修改舊版備份) |
| `src/deploy_and_run.js` | 自動部署腳本 (原地熱更新 PUT + 觸發) |
| `src/config.json` | 設定資料檔 (RSS 來源 + API Keys) |

### 重要地雷

- MiniMax M2.7 推理模型有「算字數強迫症」，Prompt 內**不可寫死字數限制**
- 部署前**必須刪除 `wfData.versionId`**，否則會部分更新
- `jsonBody` 在 n8n 中必須以 `=` 開頭 (`={{ $json.var }}`)
- 修改 Code 節點 jsCode 後，務必用 `node --check` 做語法驗證再匯入 n8n
- **不要修改舊版工作流備份**，只改 `workflow-native-v3.json`

### 最高原則

**一次只改一件事，改完測試確認後再繼續。不要多處同時改動。**

---

## 🔗 快速連結

| 服務 | 網址 |
|------|------|
| 新聞網站 | https://minglabtw.github.io/news-radar/ |
| 過刊牆 | https://minglabtw.github.io/news-radar/archive.html |
| GitHub 倉庫 | https://github.com/minglabtw/news-radar |

---

## 📋 一鍵部署

```bash
# 一鍵部署 + 觸發
node src/deploy_and_run.js
```

---

> 最後更新: 2026-05-28
> 版本: V5.0 全中文聚焦版
> 執行狀態: 🟢 運作正常 (最新執行 ID: 549)
