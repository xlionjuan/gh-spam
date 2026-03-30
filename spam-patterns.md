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
电子pg / PG电子
星力
棋牌
百家乐
百家家乐
炸金花
澳门赌场
```
Examples:
- `澳洲幸运10登录`
- `PG电子赏金女王`
- `星力十代`
- `百家家乐`
- `澳门赌场`

### 5. 銀商/上下分（賭博貨幣兌換）
```
银商
上分
下分
游戏上分
充值上分
```
Examples:
- `９１ｙ信誉银商`
- `星力游戏上下分`
- `91y上分微信`

### 6. 特殊格式 ID
```
——422463——
「『扣』——422463——」
```

### 7. 其他常見詞
```
信誉第一
娱乐
平台注册
代理
总代
优惠
返水
足球
平台
赢
```

### 8. 《资讯》格式（2023年）
```
《资讯》
-2023
AG真人
真人AG
bg真人
```

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
("主管开户" OR "开户" OR "２０２６第一" OR "２０２６彩民" OR "2026第一" OR "2026彩民" OR "——422463——" OR "彩民" OR "娱乐平台" OR "娱乐主管" OR "娱乐注册" OR "澳洲幸运10" OR "电子pg" OR "PG电子" OR "星力十代" OR "星力游戏" OR "91y" OR "银商" OR "上分" OR "下分" OR "游戏上分" OR "信誉第一" OR "代理" OR "总代" OR "AG真人" OR "真人AG" OR "百家乐" OR "百家家乐" OR "炸金花" OR "澳门赌场" OR "棋牌游戏" OR "彩票平台" OR "平台代理" OR "返水" OR "《资讯》" OR "永恒娱乐" OR "赢咖" OR "开户")
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

---

## 八、非 2026 年 Spam（歷史累積）

### 已確認的非 2026 Spam Repo

| Repo | 建立時間 | Issues 數量 | 備註 |
|------|----------|-------------|------|
| `rthrsd/baidu.com` | 2023-01-04 | 990 | 域名搶注，AG真人 spam |
| `dfghau/baidu` | 2023-01-05 | 717 | 域名搶注，AG真人 spam |
| `lilladezman-boop/y7vk53iv` | 2025-08-06 | 5,209 | 彩票 spam |
| `snowladidi-hash/zrbsou18` | 2025-08-06 | 3,795 | 彩票 spam |
| `8brdh7uf/hahaha` | 2024-03-10 | 300 | 彩票 spam |
| `hienquocha-ship-it/j` | 2025-09-25 | 99 | 彩票 spam |
| `hnsts666/-2134563145` | 2025-10-18 | 166 | 赌博 spam |
| `xx248808dfhsy/-Y-HJ0071510` | 2025-06-19 | 44 | 赌博 spam |
| `zlfhlls/-Y-` | 2025-07-13 | 36 | 赌博 spam |
| `flqazlfmmm/HJ0071510` | 2025-06-27 | 13 | 赌博 spam |
| `skdfjhjk455/-Y-` | 2025-07-11 | 4 | 赌博 spam |
| `sluo89170-maker/xs10211.com` | 2025-12-11 | 2 | 赌博 spam |

**非 2026 Spam 總計：約 11,429 issues**

---

### 2025 Spam Pattern

標題關鍵字：`2025彩民`、`彩票导师`、`加导师彩票赚钱`

```
2025彩民指南：彩票导师计划群
2025彩民推荐：导师一对一彩票
2025彩民首选：加导师彩票赚钱
```

---

### 2024 Spam Pattern

發現 `8brdh7uf/hahaha` 等少量 spam repo。

---

### 2023 Spam Pattern
```
《资讯》AG真人龙虎怎么下载玩-2023"xxx"(今日/更新）
《资讯》AG真人公司-2023"xxx"(今日/更新）
《资讯》真人AG是统一开奖吗-2023"xxx"(今日/更新）
```

### 2023 Spam 關鍵字
```
AG真人
真人AG
bg真人
《资讯》
-2023（有年份後綴）
```

### 2023 Spam 手法
- 域名搶注 `baidu.com`、`baidu` 作為 repo 名稱
- 大量建立 AG 真人賭博相關 issues
- 每個 issue 標題含年份 `-2023` 後綴

---

## 九、域名搶注 Spam Repo 搜尋

### 常見被搶注域名（無 spam issues）
```
qq.com
163.com
taobao.com
```
這些域名有大量 squatting repos，但無 spam issues。

### 搜尋方式
```bash
gh search repos 'baidu.com in:repo'
gh search repos 'qq.com in:repo'
```

---

## 十、2026 Spam（當前大規模攻擊）

### 主要 Spam Repo（2026-03-30 更新）

| Repo | 建立時間 | Issues 數量 | 備註 |
|------|----------|-------------|------|
| `rluchik1/o` | 2026-03-21 | 10,451 | **爆增中！** |
| `allisongae/oimxa` | 2026-03-29 | 3,991 | ２０２６年度盘点、２０２６第一科普 |
| `womansalad/pztlg` | 2026-03-29 | 3,917 | |
| `milica64/d1acb` | 2026-03-29 | 2,886 | |
| `agunni/d1l8f` | 2026-03-29 | 2,860 | |
| `noumarageue/5xhk7` | 2026-03-28 | 2,983 | X分钟了解-XXX-第一财经 |
| `jy2886-2/ygi0v` | 2026-03-28 | 2,958 | X分钟了解-XXX-第一财经 |
| `rhoselin/cjrsq` | 2026-03-28 | 2,997 | X分钟了解-XXX-第一财经 |
| `waizou/1uovd` | 2026-03-28 | 2,989 | X分钟了解-XXX-第一财经 |
| `lillianxxbanksh/7` | 2026-03-29 | 2,130 | 皇冠信用盘代理开户 |
| `norma9783-lundy7/o` | 2026-03-29 | 2,130 | 皇冠信用盘代理开户 |
| `julke-541/b` | 2026-03-29 | 2,130 | 皇冠信用盘代理开户 |
| `ervin-smolka346d/k` | 2026-03-29 | 2,130 | 皇冠信用盘代理开户 |
| `clebcourse/s0rpd` | 2026-03-29 | 3,800 | |
| `ln1962/anqbn` | 2026-03-29 | 1,600+ | |
| `shyathsing/drqxv` | 2026-03-29 | 3,122 | |
| `smramy/1cjhc` | 2026-03-29 | 3,086 | |
| `powersandr/x1g62` | 2026-03-29 | 2,437 | |
| `xhizan/6m81n` | 2026-03-29 | 2,469 | |
| `crib5bull/acc61` | 2026-03-29 | 2,453 | |
| `pxcarter/skc3u` | 2026-03-29 | 2,483 | |
| `arebitl/z99tq` | 2026-03-29 | 1,300+ | |
| `lisaunt/wwxeq` | 2026-03-29 | 2,591 | 銀商、極速賽車 |
| `danielfw4willisb/dvdv` | 2026-03-28 | 1,323 | 2026超全指南、2026独家精选 |
| `bbio0118/kggla` | 2026-03-28 | 496 | X分钟了解-XXX-第一财经 |
| `frederick2025-d9/erey7` | 2026-03-28 | 498 | X分钟了解-XXX-第一财经 |
| `noumarageue/tllub` | 2026-03-28 | 496 | X分钟了解-XXX-第一财经 |
| `vinod5li/gdrzb` | 2026-03-28 | 1,100+ | |
| `isaacshirt/lhag4` | 2026-03-28 | 1,000+ | |
| `zemtal/oy5ob` | 2026-03-28 | 1,100+ | |
| `frisacamer/xpe2j` | 2026-03-28 | 1,100+ | |
| `charles-king504e/xt5q0` | 2026-03-28 | 413 | X分钟了解-XXX-第一财经 |
| `rhoselin/w3z4e` | 2026-03-28 | 498 | X分钟了解-XXX-第一财经 |
| `jy2886-2/7w1v6` | 2026-03-28 | 299 | X分钟了解-XXX-第一财经 |
| `llevaner/gmvnh` | 2026-03-28 | 600+ | |
| `shrimp79sk/z57` | 2026-03-29 | 541 | 2026最新XXX、彩票导师 |
| `thedrikes/oo0` | 2026-03-29 | 501 | 2026最新XXX、彩票导师 |
| `gukasydamo/agnzgu` | 2026-03-29 | 500 | 2026独家精选、年度更新 |
| `davidljone/msxtlt` | 2026-03-29 | 500 | 2026独家精选、年度更新 |
| `eleyardone/1p1gg3` | 2026-03-29 | 500 | 2026独家精选、年度更新 |
| `klausdelac/c82ym0` | 2026-03-29 | 500 | 2026独家精选、年度更新 |
| `jimkrudzel/nir3xa` | 2026-03-29 | 500 | 2026独家精选、年度更新 |
| `bsethpwyatt/zb424` | 2026-03-28 | 294 | X分钟了解-XXX-第一财经 |
| `maxsappi/06pcc9` | 2026-03-29 | 423 | 2026全面科普 |
| `ahanhawk/m0jyqf` | 2026-03-29 | 464 | plotly_chart kwargs deprecation warning |
| `womap3/6yjlo` | 2026-03-28 | 336 | 第一人物、第一科普，分析第一 |
| `gmarla/my` | 2026-03-29 | 200 | 隨機字符 spam |
| `gmarla/il` | 2026-03-29 | 141 | 隨機字符 spam |
| `georoconto2030/w72vf` | 2026-03-28 | 140 | 第一人物、第一科普 |
| `bbio0118/g7c9f` | 2026-03-28 | 159 | 隨機字符 spam |
| `ervin-smolka346d/k` | 2026-03-29 | 2,020 | 皇冠信用盘出租 |
| `plushlowski/m88ur` | 2026-03-30 | 388 | 澳洲幸运10 spam |
| `montagrang/588ex` | 2026-03-27 | 1,504 | 彩票 spam |
| `rgrossic/g11iour4` | 2026-03-26 | 418 | 门徒娱乐 spam |
| `iphobiks/757p9` | 2026-03-27 | 2,851 | 门徒娱乐 spam |
| `smithalmed/m2d3p` | 2026-03-27 | 1,200 | 门徒娱乐 spam |
| `danyafordepsdg/j` | 2026-03-29 | 127 | 皇冠信用盘出租 |
| `rjelix/9uj` | 2026-03-30 | 46 | 保管箱 spam |
| `mf3187-6/6dnno` | 2026-03-29 | 1,018 | 技術文章偽裝 spam |
| `maxvivian/o1v0l` | 2026-03-29 | 471 | 91y銀商 spam |
| `bdtrapicom/0` | 2026-03-30 | 173 | 91y銀商 spam |
| `rjelix/04w` | 2026-03-30 | 68 | 保管箱 spam |
| `set43diviny2/8trq` | 2026-03-30 | 93 | 技術文章偽裝 spam |
| `bayjhand/xjbp` | 2026-03-30 | 90 | 技術文章偽裝 spam |
| `khanvgpalle/ubov0` | 2026-03-30 | 24 | 極速賽車 spam |
| `batchero/44h3v` | 2026-03-30 | 84 | 極速賽車 spam |

### 宝塔面板 Spam（2026-03 新發現）

| Repo | 建立時間 | Issues 數量 |
|------|----------|-------------|
| `bgfakefanon/4znbz` | 2026-03-26 | 566 |
| `ranazhalkyi/plw2i` | 2026-03-26 | 567 |
| `yuisikyiu/y8m5y` | 2026-03-26 | 399 |
| `nitagele/xpbij` | 2026-03-26 | 400 |
| `andreiruelrawald/4i2ms` | 2026-03-26 | 388 |
| `sombarwal/a8quw` | 2026-03-26 | 386 |
| `meringioeler/1j6z1` | 2026-03-26 | 335 |
| `adeatfouricl/aedyg` | 2026-03-26 | 250 |
| `friterics/52wdf` | 2026-03-26 | 254 |
| `avilehuk/2sy02` | 2026-03-26 | 239 |
| `eilyey12/b01m8` | 2026-03-27 | 182 |
| `cio-ne/7l7nb` | 2026-03-27 | 181 |
| `drixfeyt/1znx7` | 2026-03-27 | 217 |
| `takestarry/1anoi` | 2026-03-27 | 146 |
| `di-pai-phoo/p9vcv` | 2026-03-27 | 144 |

---

## 十一、數量估算總結

| 類型 | 數量 |
|------|------|
| 非 2026 Spam（歷史累積） | ~11,375 issues |
| 2026 Spam（持續增長） | **15萬+ issues**（大量新 pattern 被發現） |

---

## 更新時間
2026-03-30（大量新 spam pattern 持續發現）
