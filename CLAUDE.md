# CLAUDE.md — Trademark Advisor

> 給下一個 Claude session 的快速上手文件。30 秒內知道這是什麼、檔案在哪、能改什麼、不能碰什麼。

---

## 1. 專案是什麼

單檔 HTML 的 trademark 佈局策略顧問工具（中文 UI，繁體）。匯入 trademark portfolio 後產出策略分析與建議，內建 DEMO_DATA（糖村 Sugar & Spice 公開資料）作為展示。

- **線上**：https://tyj2025.github.io/Trademark-Advisor/（**public** GitHub Pages）
- **Repo**：https://github.com/TYJ2025/Trademark-Advisor (public)
- **Canonical 在 GitHub，不在這台 Mac**（見下方第 4 節紅線）

---

## 2. 檔案結構

```
Trademark Advisor/
├── index.html              103,110 bytes  ← GH Pages 服務的檔（從 GitHub sync 下來的）
├── README.md                              ← 從 GitHub sync
├── CLAUDE.md                              ← 本檔
└── archive/                               ← 2026-05-24 之前的本機古早 snapshot 備份
    ├── index.html.local-snapshot-20260524.bak              （61 KB, Apr 16 古早版）
    └── Trademark-Advisor.html.local-snapshot-20260524.bak  （62 KB, Apr 16 同步分支已棄）
```

HTML 是單檔（CSS / JS 全內嵌），不依賴外部資源。

---

## 3. 怎麼用

本機看：`open index.html`（不需要 server）。線上看：點上方 URL。

---

## 4. 🚨 紅線 — Canonical 在 GitHub，不在本機

**2026-05-24 audit 發現**：本機 `index.html` 跟 `Trademark-Advisor.html` 都是 4/16 的古早 snapshot；GitHub repo 的 `index.html` 已有 5 個 4/24 的新 commits（功能擴充、bug fix）。YJ 一直直接在 GitHub Web UI 或另一台機器編，本機 copy 從沒同步。

當下處置：
- 把本機 `index.html` 替換成 GitHub canonical 版本（103KB）
- 把舊 `Trademark-Advisor.html`（不再存在於 GitHub）搬進 `archive/`
- 加 README.md（從 GitHub sync）

**修改規則**：
- ✏️ 編輯**只**在 GitHub Web UI 或另一台有 .git 的 working copy 進行
- 🔁 本機 `index.html` **只是唯讀 snapshot**。要刷新就重抓：
  ```bash
  cd "$HOME/ClaudeProjects/Trademark Advisor"
  gh repo clone TYJ2025/Trademark-Advisor /tmp/ta && cp /tmp/ta/index.html index.html && cp /tmp/ta/README.md README.md && \rm -rf /tmp/ta
  ```
- 🚫 不要在本機**直接編** `index.html` — 改了也送不上 GitHub，下次重抓會被覆蓋

---

## 5. 已知待修 TODO

- [ ] **本機補上 `.git/`**。`gh repo clone` 到另一個目錄，或在當前目錄 `git init` + `git remote add origin git@github.com:TYJ2025/Trademark-Advisor.git` + `git fetch` + `git reset --hard origin/main`，這樣以後本機就能 commit + push。
- [ ] 沒做就維持「GitHub canonical / 本機 snapshot」模式，記住每次想看新功能要重抓。
- [ ] `archive/*.bak` 可定期清掉（如果確認 GitHub history 已涵蓋舊內容）。

---

_Last updated: 2026-05-24 by Claude（修正先前對 stale-index 的誤判：實際是本機 stale, GitHub 才是 canonical）_
