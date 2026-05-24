# CLAUDE.md — Trademark Advisor

> 給下一個 Claude session 的快速上手文件。30 秒內知道這是什麼、檔案在哪、怎麼編、紅線是什麼。

---

## 1. 專案是什麼

單檔 HTML 的 trademark 佈局策略顧問工具（中文 UI，繁體）。匯入 trademark portfolio 後產出策略分析與建議，內建 DEMO_DATA（糖村 Sugar & Spice 公開資料）作為展示。

- **線上**：https://tyj2025.github.io/Trademark-Advisor/（**public** GitHub Pages，服務 `index.html`）
- **Repo**：https://github.com/TYJ2025/Trademark-Advisor (public)
- **本機 working tree**：`~/ClaudeProjects/Trademark Advisor/`，已掛上 `origin/main`，可雙向 pull/push

---

## 2. 檔案結構

```
Trademark Advisor/
├── index.html              ~103 KB ← 主程式（CSS / JS 全內嵌單檔）
├── README.md
├── CLAUDE.md               ← 本檔
├── .gitignore
└── archive/                ← 2026-05-24 sync 之前的本機古早 snapshot（gitignored，本機 only）
```

---

## 3. 怎麼用

```bash
cd "$HOME/ClaudeProjects/Trademark Advisor"

open index.html         # 本機在瀏覽器看

git pull                # 從 remote 取最新（別處編完才需要）
# 編輯 index.html ...
git add -A && git commit -m "msg" && git push   # 推上 GitHub，GH Pages 自動部署
```

---

## 4. 紅線

- ❌ **不要直接編 `archive/` 下的舊 snapshot** — 那是 2026-04-16 的歷史備份，不會被部署，誤改沒意義。
- ❌ **不要在 `index.html` 內嵌 API key / token** — 這是 public repo + public GH Pages。
- ❌ **不要把這個 repo 搬進 iCloud Drive** — `.git/` 會被 `bird` daemon 鎖住。
- ⚠️ **本機與 remote 平時應該對齊**。長時間沒 `git pull` 就動手會出現衝突（2026-05-24 之前就是因為本機長期跟 remote 脫鉤、後來才重建 git tracking — 別再走回頭路）。

---

## 5. 部署

GitHub Actions 自動跑 `pages-build-deployment`，push 到 `main` 後通常 30~60 秒線上版更新。要驗證：

```bash
gh run list --repo TYJ2025/Trademark-Advisor --limit 3
curl -sI "https://tyj2025.github.io/Trademark-Advisor/" | head -3
```

CDN cache 約 5–10 分鐘可能還看到舊版，cache-bust 用 `?cb=$(date +%s)`。

---

## 6. 已知待修 TODO

- [x] ~~本機補上 `.git/` 讓本機能編能推~~ — 2026-05-24 完成（git init + remote + reset --hard origin/main）。
- [ ] `archive/*.bak` 古早 snapshot 可定期清掉（確認 GitHub history 已涵蓋舊內容後）。
- [ ] 沒有自動測試 / lint。改 `index.html` 後只能手測（demo data 跑一遍）。

---

_Last updated: 2026-05-24 by Claude（本機升級為 working tree 後同步更新）_
