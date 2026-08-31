# 聲揚聯合治療所 — 官網六版本（完整實際內容）

內容與照片全部取自官網 https://www.soundyoung.com.tw/ （擷取日期 2026-08-31），**沒有任何佔位或示意文字**。

線上 demo：https://bartester1.github.io/soundyoung-website/

## 六個版本

| 資料夾 | 風格 | 主色 | 字體 |
|---|---|---|---|
| `soundyoung-b` | 清新自然・森林系 | 鼠尾草綠＋奶油白＋杏色 | Noto Sans TC |
| `soundyoung-c` | 明亮親子・繪本風 | 天空藍＋鵝黃（粗框貼紙感） | Huninn 粉圓體＋Noto Sans TC |
| `soundyoung-d` | 沉穩專業・質感診所 | 深藍灰＋暖米＋金線 | Noto Serif TC 明體＋Noto Sans TC |
| `soundyoung-e` | 暖陽奶油・日系柔和 | 奶油白＋杏桃橘＋灰綠（無框、大量留白） | LXGW WenKai TC 楷體＋Noto Sans TC |
| `soundyoung-f` | 現代明快・大字排版 | 近黑＋珊瑚橘＋鵝黃（高對比、方正邊角） | Noto Sans TC 900 |
| `soundyoung-g` | 薰衣草薄荷・有機圓弧 | 薰衣草紫＋薄荷綠＋杏橘（不對稱圓角、無直角） | Noto Sans TC＋Zen Maru Gothic（拉丁字） |

六版**頁面結構與文字內容完全相同**，只有 `assets/style.css` 不同。挑一個資料夾整包上傳即可上線。
全部為靜態 HTML／CSS，無框架、無建置工具、**無動畫**，桌機與手機 RWD 都已實測。

## 每版包含 15 頁

| 檔案 | 內容 |
|---|---|
| `index.html` | 首頁：官網橫幅、發展遲緩說明、三大服務、關於聲揚、課程收費、最新消息、院區資訊 |
| `team.html` | 治療團隊：**10 位治療師實際照片**、姓名、學歷、工作經歷、證照、專長 |
| `environment.html` | 環境介紹：**14 張治療所實景照片** |
| `cooperate.html` | 合作單位：**6 個實際單位標誌與名稱** |
| `course.html` | 課程與收費：實際價格（1500／1200 元） |
| `speech.html` | 語言治療：服務說明＋**7 項居家語言刺激策略表**＋6 位語言治療師 |
| `ot.html` | 職能治療：5 個常見情境＋6 項服務內容＋4 位職能治療師 |
| `articles.html` | 文章列表（5 篇） |
| `article-1~5.html` | 5 篇實際文章全文 |
| `news.html` | 消息公告《我們進化囉》全文 |
| `contact.html` | 聯絡我們：電話、LINE、FB、IG、E-mail、診療時間、雙院區地圖 |

另含 `robots.txt`、`sitemap.xml`、`assets/img/`（38 張實際照片）。

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

在任一版本資料夾內執行，然後開 http://localhost:8000

```bash
python -m http.server 8000
```

## 上線部署（免費雲端代管，不用買主機）

### 方案一：Cloudflare Pages（推薦，台灣連線快）

1. 到 https://dash.cloudflare.com 註冊帳號
2. Workers & Pages → Create → Pages → **Upload assets**，把選定版本資料夾的內容整包拖上去
3. 部署後會得到 `xxx.pages.dev` 網址，先確認顯示正常
4. 網域：`.com` 可直接在 Cloudflare Registrar 註冊（成本價約 USD $10/年）；`.com.tw` 需向台灣註冊商（PChome、Gandi）購買，再把 DNS 指向 Cloudflare
5. Pages 專案 → Custom domains → 加入網域，照指示設 CNAME，SSL 憑證自動配發

### 方案二：GitHub Pages

1. 建一個 GitHub repo，把選定版本資料夾的**內容**（`index.html` 要在 repo 根目錄）push 上去
2. Settings → Pages → Source 選 `main` → 得到 `帳號.github.io/repo名`
3. 自訂網域：Settings → Pages → Custom domain 填入網域，並到網域商後台設定
   - `www` CNAME → `帳號.github.io`
   - 根網域 A 記錄 → 185.199.108.153 / 185.199.109.153 / 185.199.110.153 / 185.199.111.153
4. 勾選 Enforce HTTPS

### 換網域後要改的兩個檔案

若新網址不是 `www.soundyoung.com.tw`，請把 `sitemap.xml` 與 `robots.txt` 內的網域一併換掉。

## 日後維護

改哪一頁就編輯那個 `.html`（全站樣式集中在 `assets/style.css`），存檔後重新上傳（或 `git push`）即可。

新增文章：複製 `article-5.html` 改成 `article-6.html`，再到 `articles.html` 列表加一張卡片，並在 `sitemap.xml` 加一行。

新增／更換照片：把圖片放進 `assets/img/`，再修改對應頁面的 `<img src="assets/img/檔名">`。
