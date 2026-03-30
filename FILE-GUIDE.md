# 工作檔案分工

## 檔案結構

| 檔案 | 用途 | 內容 |
|------|------|------|
| `AGENTS.md` | 代理工作準則 | 工作流程、CLI 語法、關鍵字、簡要發現 |
| `spam-patterns.md` | 完整 pattern 分析 | 各年 spam 詳細分析、攻擊手法分類 |
| `spam-repo-list.md` | spam repo 清單 | 所有發現的 spam repos 列表 |
| `gh-api-syntax.md` | 語法參考 | gh CLI 正確語法、易錯語法提醒 |

---

## 各檔案詳細內容

### AGENTS.md
**用途**：代理的工作準則，快速查閱

**內容**：
- 工作目標
- 工具使用（gh CLI, WebFetch）
- CLI 語法快速範例（引用 gh-api-syntax.md）
- 重要技巧（識別真假 spam、驗證步驟）
- 發現的 spam pattern（簡要）
- 工作流程
- 網頁版完整搜尋語法

---

### spam-patterns.md
**用途**：完整分析 spam pattern

**內容**：
- 各年份 spam 概述
- 2026 spam 攻擊手法分類：
  - 銀商/代理/彩票
  - 技術文章偽裝（寶塔面板、plotly error）
  - 家電售后服務偽裝
  - X分钟了解-XXX-第一财经
  - 皇冠信用盘
  - 極速賽車/澳洲幸運10
  - 2026年第一指南-XXX
- 非 2026 spam（2023/2024/2025）
- 數量估算總結
- 更新時間

---

### spam-repo-list.md
**用途**：追蹤所有發現的 spam repos

**內容**：
- 2026 Spam（按數量分級）：
  - 超大型（5000+ issues）
  - 大型（2000-5000 issues）
  - 中型（500-2000 issues）
  - 小型（<500 issues）
  - 技術項目名稱 Spam
  - 寶塔面板 Spam
  - 家電售后服務 Spam
- 非 2026 Spam（2023/2024/2025）
- 每個 repo 欄位：
  - Repo 名稱
  - 建立時間
  - Issues 數量
  - Report 日期（用戶填寫）
- 數量統計
- 更新時間

---

### gh-api-syntax.md
**用途**：gh CLI 正確語法參考

**內容**：
- 日期查詢語法（CLI）
- gh api 查詢 repo/user 資訊
- gh search issues 注意事項
- 網頁版 vs CLI 語法差異
- 實用查詢範例

---

## 更新時機

| 情況 | 更新檔案 |
|------|----------|
| 發現新 spam pattern | `spam-patterns.md` |
| 發現新 spam repo | `spam-repo-list.md` |
| 確認 spam repo 數量增加 | `spam-repo-list.md` |
| 確認 repo 被刪除 | `spam-repo-list.md` |
| 用戶 report 完成 | `spam-repo-list.md`（填寫 Report 日期） |
| 學習到新 CLI 語法 | `gh-api-syntax.md` |
| 工作流程更新 | `AGENTS.md` |

---

## 驗證流程

1. 發現可疑 spam → 檢查 repo 建立時間
2. 確認是 spam → 記錄到 spam-repo-list.md
3. 用戶 report → 更新 Report 日期欄位
4. 定時 validate → 確認 repo 存在、數量更新
