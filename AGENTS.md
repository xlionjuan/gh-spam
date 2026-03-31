# GitHub Spam Investigation Work Pattern

## 目標
分析 GitHub Issues 賭博spam攻擊的 pattern

## 工具
- `gh` CLI - GitHub 命令列工具
- WebFetch - 抓取網頁版搜尋結果

## 檔案架構
| 檔案 | 用途 |
|------|------|
| `spam-repo-list.md` | 維護**仍存在**的 spam repos |
| `deleted-spam-repo-list.md` | 歸檔**已刪除**的 spam repos |
| `github-spam-report-YYYY-MM-DD.md` | 舉報檔案（每個 report 獨立） |
| `gh-api-syntax.md` | Gh CLI 語法參考 |

---

## 工作流程

### 1. 發現新 spam repos
```bash
# 搜尋特定關鍵字（推薦）
gh search issues 'PG電子 --created 2026-03-30' --limit 100
gh search issues '主管开户' --limit 100
gh search issues 'AG真人' --limit 100

# 搜尋特定日期的所有 repos
gh search issues 'created:2026-03-30' --limit 500 --sort created
```

### 2. 驗證並記錄新 repos
```bash
# 批次驗證 repos（檢查建立時間和 issue 數量）
for repo in repo1 repo2 repo3; do
  info=$(gh api repos/$repo --jq '{created: .created_at, issues: .open_issues_count}' 2>/dev/null)
  echo "$repo: $info"
done

# 檢查 issue 標題確認是否為 spam
gh api repos/USER/REPO/issues --jq '.[0:3] | .[].title'
```

### 3. 驗證刪除狀態
```bash
# 檢查 spam-repo-list.md 中所有 repos 是否仍存在
grep -oP '^\| `\K[^`]+' spam-repo-list.md | grep '/' | sort -u > /tmp/list_repos.txt
xargs -P 50 -I {} sh -c 'gh api repos/{} --jq ".name" 2>&1 | grep -q "Not Found" && echo {}' < /tmp/list_repos.txt

# 發現刪除 → 從 spam-repo-list.md 移除，加入 deleted-spam-repo-list.md
```

### 4. 驗證 Report 與 List 一致
```bash
# 確認 report 中 repo 數量
grep -E '^\| `[^`]+` ' github-spam-report-YYYY-MM-DD.md | wc -l

# 確認沒有重複
grep -E '^\| `[^`]+` ' github-spam-report-YYYY-MM-DD.md | awk -F'`' '{print $2}' | sort | uniq -d

# 確認 report repos 都在 list 中
grep -oP '^\| `\K[^`]+' github-spam-report-YYYY-MM-DD.md | while read repo; do
  grep -q "$repo" spam-repo-list.md || echo "MISSING: $repo"
done
```

### 5. 提交 GitHub Abuse Report
1. 建立 report 檔案：`github-spam-report-YYYY-MM-DD.md`
2. **Report 必須獨立**：不應交叉引用其他 report
3. **格式規則**：
   - 不要包含：`Report Date:`, `Reporter:`, `Contact:`, `Report ID:`, `Generated:`
   - 如果某個 size category 沒有 repos，必須刪除該 section，不要留空 header
4. 複製 report 內容到 [GitHub Abuse Form](https://github.com/contact/report-abuse)
5. 更新 spam-repo-list.md 中相關 repos 的 Report 日期

### 6. Git 工作流程
```bash
git add -A
git commit -m 'Update: description'
git push
# 若 push 失敗，重試一次（Forgejo 認證問題）
```

---

## CLI 語法參考
**重要**：詳細語法請參考 `gh-api-syntax.md`

```bash
# 確認 repo 建立時間和 issue 數量
gh api repos/USER/REPO --jq '{name: .name, created: .created_at, open_issues: .open_issues_count}'

# 確認 repo 是否已刪除
gh api repos/USER/REPO --jq '.name' 2>/dev/null || echo "DELETED"

# 查詢 user 資訊（注意：用 users 而非 repos）
gh api users/USERNAME --jq '{login: .login, created: .created_at}'
```

---

## 重要規則

### 識別真假老 spam
標題含年份（如 `2025彩民指南`）**不代表**是老 spam！
- **關鍵**：用 `gh api repos/USER/REPO --jq '.created_at'` 確認 repo 真正建立時間
- **假老 spam**：`jy2886-2/ygi0v` (2026-03-28) 但標題是 `2024年第一指南`
- **真老 spam**：`lilladezman-boop/y7vk53iv` (2025-08-06)

### ⚠️ 嚴禁提前填寫 Report 日期
- 只有已提交 abuse report 的 repos 才能填寫 Report 日期
- 發現新 spam repo 時，Report 欄位留空
- 填寫日期必須是真正完成 report 的日期

---

## 發現的 Spam Pattern

### 2026 Spam（當前大規模攻擊）

#### 主要關鍵字
```
主管开户、开户、彩民、娱乐、澳洲幸运10、星力、AG真人、
百家乐、百家家乐、炸金花、澳门赌场、银商、91y、彩票、
棋牌、代理、总代、返水、信誉、皇冠信用盘、pg电子、PG電子、
c7、188BET、kaiyun、芒果体育、芒果棋牌、集结号、信誉第一、
买球、世界杯买球、赛车、极速赛车、快3、加拿大28、pc28、
一肖一码、白小姐、威尼斯、bbin、倍投、上岸、回血、包赔
```

#### 技術項目名稱偽裝 spam
- Repo 名稱：隨機字元組合（如 `khanvgpalle/ubov0`）
- Issue 內容：賭博關鍵字隱藏在技術標題中
- 同時間大量出現（同一分鐘建立）

#### 2026 Spam 攻擊時間線
- **2026-03-30** 大規模攻擊（多個 repos 同時建立，如 08:19）
- **2026-03-31** 持續攻擊波

#### 大型 spam 類型（2026-03-30）
| 類型 | Issues/Repo |
|------|-------------|
| pg麻将胡了 | ~7,400 |
| ２０２６第一指南/甄选/专栏 | ~8,500-9,600 |
| c7 平台 | ~9,000+ |
| 188BET 平台 | ~8,500-9,500 |
| AG真人 | ~6,200+ |
| 炸金花 | ~6,200+ |
| kaiyun | ~6,200+ |
| 买球 | ~5,000 |
| 芒果棋牌 | ~6,300+ |
| 一肖一码/白小姐 | ~17,000+ |
| 信誉类 | ~43,000+ |

### 2025 Spam
- 關鍵字：`2025彩民`、`彩票导师`

### 2023 Spam（域名搶注）
- 關鍵字：`《资讯》`、`AG真人`、`-2023`
- 手法：域名搶注（如 `baidu.com` 作為 repo 名稱）

---

## 網頁版完整搜尋語法
```
("主管开户" OR "开户" OR "彩民" OR "娱乐平台" OR "澳洲幸运10" OR "星力" OR 
"91y" OR "银商" OR "AG真人" OR "百家乐" OR "百家家乐" OR "炸金花" OR 
"澳门赌场" OR "彩票平台" OR "棋牌" OR "代理" OR "总代" OR "返水" OR 
"信誉第一" OR "皇冠信用盘" OR "耀世" OR "门徒娱乐" OR "pg电子" OR 
"PG电子" OR "c7" OR "188BET" OR "kaiyun" OR "BET9" OR "芒果体育" OR 
"芒果棋牌" OR "集结号" OR "信誉网投" OR "买球" OR "世界杯买球" OR 
"赛车" OR "极速赛车" OR "快3" OR "加拿大28" OR "pc28" OR "pk10" OR 
"一肖一码" OR "白小姐")
```
