# 聲揚聯合治療所 — 官網改版

內容與照片取自官網 https://www.soundyoung.com.tw/ （擷取日期 2026-08-31），**沒有任何佔位或示意文字**。

線上 demo：https://bartester1.github.io/soundyoung-website/soundyoung-b/

## 版本

只保留 **`soundyoung-b`｜清新自然・森林系**（鼠尾草綠＋奶油白＋杏色，Noto Sans TC）。
先前並列比較的 C～G 五個版本已於 2026-09-02 移除，內容仍保留在 git 歷史中。

根目錄的 `index.html` 只是導向 `soundyoung-b/` 的跳轉頁。

靜態 HTML／CSS，**無框架、無建置工具、無 JavaScript 函式庫、無動畫**，全站樣式集中在 `assets/style.css`（約 300 行）。

## 頁面（16 頁）

| 檔案 | 內容 |
|---|---|
| `index.html` | 首頁：主視覺、三大服務、治療團隊、關於聲揚、課程收費、發展遲緩說明、最新消息、院區資訊 |
| `team.html` | 治療團隊：10 位治療師照片、學歷、工作經歷、證照、專長 |
| `environment.html` | 環境介紹：14 張治療所實景照片 |
| `cooperate.html` | 合作單位：6 個實際單位（含兒童通報轉介中心聯絡方式） |
| `course.html` | 課程與收費：初次評估 0 元、實際價格、早療補助說明（`#subsidy`） |
| `speech.html` | 語言治療：服務說明＋7 項居家語言刺激策略表 |
| `ot.html` | 職能治療：5 個常見情境＋6 項服務內容 |
| `articles.html` | 文章列表（5 篇） |
| `article-1~5.html` | 5 篇實際文章全文，各含文末轉換區塊 |
| `news.html` | 消息公告《我們進化囉》全文 |
| `contact.html` | 聯絡我們：預約流程、聯絡方式、雙院區嵌入地圖 |
| `404.html` | 找不到頁面（noindex；需 B 版內容位於站台根目錄才會生效） |

另含 `robots.txt`、`sitemap.xml`、`assets/img/`（44 個檔案）。

## 已完成的品質基準

- **無障礙**：16 頁完整標題階層、`lang`、全 `alt`、全語意連結名稱、skip link（WCAG 2.4.1 Level A）、允許縮放、目標尺寸 48–56px（超過 2.5.5 AAA）
- **對比**：全站配色實測通過 WCAG 2.1 AA（4.5:1）。LINE 按鈕保留品牌亮綠 `#06C755`，文字用 `#0B2E16`（6.57:1）
- **SEO**：每頁 canonical、meta description、og 五件套、Twitter card；`MedicalClinic` JSON-LD ×2、`BreadcrumbList` ×14
- **效能**：首頁 8 個請求；圖庫 2,370 KB（長邊上限 1000px、q82 progressive）；主視覺用 `srcset` 提供 600／900／1400 三種寬度

## 治療團隊（頁面實際收錄）

**語言治療**：董沛佳（所長）、孫慧心、陳亮嘉、劉芳瑜、劉芳岑、梁朝崴
**職能治療**：劉燕（副所長）、陳韻雯、謝明潔、沈芸嫺

## 診所資訊

- 電話 0910-071-370（採預約制）
- 診療時間：星期一～星期六 9:00～21:00
- E-mail：soundyoung351@gmail.com
- LINE：@322vxncz
- 聲揚聯合治療所：苗栗縣頭份市維新路 26 號（品未來 3 社區）
- 聲禾語言治療所：苗栗縣頭份市富強一街 59 號

## 本機預覽

在 repo 根目錄執行，然後開 http://localhost:8000/soundyoung-b/

```bash
python -m http.server 8000
```

## 上線部署

### 方案一：Cloudflare Pages（推薦，台灣連線快，且可設 301 轉址）

1. 到 https://dash.cloudflare.com 註冊帳號
2. Workers & Pages → Create → Pages → **Upload assets**，把 `soundyoung-b` 資料夾的**內容**整包拖上去（`index.html` 要在根）
3. 部署後會得到 `xxx.pages.dev` 網址，先確認顯示正常
4. 網域：`.com` 可直接在 Cloudflare Registrar 註冊；`.com.tw` 需向台灣註冊商購買再把 DNS 指向 Cloudflare
5. Pages 專案 → Custom domains → 加入網域，照指示設 CNAME，SSL 憑證自動配發

### 方案二：GitHub Pages

1. 把 `soundyoung-b` 的**內容**放到 repo 根目錄（`index.html` 要在根，`404.html` 才會生效）
2. Settings → Pages → Source 選 `main`
3. 自訂網域：Settings → Pages → Custom domain 填入網域，並到網域商後台設定 `www` CNAME 與根網域 A 記錄（IP 以 GitHub 文件公告為準）
4. 勾選 Enforce HTTPS

## 換網域時要做的事

網域字串目前在 HTML 的 canonical／og／JSON-LD、`sitemap.xml`、`robots.txt` 共出現 116 處，全部一致，一次取代即可：

```bash
grep -rl "https://www.soundyoung.com.tw" soundyoung-b/ | xargs sed -i "s|https://www.soundyoung.com.tw|https://新網域|g"
```

### 若要取代現行正式站

舊站有 9 個網址在 B 版改了檔名（`pics-list-1`→`environment`、`contents-1`→`articles`、`contents-2`→`news`、`yuyanz`→`speech`、`zhinengz`→`ot`、`content-4/8/9/10`→`article-N`），需要 301 轉址。GitHub Pages 發不了 301，建議走 Cloudflare Pages 或在前面掛 Cloudflare。

## 分析追蹤

已掛 GA4，沿用治療所既有 property `G-Y2758WWD33`（與原站同一組，取代原站後資料連續）。
除了預設的頁面瀏覽，另有兩個自訂事件：

| 事件 | 觸發 | 參數 |
|---|---|---|
| `contact_phone` | 點擊任何 `tel:` 連結 | `link_url`、`page_path` |
| `contact_line` | 點擊任何 line.me 連結 | `link_url`、`page_path` |

兩個事件需在 GA4 後台設為「關鍵事件」才會進轉換報表。

## 不實作的項目

- **線上預約表單**：治療所只走電話與 LINE，不採用表單（營運選擇）
- **FAQ**：治療所沒有制式規定（要帶什麼、改期規則等），資訊不存在

## 日後維護

改哪一頁就編輯那個 `.html`（全站樣式集中在 `assets/style.css`），存檔後 `git push` 即可。

新增文章：複製 `article-5.html` 改成 `article-6.html`，再到 `articles.html` 列表加一張卡片，並在 `sitemap.xml` 加一行。

新增／更換照片：把圖片放進 `assets/img/`，再修改對應頁面的 `<img src="assets/img/檔名">`。新圖請先縮到長邊 1000px 以內。
