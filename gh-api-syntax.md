# Gh API 查詢語法參考

## 日期查詢語法（CLI）

### 正確語法
```bash
# 查詢特定年份（正確）
gh search issues '彩票导师 --created 2025-01-01..2025-12-31'

# 查詢特定月份（正確）
gh search issues '主管开户 --created 2026-03-01..2026-03-31'

# 查詢某年之后（正確）
gh search issues '彩民 --created 2025-01-01..'
```

### 錯誤語法（需避免）
```bash
# 錯誤：引號位置錯誤
gh search issues 'created:2025 "彩票导师"'
# 錯誤：ISO 格式不接受 "2025" 作為日期

# 錯誤：created 不支援這種格式
gh search issues 'created:2024..2025 "彩票"'
```

## gh api 查詢 repo/user 資訊

### 查詢 repo 資訊
```bash
# 正確
gh api repos/USER/REPO --jq '{name: .name, created: .created_at, open_issues: .open_issues_count}'

# 注意：USER/REPO 格式，如果 repo 名稱含有 .com 之類的域名也是有效的（如 rthrsd/baidu.com）
```

### 查詢 user 資訊
```bash
# 正確（users endpoint）
gh api users/USERNAME --jq '{login: .login, created: .created_at}'

# 注意：用 repos/USER 會 404，應改用 users/USER
```

## gh search issues 注意事項

### --limit 參數
```bash
# 預設 limit 是 30
gh search issues '關鍵字'
gh search issues '關鍵字' --limit 50
```

### --sort 參數
```bash
gh search issues '關鍵字' --sort created
gh search issues '關鍵字' --sort updated
```

### --match 參數（限制搜尋範圍）
```bash
# 只搜尋標題
gh search issues '關鍵字' --match title

# 只搜尋 body
gh search issues '關鍵字' --match body
```

## 網頁版 vs CLI 語法差異

| 功能 | 網頁版 | CLI |
|------|--------|-----|
| OR 搜尋 | `OR` 關鍵字 | CLI 不支援，需分開搜 |
| 日期範圍 | `created:2025-01-01..2025-12-31` | 同樣語法 |
| 年份查詢 | `created:2025` | 不支援，需用 `created:2025-01-01..` |

## 實用查詢範例

```bash
# 查詢 2025 年的 spam
gh search issues '彩票导师 --created 2025-01-01..2025-12-31' --limit 100

# 查詢特定 repo 的所有 issues
gh search issues 'repo:USER/REPO' --limit 100

# 查詢包含多個關鍵字的 issues
gh search issues '主管开户'
gh search issues '彩民'
gh search issues '信誉第一'
```
