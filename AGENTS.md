# GitHub Spam Investigation Work Pattern

## 目標
分析 GitHub Issues 賭博spam攻擊的 pattern

## 工具
- `gh` CLI - GitHub 命令列工具
- WebFetch - 抓取網頁版搜尋結果

## CLI 語法參考
**重要**：正確語法請參考 `gh-api-syntax.md`

### 查詢 repo 資訊（確認是否真的老spam）
```bash
# 確認 repo 建立時間和 issue 數量
gh api repos/USER/REPO --jq '{name: .name, created: .created_at, open_issues: .open_issues_count}'
```

### 搜尋特定日期的 spam
```bash
# 查詢 2025 年 spam
gh search issues '彩票导师 --created 2025-01-01..2025-12-31' --limit 100

# 查詢 2023-2024 年 spam
gh search issues 'AG真人 --created 2023-01-01..2024-12-31' --limit 100

# 查詢最新 spam（2026-03-30 以後）
gh search issues 'created:2026-03-30' --limit 100 --sort created
```

### 查詢 user 資訊（注意 endpoint）
```bash
# 正確：用 users 而非 repos
gh api users/USERNAME --jq '{login: .login, created: .created_at}'
```

## 重要技巧

### 識別真假老 spam
標題含年份（如 `2025彩民指南`）**不代表**是老 spam！
- **關鍵**：用 `gh api repos/USER/REPO --jq '.created_at'` 確認 repo 真正建立時間
- **假老 spam**：`jy2886-2/ygi0v` (2026-03-28) 但標題是 `2024年第一指南`、`2025年第一指南`
- **真老 spam**：`lilladezman-boop/y7vk53iv` (2025-08-06) 且標題確實是 `2025彩民...`

### 驗證步驟
1. 發現可疑 spam repo → 2. 檢查 `gh api repos/USER/REPO --jq '.created_at'` → 3. 確認建立時間 → 4. 記錄到 spam-repo-list.md

### 驗證 repo 是否仍存在
```bash
gh api repos/USER/REPO --jq '.name' 2>/dev/null || echo "DELETED"
```

## 發現的 Spam Pattern

### 2026 Spam（當前大規模攻擊）

#### 主要關鍵字
```
主管开户
开户
彩民
娱乐
澳洲幸运10
星力
AG真人
百家乐
百家家乐
炸金花
澳门赌场
银商
上分
下分
91y
彩票
棋牌
代理
总代
返水
信誉
耀世
门徒娱乐
皇冠信用盘
```

#### 2026 新 spam 標題 pattern
```
# X分钟了解-XXX-第一财经
X分钟了解-168财神捕鱼-第一财经
X分钟了解-PG电子招财喵-第一财经

# ２０２６年第一指南-XXX
２０２6年第一指南-体育平台
２０２6年第一指南-PG电子
２０２6年第一指南-AG真人

# 皇冠信用盘出租
皇冠信用盘代理开户
皇冠登0123系统出租

# 技術項目名稱偽裝（大量同時發布）
Vite-React-TS-Boilerplate
Diffusion-Model-FineTune
SpringMVC 核心原理讲解
宝塔面板如何修改管理员邮箱

# 銀商/極速賽車
91y银商
极速赛车qq群
澳洲幸运10微信群
```

#### 2026 代表 spam repo
| Repo |  Issues 數量 |
|------|-------------|
| `rluchik1/o` | 10,000+ |
| `allisongae/oimxa` | 4,000+ |
| `womansalad/pztlg` | 4,000+ |
| `noumarageue/5xhk7` | 2,983 |
| `jy2886-2/ygi0v` | 2,958 |

### 2025 Spam
- 關鍵字：`2025彩民`、`彩票导师`
- 代表 repo：`lilladezman-boop/y7vk53iv`（5,209 issues）

### 2024 Spam
- 少量 spam
- 代表 repo：`8brdh7uf/hahaha`（300 issues）

### 2023 Spam（域名搶注）
- 關鍵字：`《资讯》`、`AG真人`、`-2023`
- 手法：域名搶注（如 `rthrsd/baidu.com`）
- 代表 repo：`rthrsd/baidu.com`（990 issues）

## 工作流程

### 發現新 spam 的方法
1. **搜尋特定日期**：`gh search issues 'created:2026-03-30' --limit 100 --sort created`
2. **檢查 issue 數量異常的 repo**：數量突然增加的 repo
3. **驗證 repo 建立時間**：確認是否為新攻擊
4. **更新 spam-repo-list.md**：記錄新發現的 spam repo

### 驗證並更新清單
1. 發現可疑 repo → 2. `gh api repos/USER/REPO --jq '{...}'` → 3. 記錄到 spam-repo-list.md → 4. 如已 report，填寫 report 日期

### 批次尋找新 spam repos（2026-03-30 為例）
```bash
# 1. 列出特定日期的所有 unique repos
gh search issues 'created:2026-03-30' --limit 500 --sort created | \
  grep -E '^[a-z0-9-]+/[a-z0-9]+' | awk '{print $1}' | sort -u

# 2. 過濾高 issue 數量的可疑 repos
gh search issues 'created:2026-03-30' --limit 500 --sort created | \
  grep -E '^[a-z0-9-]+/[a-z0-9]+' | awk '{if ($2 > 100) print}' | head -30

# 3. 批次驗證 repos（檢查建立時間和 issue 數量）
for repo in repo1 repo2 repo3; do
  info=$(gh api repos/$repo --jq '{created: .created_at, issues: .open_issues_count}' 2>/dev/null)
  echo "$repo: $info"
done

# 4. 檢查 issue 標題確認是否為 spam
gh api repos/USER/REPO/issues --jq '.[0:3] | .[].title'
```

### 識別技術名稱偽裝 spam
技術專案名稱 spam 的共同特徵：
- Repo 名稱：隨機字元組合（如 `khanvgpalle/ubov0`、`kwonghugo/o8629`）
- Issue 內容：賭博關鍵字隱藏在技術標題中
- 同時間大量出現（同一分鐘建立）
```bash
# 搜尋技術名稱偽裝 spam
gh search issues 'created:2026-03-30' --limit 500 --sort created | \
  grep -E '(Vite|React|Spring|LangChain|Docker|Gatsby|Nuxt)' | head -20
```

### Git 工作流程
```bash
# 初始化（首次）
git init -b main
git add -A
git commit -m 'Initial commit'
git remote add origin https://git.xlion.tw/xlionjuan/gh-spam.git
git push -u origin main

# 更新後推送
git add -A
git commit -m 'Update: add new spam repos found'
git push
```

**Forgejo Push 注意**：此專案托管於 Forgejo (`git.xlion.tw`)，偶爾會出現認證錯誤。若 push 失敗，重試一次即可成功。

### 提交 GitHub Abuse Report
1. 建立 report 檔案：`github-spam-report-YYYY-MM-DD.md`
2. **Report 格式注意**：不要包含以下欄位：
   - `Report Date:`
   - `Reporter:`
   - `Contact:`
   - `Report ID:`
   - `Generated:`
3. 複製 report 內容到 [GitHub Abuse Form](https://github.com/contact/report-abuse)
4. 或 email 到 abuse@github.com
5. 更新 spam-repo-list.md 中所有相關 repos 的 Report 日期

### 批次更新 Report 日期
```bash
# 將所有空的 Report 欄位填入日期
sed -i '/^|.*| |$/s/| |/| Report: 2026-03-30 |/' spam-repo-list.md

# 或手動指定某幾個 repo（需手動編輯）
```

## 研究檔案
- `spam-patterns.md` - 完整 pattern 分析
- `spam-repo-list.md` - 已被確認的 spam repo 清單（含 report 狀態）
- `gh-api-syntax.md` - Gh CLI 語法參考（重要！易錯語法記錄）

## 網頁版完整搜尋語法
```
("主管开户" OR "开户" OR "彩民" OR "娱乐平台" OR "澳洲幸运10" OR "星力" OR "91y" OR "银商" OR "AG真人" OR "百家乐" OR "百家家乐" OR "炸金花" OR "澳门赌场" OR "彩票平台" OR "棋牌" OR "代理" OR "总代" OR "返水" OR "信誉第一" OR "皇冠信用盘" OR "耀世" OR "门徒娱乐")
```

URL: https://github.com/search?q=%28%22%E4%B8%BB%E7%AE%A1%E5%BC%80%E6%88%B7%22+OR+%22%E5%BC%80%E6%88%B7%22+OR+%22%E5%BD%A9%E6%B0%91%22+OR+%22%E5%A8%B1%E6%A8%82%E5%B9%B3%E5%8F%B0%22+OR+%22%E6%BE%B3%E6%B4%B2%E5%B9%B8%E8%BF%9C10%22+OR+%22%E6%98%9F%E5%8A%9B%22+OR+%2291y%22+OR+%22%E9%93%B6%E5%95%86%22+OR+%22AG%E7%9C%9F%E4%BA%BA%22+OR+%22%E7%99%BE%E5%AE%B6%E4%B9%90%22+OR+%22%E7%99%BE%E5%AE%B6%E5%AE%B6%E4%B9%90%22+OR+%22%E7%82%B8%E9%87%91%E8%8A%B1%22+OR+%22%E6%BE%B3%E5%A4%96%E5%9C%B0%E5%9C%B0%22+OR+%22%E5%BD%A9%E7%90%83%E5%B9%B3%E5%8F%B0%22+OR+%22%E6%A3%8B%E7%89%88%22+OR+%22%E4%BB%A3%E7%90%86%22+OR+%22%E6%80%BB%E4%BB%A3%22+OR+%22%E8%BF%94%E6%B0%B4%22+OR+%22%E4%BF%A1%E8%AA%8D%E7%AC%AC%E4%B8%80%22%29&type=issues
