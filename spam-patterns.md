# GitHub Spam Issue Pattern 研究

## 概述
這是一個大規模的 GitHub Issues Spam 攻擊，主要推銷賭博平台。

---

## 一、核心關鍵字 Pattern

### 1. 主管開戶類（最高頻）
```
主管开户
开户
```
Examples:
- `耀世主管开户`
- `杏彩主管`
- `意昂开户`
- `长运开户`

### 2. ２０２６ 與 "第一" 組合
```
２０２６第一
２０２６彩民
2026第一
2026彩民
```
Examples:
- `２０２６第一科普：xxx`
- `２０２６彩民热搜：xxx`
- `２０２６年度盘点：xxx`
- `第一人物-xxx主管`

### 3. 娛樂平台名
```
娱乐平台
娱乐主管
娱乐注册
```
Examples:
- `星欧娱乐平台`
- `门徒娱乐平台`
- `高德娱乐平台`

### 4. 賭博遊戲相關
```
澳洲幸运10
电子pg / PG电子 / pg电子
星力
棋牌
百家乐 / 百家家乐
炸金花
澳门赌场
芒果体育
```
Examples:
- `澳洲幸运10登录`
- `PG电子赏金女王`
- `pg电子赌博`
- `星力十代`
- `百家家乐`
- `澳门赌场`
- `芒果体育平台`

### 5. 銀商/上下分（賭博貨幣兌換）
```
银商
上分
下分
游戏上分
充值上分
91y
集结号
集结号91y
```
Examples:
- `９１ｙ信誉银商`
- `星力游戏上下分`
- `91y上分微信`
- `集结号银商`
- `集结号上下分`

### 6. 特殊格式 ID
```
——422463——
「『扣』——422463——」
```

### 7. 其他常見詞
```
信誉第一
网投信誉
娱乐
平台注册
代理
总代
优惠
返水
足球
平台
赢
芒果棋牌
c7
188BET
kaiyun
BET9
```
Examples:
- `网投第一信誉`
- `c7.c7.ccm登录入口`
- `kaiyun登录入口`

### 8. 《资讯》格式（2023年）
```
《资讯》
-2023
AG真人
真人AG
bg真人
```

### 9. 彩票/投注相關（2026新）
```
买球
世界杯买球
赛车
极速赛车
快3
一分快3
3分快3
```
Examples:
- `买球世界杯买球`
- `极速赛车精准计划网`
- `快3带赚包赔快3导师`

### 10. 加拿大赛车/PC28（2026新）
```
加拿大28
pc28
pk10
```
Examples:
- `加拿大28pc信誉群`
- `pk10微信群`

### 11. 一肖一码/香港彩票（2026新）
```
一肖一码
白小姐
香港一肖一码
精准四肖
```
Examples:
- `一肖一码澳门一肖`
- `白小姐一码一肖中特`

---

## 二、標題 Pattern 結構

### Pattern 1: 年份 + 彩民/第一 + 內容
```
２０２６彩民看点：[平台名]
２０２６第一科普：[平台名]
２０２６彩民热搜：[平台名]
```

### Pattern 2: 第一 + 動作 + 平台
```
第一人物-[平台名]主管
第一科普-[平台名]娱乐
分析第一-[平台名]
```

### Pattern 3: 年代數字 + 年第一指南
```
2024年第一指南-[內容]
2025年第一指南-[內容]
2026年第一指南-[內容]
2027年第一指南-[內容]
2028年第一指南-[內容]
2029年第一指南-[內容]
```
（未來年份，濫用）

### Pattern 4: 《资讯》+ 內容（2023年）
```
《资讯》AG真人龙虎怎么下载玩-2023"xxx"(今日/更新）
《资讯》AG真人公司-2023"xxx"(今日/更新）
```

---

## 三、Body Content Pattern

### 典型 Spam Body（來源：womap3/6yjlo）
```
分析第一:√意昂体育怎么做√【QQ:630002】意昂体育怎么做【官网 22bc點cn】
意昂体育怎么做【QQ:630002】意昂体育怎么做【官网 22bc點cn】【主管总代:万三】【信誉第一】

<img src="https://foruda.gitee.com/images/xxx.png" /> (多次重複)

[偽造的技術文章內容...]

開發一個小程式以生成500篇文章...
```

### Body 關鍵字：
- `QQ:630002`（QQ號碼）
- `官網 xxx點cn`（網址）
- `主管总代:万三`（代理資訊）
- `foruda.gitee.com`（圖床）
- 大量重複圖片

---

## 四、Spam Repo Pattern

### Repo 名稱特徵
- 5-6個隨機字母數字：`womap3`, `6yjlo`, `xol1p`, `22gz9`, `gdrzb`
- 或簡短隨機：`a`, `g`, `oimxa`, `acc61`

### Repo 建立時間
- 集中在 2026-03-28 / 2026-03-29（攻擊日期）

### Repo 建立者
- 看似隨機的用戶名：`womap3`, `crib5bull`, `allisongae`, `limbosbank`

---

## 五、擴展搜尋語法（網頁版 OR）

```
("主管开户" OR "开户" OR "２０２６第一" OR "２０２６彩民" OR "2026第一" OR "2026彩民" OR "——422463——" OR "彩民" OR "娱乐平台" OR "娱乐主管" OR "娱乐注册" OR "澳洲幸运10" OR "电子pg" OR "PG电子" OR "pg电子" OR "星力十代" OR "星力游戏" OR "91y" OR "银商" OR "上分" OR "下分" OR "游戏上分" OR "信誉第一" OR "网投信誉" OR "代理" OR "总代" OR "AG真人" OR "真人AG" OR "百家乐" OR "百家家乐" OR "炸金花" OR "澳门赌场" OR "棋牌游戏" OR "彩票平台" OR "平台代理" OR "返水" OR "《资讯》" OR "永恒娱乐" OR "赢咖" OR "开户" OR "芒果体育" OR "芒果棋牌" OR "c7" OR "188BET" OR "kaiyun" OR "BET9" OR "买球" OR "世界杯买球" OR "赛车" OR "极速赛车" OR "快3" OR "加拿大28" OR "pc28" OR "pk10" OR "一肖一码" OR "白小姐" OR "集结号")
```

---

## 六、單一關鍵字搜尋（CLI）

```bash
gh search issues '主管开户'
gh search issues '２０２６第一'
gh search issues '——422463——'
gh search issues '彩民'
gh search issues '娱乐平台'
gh search issues '澳洲幸运10'
gh search issues '星力'
gh search issues '91y'
gh search issues '电子pg'
gh search issues 'pg电子'
gh search issues '银商'
gh search issues '百家乐'
gh search issues '百家家乐'
gh search issues '炸金花'
gh search issues '澳门赌场'
gh search issues '棋牌游戏'
gh search issues '彩票平台'
gh search issues '代理'
gh search issues '《资讯》'
gh search issues 'AG真人'
gh search issues '开户'
gh search issues '芒果体育'
gh search issues '芒果棋牌'
gh search issues 'c7'
gh search issues '188BET'
gh search issues 'kaiyun'
gh search issues 'BET9'
gh search issues '买球'
gh search issues '世界杯买球'
gh search issues '赛车'
gh search issues '极速赛车'
gh search issues '快3'
gh search issues '加拿大28'
gh search issues 'pc28'
gh search issues 'pk10'
gh search issues '一肖一码'
gh search issues '白小姐'
gh search issues '集结号'
```

---

## 七、已識別的 Spam 相關平台

### 娛樂/賭博平台名（部分）
- 意昂 / 意昂3 / 意昂体育
- 杏彩 / 杏悦2
- 星力 / 星力十代
- 91y
- 耀世
- 门徒
- 高德
- 天狮
- 摩杰
- 汇赢
- 长运
- 摩根
- 赢咖
- 焦点
- 恒行6
- 富联
- 蓝图
- 天辰
- 益达
- 天九
- 盛煌
- 卧龙
- 申博
- 新宝
- 欧陆
- 恒盛
- c7 / c7.ccm
- 188BET
- kaiyun
- BET9 / BET9九卅娱乐
- 芒果体育 / 芒果棋牌
- 集结号
- 银河999
- 加拿大28 / pc28
- pk10

---

## 八、歷史 Spam Pattern

### 2025 Spam Pattern
標題關鍵字：`2025彩民`、`彩票导师`、`加导师彩票赚钱`

### 2024 Spam Pattern
少量 spam，關鍵字與 2025 類似

### 2023 Spam Pattern
```
《资讯》AG真人龙虎怎么下载玩-2023"xxx"(今日/更新）
《资讯》AG真人公司-2023"xxx"(今日/更新）
```
關鍵字：`AG真人`、`《资讯》`、`-2023`（年份後綴）
手法：域名搶注（如 `baidu.com` 作為 repo 名稱）

---

## 九、域名搶注 Spam Repo 搜尋

### 常見被搶注域名（無 spam issues）
```
qq.com / 163.com / taobao.com
```
這些域名有大量 squatting repos，但無 spam issues。

```bash
gh search repos 'baidu.com in:repo'
```

---

## 十、2026 Spam（當前大規模攻擊）

### 2026-03-30 大規模攻擊特徵
- 攻擊時間：多個 repos 同時建立（08:19）
- Repo 名稱：隨機字母數字或看似正常的單字
- 使用大量不同用戶帳號建立 repos

### 攻擊者使用的 repo 名稱 pattern
- 5-6個隨機字母數字：`huzhangh2010`, `lucavieidev`
- 看似正常的單字：`thedardney`, `janceswl`, `octnihb`
- 隨機用戶名統一建立大量 repos

### 2026 Spam 數量估算
- 非 2026 Spam（歷史累積）：~11,000 issues
- 2026 Spam（持續變化）：15萬+ issues

---

## 更新時間
2026-04-01：新增 c7, 188BET, kaiyun, 芒果体育, 集结号, 信誉第一, 买球, 赛车, 快3, 加拿大28/pc28, 一肖一码/白小姐 patterns
