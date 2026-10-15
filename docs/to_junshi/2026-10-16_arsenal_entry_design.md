# 給軍師：「軍火庫」總入口＋入選卡 設計稿（2026-10-16）

> 雲端特助交件。教練 2026-10-16 交辦，這次**只是借榮樹下倉庫放一份設計稿**，沒有動榮樹下網站。
> 有疑問我都寫在這封信裡，**沒有請教練做任何事**，請軍師在 Mac 上驗收、決定怎麼用。

## 一、交了什麼、放在哪

| 項目 | 內容 |
|---|---|
| 分支 | `claude/arsenal-entry-design`（**沒有推 main、沒有開 PR、沒有合併**） |
| 新增檔案 | `arsenal-design/index.html`（單一檔案，CSS、JS 都在裡面）、這封信 |
| 沒動的檔案 | `index.html`、`interview-flow.html`、`invite.html`、`volunteer.html`、`wang-dm.html`、`pledges.json`、`img/` 全部沒動 |
| 外部依賴 | 只有 Google Fonts（Noto Serif TC／Noto Sans TC）；連不到時自動換成蘋方、微軟正黑體。沒有外部 JS、沒有引用 `/static/`、沒有圖片 |
| 怎麼預覽 | `git fetch origin claude/arsenal-entry-design`，再 `git show origin/claude/arsenal-entry-design:arsenal-design/index.html > /tmp/arsenal.html`，用瀏覽器直接打開就能看（`file://` 也行，我測過 0 個 JS 錯誤、0 個對外請求） |

頁面最上方有一條黃黑斜紋提示「設計稿 ‧ 示範資料」，頁尾也有「本頁為設計稿，資料皆為示範」。`<head>` 有 `noindex`，萬一被放上網也不會被搜尋引擎收錄。
**所有人名、數字、許願都是示範**（示範夥伴 01～40、台中 ‧ 餐飲業 這種），沒有任何真人姓名、照片、電話、LINE。對外沒有放 BNI 商標，也沒有寫分會名義，只說「我們的夥伴」；沒有寫「全台最大」之類沒辦法證明的話。

## 二、頁面各區塊 ↔ 企劃書哪一點

| # | 頁面區塊（錨點） | 對應企劃書 | 做法重點 |
|---|---|---|---|
| 0 | 最上方提示條＋導覽列 | 「設計稿 ‧ 示範資料」提示 | 提示條不黏住；導覽列黏在上方，右邊「我也想被看見」（手機上縮成「加入」） |
| 1 | 首屏 `#top` | 主標、副標、即時人數計數器、兩個最大的按鈕 | 主標「你要的資源，這裡找得到。」、副標「你的優秀與想法，也會在這裡被看見。」；右邊「集結看板」：大數字從 0 數到 `COUNTERS.joined`、進度條到 `goal`、還差幾位、已上架／許願／引薦三個數字、四張臉各幾位。按鈕「找資源」（金色）→ `#find`，「我也想被看見」（框線）→ `#join`，兩顆一樣大 |
| 2 | 找資源 `#find`（需求端） | 搜尋框、「能幫你解決什麼」分類、臉的篩選、人物卡、「請大樹團隊幫我引薦」 | 搜尋同時找姓名、領域、一句話（也找領域的白話說明，例如打「補助」會找到「協會與政府補助」）；分類分兩組：「做生意的難題」＝真 AI 導師席 8 大領域、「做公益的需要」＝**示範分類**；臉：全部／真 AI／真公益／榮樹下嘉賓／志工，每顆按鈕後面有人數，**一人多臉是同一筆資料換看法**（例：示範夥伴 28 同時在「真公益」和兩個領域都找得到，沒有複製）；結果一次 6 位，「再看 6 位」；沒結果時引導去許願池 |
| 2a | 引薦彈窗 | 「這個按鈕要經過我們，不是直接給電話」 | 按下去跳出小表單（你的稱呼、電話或 Email、想請他幫什麼），寫明「我們會先問過他，雙方都同意才牽線」；DEMO 時送出只顯示「已收到（示範）」 |
| 3 | 席次牆 `#wall` | No.001～No.100 創始席，參考榮樹下 1～100 格 | 跟榮樹下同一套格子（葉形圓角、金色亮起）。亮著的格子寫**這位最拿手的領域**（兩個字，例：AI、媒體、教育），整面牆看起來就是「軍火」清單；點了跳出那位的卡。「等你」格點了到 `#join`。另外多一種**虛線「保留」格**＝已入席但還沒按同意上架（不畫名字）。示範：亮 37 格、保留 3 格、等你 60 格。手機 5 欄、每格至少 59×68px |
| 4 | 許願池 `#wish`（需求端） | 「說出你要找什麼」、一個輸入框＋送出、3～5 則示範 | 一個輸入框＋「丟進許願池」；右邊「大家在找什麼」5 則示範許願，標「已牽線 2 位」或「找人中」，看得出池子是活的。送出後新許願出現在最上面，標「只有你看得到（示範）」 |
| 5 | 入選卡 `#card` | 「我入選了大樹軍火庫 No.0XX」、3 張不同領域、直式 4:5、分享 | 3 張卡＝No.001（AI 落地）、No.003（偏鄉教育）、No.032（媒體曝光），由 `SHOWCASE` 決定；旁邊 3 步：被提名→按「我同意上架」→領卡分享。分享：有 Web Share 就叫手機分享選單；沒有就複製網址；再不行就顯示網址框讓人長按複製，每一步都有提示 |
| 6 | 加入區 `#join`（供給端） | 5 分鐘表單：姓名、領域、一句話、公開連結、勾「我同意上架」 | 照企劃書欄位，**另外多一欄「電話或 Email（不公開）」**，原因見第六節；DEMO 時送出只顯示「已收到（示範）」 |
| 7 | 關係階梯（加入區最上面一行） | 路人→被看見→連結→合作→加入 | 一行小字帶過，「被看見」那格亮金色，旁邊寫「填完下面這張表，你就從『路人』走到『被看見』」 |
| 8 | 頁尾 | 「本頁為設計稿，資料皆為示範」＋沿用榮樹下頁尾 | 連結沿用榮樹下頁尾既有的：SoundOn Podcast、榮樹下 LINE@、真公益・企業家俱樂部、回到頂端。**頁尾字也是 20px**（榮樹下頁尾的 16px 例外這裡沒有沿用） |

「每一頁只放一個最大的按鈕」我的理解是「每一區只有一顆主按鈕」：首屏照企劃書放兩顆（一金一框，一樣大），其他區各一顆（席次牆「坐上一個創始席」、入選卡「我也想要一張卡」、加入區「送出，我想被看見」）。如果教練的意思是首屏也只能一顆，把「我也想被看見」那顆拿掉即可。

視覺：沿用榮樹下的色票（墨綠 `#0e1712`、米紙 `#f2ead8`、琥珀金 `#d9a441`）、Noto 宋體大標、葉形圓角、按鈕樣式、彈窗樣式，看得出是同一個品牌家族；首屏背景多一層淡淡的金色格子牆，入選卡是黑金票券＋內框，氣勢比榮樹下更大。

## 三、資料形狀（原樣貼出，之後換成真名冊 API）

畫面上的人物、計數器、許願、入選卡，**全部從 script 最上面這一段畫出來**，HTML 裡沒有寫死任何一個人。下面是 `arsenal-design/index.html` 這一段的原文（一字不改）：

```js
const DEMO = true; // 設計稿開關：true＝所有表單只顯示「已收到（示範）」，不發任何網路請求；接好真資料後改 false 才會打 API

/* ================= 資料區（軍師之後把這一段換成真名冊 API） =================
   畫面上的人物、計數器、許願、入選卡，全部從這裡畫出來。
   ROSTER  每人一筆：no 席次編號、name 姓名、faces 臉（陣列，可多張）、domains 領域（陣列，名稱要跟 DOMAINS 一樣）、
           line 一句話、consent 是否同意公開（只有 true 才畫出來）、link 公開連結（選填，只接受 https://）。
           consent 不是 true 的人：不畫名字，只在席次牆把那一格標成「保留」。正式 API 只要給 {no, consent:false} 就好，別送個資。
   COUNTERS joined 已集結人數（含還沒公開的）、goal 目標、wishes 許願則數、introductions 引薦次數。
   WISHES  許願清單：text 內容、from 哪裡來（地區 ‧ 行業，不放人名）、date 日期、matched 已牽線幾位（0＝找人中）。 */
const API = '/api/works/contact';   // 教練 Mac 上的伺服器 → 「活動報名即時通知」群（欄位格式照抄榮樹下「預約合作」表單）
const SITE = 'arsenal';             // 待軍師確認：伺服器是否接受這個 site 名稱

const FACES = {                     // 臉：key 給程式用，label 給人看
  ai:        {label:'真 AI'},
  charity:   {label:'真公益'},
  rongtree:  {label:'榮樹下嘉賓'},
  volunteer: {label:'志工'}
};
const DOMAINS = [                   // group：biz＝真 AI 導師席 8 大領域；good＝公益領域（示範分類，待軍師換成真公益 9 大領域）
  {group:'biz',  name:'搜尋行銷',       short:'搜尋', need:'讓客戶在網路上搜得到你'},
  {group:'biz',  name:'媒體曝光',       short:'媒體', need:'讓媒體報導你，讓更多人聽見你'},
  {group:'biz',  name:'在地行銷',       short:'在地', need:'讓附近的人走進你的店'},
  {group:'biz',  name:'資本與商業模式', short:'資本', need:'把怎麼賺錢想清楚，找到資金'},
  {group:'biz',  name:'數位轉型',       short:'數位', need:'把紙本和人工流程搬上線'},
  {group:'biz',  name:'協會與政府補助', short:'補助', need:'申請政府補助，接上協會資源'},
  {group:'biz',  name:'AI 落地',        short:'AI',   need:'把 AI 真的用進每天的工作'},
  {group:'biz',  name:'音樂藝文',       short:'藝文', need:'辦一場有質感的活動或藝文合作'},
  {group:'good', name:'偏鄉教育',       short:'教育', need:'讓偏鄉孩子有好的學習機會'},
  {group:'good', name:'長者陪伴',       short:'長者', need:'陪伴長輩，照顧家中老人'},
  {group:'good', name:'弱勢就業',       short:'就業', need:'幫需要的人找到穩定的工作'},
  {group:'good', name:'環境永續',       short:'環境', need:'減碳減塑，讓環境更好'},
  {group:'good', name:'食物分享',       short:'食物', need:'讓多出來的食物送到需要的人手上'},
  {group:'good', name:'身障支持',       short:'身障', need:'支持身障朋友就業與生活'},
  {group:'good', name:'動物保護',       short:'動保', need:'照顧流浪動物，推動認養'},
  {group:'good', name:'社區營造',       short:'社區', need:'讓社區有活力，鄰里互相幫忙'},
  {group:'good', name:'急難救助',       short:'急難', need:'災難或急難時，馬上有人幫忙'}
];
const ROSTER = [                    // 示範資料：全部是假的
  {no:1,  name:'示範夥伴 01', faces:['ai','rongtree'],        domains:['AI 落地','數位轉型'],        line:'一個月，帶中小企業把 AI 用進每天的工作流程。', consent:true, link:'https://example.com/'},
  {no:2,  name:'示範夥伴 02', faces:['ai'],                   domains:['搜尋行銷'],                  line:'讓你的店在 Google 搜得到、地圖找得到。', consent:true},
  {no:3,  name:'示範夥伴 03', faces:['charity'],              domains:['偏鄉教育'],                  line:'每週陪偏鄉孩子上一堂線上英文課，已經陪了三年。', consent:true},
  {no:4,  name:'示範夥伴 04', faces:[],                       domains:['資本與商業模式'],            line:'幫小公司把「怎麼賺錢」講清楚，再去找錢。', consent:true},
  {no:5,  name:'示範夥伴 05', faces:['volunteer'],            domains:['社區營造'],                  line:'活動現場的大小事，交給我排班。', consent:true},
  {no:6,  name:'示範夥伴 06', faces:['ai'],                   domains:['媒體曝光'],                  line:'把你的故事，寫成記者願意報的新聞稿。', consent:true},
  {no:7,  name:'示範夥伴 07', faces:['ai'],                   domains:['數位轉型'],                  line:'（還沒同意公開，這行不會出現在畫面上）', consent:false},
  {no:8,  name:'示範夥伴 08', faces:['charity','volunteer'],  domains:['食物分享'],                  line:'把賣場的即期品，當天送到需要的家庭。', consent:true},
  {no:9,  name:'示範夥伴 09', faces:['ai'],                   domains:['協會與政府補助'],            line:'陪你看懂政府補助，從寫計畫一路到結案。', consent:true},
  {no:10, name:'示範夥伴 10', faces:[],                       domains:['在地行銷'],                  line:'讓方圓三公里內的人，一想到就先想到你。', consent:true},
  {no:11, name:'示範夥伴 11', faces:['rongtree','charity'],   domains:['環境永續'],                  line:'用回收材料做家具，順便教大家怎麼減碳。', consent:true},
  {no:12, name:'示範夥伴 12', faces:['ai'],                   domains:['AI 落地'],                   line:'用 AI 幫業務每天少做兩小時報表。', consent:true},
  {no:13, name:'示範夥伴 13', faces:['volunteer'],            domains:['長者陪伴'],                  line:'每週二下午，陪社區長輩說故事、量血壓。', consent:true},
  {no:14, name:'示範夥伴 14', faces:['ai'],                   domains:['音樂藝文'],                  line:'幫品牌辦一場有溫度的小型音樂會。', consent:true},
  {no:15, name:'示範夥伴 15', faces:['charity'],              domains:['弱勢就業'],                  line:'幫二度就業的媽媽，找到能兼顧家庭的工作。', consent:true},
  {no:16, name:'示範夥伴 16', faces:[],                       domains:['數位轉型'],                  line:'把紙本訂單搬上雲端，老闆用手機就能看。', consent:true},
  {no:17, name:'示範夥伴 17', faces:['ai','volunteer'],       domains:['搜尋行銷','在地行銷'],       line:'教店家自己經營 Google 商家，好評越來越多。', consent:true},
  {no:18, name:'示範夥伴 18', faces:['charity'],              domains:['動物保護'],                  line:'幫流浪貓狗找到家，也幫中途之家募物資。', consent:true},
  {no:19, name:'示範夥伴 19', faces:['charity'],              domains:['偏鄉教育'],                  line:'（還沒同意公開，這行不會出現在畫面上）', consent:false},
  {no:20, name:'示範夥伴 20', faces:['rongtree'],             domains:['資本與商業模式'],            line:'看過上百份營運計畫書，幫你抓出最弱的那一頁。', consent:true},
  {no:21, name:'示範夥伴 21', faces:['ai'],                   domains:['媒體曝光','音樂藝文'],       line:'幫你上 Podcast、上直播，讓更多人聽見你。', consent:true},
  {no:22, name:'示範夥伴 22', faces:['volunteer'],            domains:['急難救助'],                  line:'颱風、地震過後，第一時間組物資車出發。', consent:true},
  {no:23, name:'示範夥伴 23', faces:[],                       domains:['協會與政府補助'],            line:'熟悉商會與協會怎麼運作，幫你找到對的門。', consent:true},
  {no:24, name:'示範夥伴 24', faces:['charity'],              domains:['身障支持'],                  line:'陪身障朋友練職場技能，也陪企業設計友善職缺。', consent:true},
  {no:25, name:'示範夥伴 25', faces:['ai'],                   domains:['數位轉型'],                  line:'幫傳產工廠導入排程系統，交期不再靠喊。', consent:true},
  {no:26, name:'示範夥伴 26', faces:['volunteer','rongtree'], domains:['社區營造'],                  line:'把老街的故事，做成一條可以走的導覽路線。', consent:true},
  {no:27, name:'示範夥伴 27', faces:[],                       domains:['搜尋行銷'],                  line:'幫你寫官網文章，讓客戶搜尋時先看到你。', consent:true},
  {no:28, name:'示範夥伴 28', faces:['charity'],              domains:['偏鄉教育','弱勢就業'],       line:'帶偏鄉青年學一技之長，畢業就有工作。', consent:true},
  {no:29, name:'示範夥伴 29', faces:['ai'],                   domains:['資本與商業模式'],            line:'陪新創練募資簡報，十分鐘講出重點。', consent:true},
  {no:30, name:'示範夥伴 30', faces:['volunteer'],            domains:['食物分享'],                  line:'週末到食物銀行幫忙分裝，一次備好 200 份。', consent:true},
  {no:31, name:'示範夥伴 31', faces:['ai','charity'],         domains:['AI 落地','長者陪伴'],        line:'做給長輩用的 AI 語音小幫手，按一下就能說話。', consent:true},
  {no:32, name:'示範夥伴 32', faces:[],                       domains:['媒體曝光'],                  line:'拍短影音，一支 60 秒把你的產品講清楚。', consent:true},
  {no:33, name:'示範夥伴 33', faces:['volunteer'],            domains:['社區營造'],                  line:'（還沒同意公開，這行不會出現在畫面上）', consent:false},
  {no:34, name:'示範夥伴 34', faces:['rongtree'],             domains:['環境永續'],                  line:'幫工廠算碳排，找出最省錢的減碳方法。', consent:true},
  {no:35, name:'示範夥伴 35', faces:['volunteer'],            domains:['動物保護'],                  line:'假日帶狗狗做社會化訓練，提高認養機會。', consent:true},
  {no:36, name:'示範夥伴 36', faces:['ai'],                   domains:['在地行銷'],                  line:'幫餐廳設計集點和回訪活動，熟客越來越多。', consent:true},
  {no:37, name:'示範夥伴 37', faces:['charity'],              domains:['急難救助','社區營造'],       line:'平常培訓社區防災志工，災難來時就能自救互救。', consent:true},
  {no:38, name:'示範夥伴 38', faces:[],                       domains:['音樂藝文'],                  line:'幫企業尾牙、記者會，找到對的表演團隊。', consent:true},
  {no:39, name:'示範夥伴 39', faces:['ai'],                   domains:['協會與政府補助','AI 落地'],  line:'幫協會用 AI 整理會員資料，申請補助更快。', consent:true},
  {no:40, name:'示範夥伴 40', faces:['charity','volunteer'],  domains:['身障支持'],                  line:'辦手作市集，讓身障夥伴的作品被買走。', consent:true}
];
const COUNTERS = {joined:40, goal:200, wishes:27, introductions:14};   // 示範數字
const WISHES = [                    // 示範許願
  {text:'想找短影音團隊，每個月幫我們拍 4 支產品介紹。',     from:'台中 ‧ 餐飲業',   date:'2026-10-15', matched:2},
  {text:'想找 AI 導入顧問，幫 20 人的公司把報價流程自動化。', from:'新北 ‧ 製造業',   date:'2026-10-14', matched:1},
  {text:'協會想申請政府補助，需要有人帶著寫計畫。',           from:'高雄 ‧ 社團協會', date:'2026-10-14', matched:0},
  {text:'想找願意週末來陪長輩的志工，一個月兩次就好。',       from:'台南 ‧ 社福機構', date:'2026-10-13', matched:3},
  {text:'尾牙想請一組小型樂團，預算有限但很有誠意。',         from:'桃園 ‧ 科技業',   date:'2026-10-12', matched:0}
];
const SHOWCASE = [1, 3, 32];        // 入選卡示範：挑 3 個不同領域的席次
/* ================= 資料區結束 ================= */
```

重點規則（程式已照做）：

- **`consent` 只有 `true` 才畫**：名字、一句話、領域都不會出現在畫面上任何地方（自動測試有掃整頁的文字和屬性確認）。不是 `true` 的人只在席次牆把那格標成「保留」。**正式 API 請不要把沒同意的人的個資送到前端**，給 `{no:7, consent:false}` 就夠。
- `faces` 是陣列，一人可以多張臉；空陣列＝「我們的夥伴」（只在「全部」看得到）。`FACES` 加一個 key，篩選按鈕、首屏人數、卡片標籤會自動多出來。
- `domains` 的名稱要跟 `DOMAINS[].name` 一字不差。`short` 是牆上格子的兩個字，`need` 是「能幫你：……」那句白話。
- `link` 選填，只接受 `https://` 開頭，其他一律不顯示。
- `COUNTERS.joined`＝已集結（**含還沒公開的**）；首屏另外顯示「位已上架」＝`ROSTER` 裡 `consent:true` 的人數，由程式自己算。
- `WISHES[].from` 只寫「地區 ‧ 行業」，不放人名；`matched` 0＝找人中。
- 分享網址是「本頁網址＋`#seat-001`」，打開就直接跳出那位的卡（沒同意公開的席次不會打開）。

## 四、送出：DEMO 開關與 API 欄位

- script 第一行就是 `const DEMO = true;`。DEMO 時三個表單（許願、引薦、加入）**完全不發網路請求**，只在畫面顯示「已收到（示範）」，軍師在 Mac 上預覽不會誤發通知。
- 改成 `false` 才會打 `/api/works/contact`，欄位**照抄榮樹下 `index.html`「預約合作」表單**：`site, name, phone, email, item, message, website`（`website` 是防機器人的隱藏欄位）；聯絡方式有 `@` 放 `email`，否則放 `phone`；成功的判斷也一樣是 `r.ok && json.ok === true`。
- 我在雲端用假的 API 模擬 `DEMO=false`，實際送出的內容如下（`site` 目前寫 `arsenal`）：

```json
{"site":"arsenal","name":"許願池（未留名）","phone":"","email":"","item":"許願池","message":"我想找：想找會剪片的人","website":""}
{"site":"arsenal","name":"王測試","phone":"0912345678","email":"","item":"引薦請求","message":"想認識：No.001 示範夥伴 01","website":""}
{"site":"arsenal","name":"測試夥伴","phone":"","email":"a@b.co","item":"我也想被看見","message":"領域：偏鄉教育\n一句話：我能幫忙\n同意上架：是","website":""}
```

- 伺服器回失敗時：許願池顯示「線上送出暫時沒成功，請稍後再試」，引薦和加入顯示「……或加榮樹下官方 LINE@ 告訴我們」（也測過）。

## 五、我怎麼驗證的

雲端連不到正式網站，所以跟做榮樹下那次一樣，用 Playwright 的 Chromium 在雲端開頁自動檢查，再自己一張一張看截圖。

**自動檢查：有 Google 字型 147 項全過、擋掉 Google 字型（替代字型）135 項全過。** 四種寬度都跑：桌機 1440×900、平板 1024×768、手機 400×860、小手機 360×740。每個寬度都檢查：

1. 沒有 JavaScript 錯誤。
2. 所有字 ≥ 20px：(a) 掃原始碼，所有 `font-size` 和 `font` 簡寫都沒有小於 20px，也沒有用 em／rem／% 繞過；(b) 頁面上每一個有字的元素、輸入框、按鈕、placeholder、`::before`／`::after`，計算後都 ≥ 20px；而且在打開彈窗、送出後、錯誤訊息出現後**再掃一次**。
3. 所有 `#` 連結都找得到位置（包含表單錯誤清單裡的連結）。
4. 創始席剛好 100 格，編號 001～100 照順序；亮 37 格（在 30～40 之間）。
5. 頁面沒有左右多出來可以橫向滑動（一開始、所有互動之後都檢查）。
6. 手機和平板上，所有看得到、可以點的東西都 ≥ 44×44px（一開始、找資源互動後、彈窗打開時、加入表單出現錯誤時都檢查）。
7. **DEMO = true 時，搜尋、換臉、選領域、開人物卡、送引薦、送許願、按分享、送加入表單，全程 0 個對外網路請求、0 個 POST**（只排除 Google 字型檔本身）。
8. 功能：搜尋「AI」有結果；「真公益」只出現有那張臉的人；「真公益＋偏鄉教育」＝2 位；同一人在不同臉都找得到；「再看 6 位」；沒結果時出現許願池連結；點亮著的格子跳出那位的卡；引薦表單空白會提示、填好顯示「已收到（示範）」；許願送出後池子多一則；加入表單空白列出 5 個要補的地方、填好顯示「已收到（示範）」。
9. 沒同意公開的 3 位（No.007、019、033），名字和一句話**不在畫面上任何地方**；`#seat-007` 打不開卡。
10. 分享三條路都測過：有 Web Share（標題「我入選了大樹軍火庫 No.001」、網址結尾 `#seat-001`）、只有剪貼簿（網址真的被複製）、兩個都沒有（顯示網址框）。
11. 入選卡寬÷高＝0.788，接近直式 4:5。
12. `DEMO=false` 模擬：3 次送出欄位跟榮樹下一樣；成功顯示「已送出」、失敗顯示提示；「示範數字」小標籤自動消失。

**自己看截圖後修掉的問題**（都已修好再交）：

- 桌機：首屏右邊的集結看板太高，被螢幕底部切掉 → 縮小數字、重排，1440×900 一屏看完。
- 桌機／手機：「位已公開上架」斷成兩行 → 改「位已上架」。
- 許願池標題「說出你要找什 ／ 麼。」斷在字中間 → 改成兩行「說出你／要找什麼。」。
- 搜尋框、許願框、一句話框的範例字被切掉 → 縮短範例字。
- 平板：三張入選卡高低不齊 → 用格線對齊，三張一樣高、分享鈕在同一條線；修的過程中一度讓卡片變寬、平板出現橫向捲動，抓到後已修正。
- 分享網址打開時，背後的頁面沒捲到席次牆 → 修好並加測試。
- 表單錯誤清單裡的連結在手機上只有 29px 高 → 加高到 44px。

手機版（400、360）樣子：首屏主標兩行、兩顆按鈕滿版上下排、集結看板在下面；找資源的分類每排兩顆；席次牆 5 欄 × 20 排；入選卡一張一張往下排；表單欄位滿版。替代字型（沒有 Google 字型）也看過，版面不壞。

自動檢查腳本附在這封信最後的附錄（照規定沒有另外加檔案），要在 Mac 上重跑可以直接複製。

## 六、沒做完、我不確定、要軍師決定的地方

1. **公益領域是我自己想的示範分類**（偏鄉教育、長者陪伴、弱勢就業、環境永續、食物分享、身障支持、動物保護、社區營造、急難救助），**待軍師換成真公益 9 大領域**。換的時候每一項要給 `name`、`short`（牆上兩個字）、`need`（能幫你：……）。
2. **`site:'arsenal'`**：不確定伺服器 `/api/works/contact` 有沒有限制 `site` 只能是已知的名稱。如果有，要在伺服器加上 `arsenal`，或改用 `rongtree`。
3. **許願池只有一個輸入框**（照企劃書），所以送出時 `name` 寫「許願池（未留名）」、`phone`／`email` 是空的。如果伺服器規定一定要有聯絡方式，會送不出去；而且沒有聯絡方式，大樹團隊也沒辦法回覆許願的人。要不要加一個「選填：怎麼聯絡你」，請軍師決定。
4. **加入表單我多加了一欄「電話或 Email（不公開）」**（企劃書沒列）。原因：沒有它，大樹團隊沒辦法跟本人確認、也沒辦法請他按「我同意上架」，API 的 `phone`／`email` 也會是空的。不要的話刪掉那一個 `.field` 和檢查那一行即可。
5. **`COUNTERS.joined` 的定義**：我設計成「已集結（含還沒公開的）」，首屏另外顯示「位已上架」。示範是 40 位集結、37 位上架、3 格保留。如果教練要對外只喊公開上架的人數，把 `joined` 改成等於上架人數就好。
6. **席次號碼什麼時候給**：我的設計是「入列就給號碼，按同意才亮起來」，所以牆上會有「保留」格。如果決定「按同意才給號碼」，就不會有保留格，程式不用改。
7. **我們的夥伴（BNI）沒有自己的臉**：企劃書的篩選沒有這一項，所以 `faces:[]` 的人只在「全部」看得到，卡片標「我們的夥伴」。如果要讓他們也能被篩選，在 `FACES` 加一個 `partner:{label:'我們的夥伴'}` 就會自動出現（顏色已預留）。
8. **「即時」目前是頁面打開時讀常數**，數字會從 0 數上來，但不會自己再更新。接 API 後建議開頁讀一次、之後每 1～5 分鐘重抓一次。「進度每天看得到在漲」目前只有進度條；如果要畫每天的成長曲線，`COUNTERS` 要再多一個每天人數的清單（我沒做，避免加企劃書沒要的東西）。
9. **分享到 LINE／FB 的預覽圖**：設計稿沒有 `og:image`，分享出去的預覽只會是一般網頁。如果要「每個人的入選卡自己一張預覽圖」，需要伺服器幫每一位產生圖片，這部分前端做不到，留給軍師評估。
10. **手機選單**：榮樹下用的漢堡選單是 `/static/nav-burger.js`（Mac 伺服器上的檔案），照規定沒有引用；所以窄螢幕只顯示品牌和「加入」。正式上線時可以接回共用的漢堡選單。
11. **正式上線前要手動拿掉的東西**：最上方提示條 `.demo-bar`、頁尾 `.foot-demo`、`<head>` 的 `noindex`、`<title>` 的「（設計稿）」、頁尾「© 2026 大樹軍火庫 ‧ 設計稿」。（「示範數字」標籤、表單下的「設計稿：按下去……」、入選卡底下的「示範卡 ‧ 設計稿」會跟著 `DEMO=false` 自動消失。）

## 七、要軍師在 Mac 上接真資料或確認的清單

1. 在 Mac 上打開設計稿看一遍（桌機＋手機），覺得可以再給教練看。
2. 決定名冊 API 的網址和形狀，例如 `GET /api/arsenal/roster` 回 `{roster, counters, wishes}`，欄位照第三節；然後把 `ROSTER`／`COUNTERS`／`WISHES` 三個常數改成從 API 讀（畫面程式不用改）。
3. 確認 `/api/works/contact` 接不接受 `site:'arsenal'`、`item:'許願池'／'引薦請求'／'我也想被看見'`，以及許願池沒有聯絡方式時會不會被擋。
4. 換上真公益 9 大領域（第六節第 1 點）。
5. 決定第六節第 3～7 點。
6. 決定這頁正式要放在哪個網址；放上去前拿掉第六節第 11 點的設計稿標記，把 `DEMO` 改成 `false`。

—— 雲端特助

---

## 附錄：自動檢查腳本（要在 Mac 上重跑可以直接複製）

存成倉庫最上層的 `arsenal_check.js`（**只是本機檢查用，不要 commit**），需要 Node 和 Playwright。

<details><summary>展開腳本</summary>

```js
// 軍火庫設計稿自動檢查
// 用法（在倉庫最上層資料夾）：
//   1) 開一個視窗：python3 -m http.server 8765 --bind 127.0.0.1
//   2) 另一個視窗：node arsenal_check.js            （會用 Google 字型）
//                  node arsenal_check.js --offline  （擋掉 Google 字型，看替代字型）
//   截圖會存到 ./arsenal-shots/（只是本機檢查用，不要 commit）
const { chromium } = require('playwright');
const fs = require('fs');
const path = require('path');
const FILE = process.env.FILE || 'arsenal-design/index.html';
const BASE = 'http://127.0.0.1:8765/arsenal-design/index.html';
const OUT = process.env.OUT || 'arsenal-shots';
fs.mkdirSync(OUT, { recursive: true });
const BLOCK_FONTS = process.argv.includes('--offline');

const report = [];
const check = (name, ok, detail = '') => { report.push({ name, ok, detail }); console.log(`${ok ? 'PASS' : 'FAIL'}  ${name}${detail ? '  → ' + (typeof detail === 'string' ? detail : JSON.stringify(detail)) : ''}`); };

// ---- 1. 掃 CSS／JS 原始碼：任何 font-size 或 font 簡寫都不能小於 20px ----
function scanSource() {
  const src = fs.readFileSync(FILE, 'utf8');
  const bad = [];
  for (const m of src.matchAll(/font-size\s*:\s*([^;}"`]+)/g)) {
    const v = m[1].trim();
    if (/^(inherit|initial|unset)$/.test(v)) continue;
    const px = [...v.matchAll(/(\d+(?:\.\d+)?)px/g)].map(x => +x[1]);
    if (!px.length || px.some(n => n < 20)) bad.push('font-size:' + v);
  }
  for (const m of src.matchAll(/(?<![-\w])font\s*:\s*([^;}"`]+)/g)) {
    const v = m[1].trim();
    if (/^(inherit|initial|unset)$/.test(v)) continue;
    const size = v.split('/')[0];
    const px = [...size.matchAll(/(\d+(?:\.\d+)?)px/g)].map(x => +x[1]);
    if (!px.length || px.some(n => n < 20)) bad.push('font:' + v);
  }
  // 也不准用 em／rem／% 來設字級（避免繞過檢查）
  for (const m of src.matchAll(/font(?:-size)?\s*:[^;}]*\d(?:em|rem|%)/g)) bad.push('相對單位:' + m[0]);
  check('原始碼：沒有任何小於 20px 的 font-size／font 簡寫', bad.length === 0, bad);
  check('原始碼：script 第一行是 const DEMO = true;', /<script>\s*const DEMO = true;/.test(src));
  check('原始碼：沒有引用 /static/ 或外部 CDN 腳本', !/\/static\//.test(src) && !/<script[^>]+src=/.test(src));
  return src;
}

// ---- 頁面裡：每個有字的元素，計算後字級都要 ≥ 20px ----
const fontScan = () => {
  const bad = [], seen = new Set();
  const w = document.createTreeWalker(document.body, NodeFilter.SHOW_TEXT);
  while (w.nextNode()) {
    const t = w.currentNode; if (!t.textContent.trim()) continue;
    const el = t.parentElement; if (!el || seen.has(el) || el.closest('script,style,noscript')) continue; seen.add(el);
    const fs = parseFloat(getComputedStyle(el).fontSize);
    if (fs < 20) bad.push({ el: el.tagName + '.' + el.className, text: t.textContent.trim().slice(0, 20), fs });
  }
  for (const el of document.querySelectorAll('input,select,textarea,button,option,optgroup')) {
    const fs = parseFloat(getComputedStyle(el).fontSize);
    if (fs < 20) bad.push({ el: el.tagName + '#' + el.id, fs });
    if (el.placeholder) { const p = parseFloat(getComputedStyle(el, '::placeholder').fontSize); if (p < 20) bad.push({ el: el.id + '::placeholder', fs: p }); }
  }
  for (const el of document.querySelectorAll('body *')) for (const ps of ['::before', '::after']) {
    const cs = getComputedStyle(el, ps), c = cs.content;
    if (!c || c === 'none' || c === 'normal' || c === '""') continue;
    if (parseFloat(cs.fontSize) < 20) bad.push({ el: el.tagName + '.' + el.className + ps, content: c, fs: cs.fontSize });
  }
  return bad;
};

const anchorScan = () => [...document.querySelectorAll('a[href^="#"]')].map(a => a.getAttribute('href'))
  .filter(h => h === '#' || !document.getElementById(decodeURIComponent(h.slice(1))));

const tapScan = (scope) => {
  const bad = [];
  const root = scope ? document.querySelector(scope) : document;
  for (const el of root.querySelectorAll('a[href],button,input:not([type=hidden]),select,textarea,summary,label.consent')) {
    if (el.classList.contains('hp') || el.type === 'checkbox') continue;
    if (el.closest('[hidden]') || el.closest('dialog:not([open])')) continue;
    const cs = getComputedStyle(el); if (cs.display === 'none' || cs.visibility === 'hidden') continue;
    const r = el.getBoundingClientRect(); if (!r.width && !r.height) continue;
    if (r.right < 0) continue; // 跳到主要內容（還沒按 Tab 時藏在畫面外）
    if (r.width < 44 || r.height < 44) bad.push({ el: el.tagName + (el.id ? '#' + el.id : '') + '.' + el.className, text: (el.textContent || el.placeholder || '').trim().slice(0, 16), w: Math.round(r.width), h: Math.round(r.height) });
  }
  return bad;
};

(async () => {
  const src = scanSource();
  const browser = await chromium.launch({ args: process.env.HTTPS_PROXY ? ['--proxy-server=' + process.env.HTTPS_PROXY, '--proxy-bypass-list=127.0.0.1;localhost'] : [] });
  const sizes = [
    { name: 'desktop1440', w: 1440, h: 900 },
    { name: 'tablet1024', w: 1024, h: 768, mobile: true },
    { name: 'mobile400', w: 400, h: 860, mobile: true },
    { name: 'mobile360', w: 360, h: 740, mobile: true },
  ];
  for (const sz of sizes) {
    const tag = sz.name + (BLOCK_FONTS ? '-offline' : '');
    const ctx = await browser.newContext({ viewport: { width: sz.w, height: sz.h }, isMobile: !!sz.mobile, hasTouch: !!sz.mobile, deviceScaleFactor: 1 });
    const page = await ctx.newPage();
    if (BLOCK_FONTS) await page.route(/fonts\.(googleapis|gstatic)\.com/, r => r.abort());
    const jsErr = [];
    page.on('pageerror', e => jsErr.push(e.message));
    page.on('console', m => { if (m.type() === 'error' && !/fonts\.g/.test(m.text()) && !/ERR_FAILED|net::/.test(m.text())) jsErr.push('console: ' + m.text()); });
    await page.goto(BASE, { waitUntil: 'networkidle' });
    await page.waitForTimeout(1800);
    const fontsOk = await page.evaluate(() => [...document.fonts].some(f => f.status === 'loaded' && /Noto/.test(f.family)));
    console.log(`\n=== ${tag}（Google 字型${fontsOk ? '有' : '沒有'}載入，${fontsOk ? '用 Noto' : '用替代字型'}）===`);

    const ov = await page.evaluate(() => ({ sw: document.documentElement.scrollWidth, cw: document.documentElement.clientWidth }));
    check(`${tag} 頁面沒有左右多出來`, ov.sw <= ov.cw, ov);
    check(`${tag} 所有字 ≥ 20px（初始畫面）`, (await page.evaluate(fontScan)).length === 0, await page.evaluate(fontScan));
    check(`${tag} 所有 # 連結都找得到位置`, (await page.evaluate(anchorScan)).length === 0, await page.evaluate(anchorScan));
    const grid = await page.evaluate(() => [...document.querySelectorAll('#seat-grid > li .n')].map(n => n.textContent));
    check(`${tag} 創始席剛好 100 格、編號 001～100 照順序`, grid.length === 100 && grid.every((t, i) => t === String(i + 1).padStart(3, '0')));
    const lit = await page.evaluate(() => ({ on: document.querySelectorAll('#seat-grid .cell.on').length, held: document.querySelectorAll('#seat-grid .cell.held').length, wait: document.querySelectorAll('#seat-grid a.cell').length }));
    check(`${tag} 牆上亮 30～40 格`, lit.on >= 30 && lit.on <= 40, lit);
    const hidden = await page.evaluate(() => { const shown = [...document.body.querySelectorAll('*')].filter(e => !e.closest('script')).map(e => [...e.childNodes].filter(n => n.nodeType === 3).map(n => n.textContent).join('') + ' ' + [...e.attributes].map(x => x.value).join(' ')).join('\n'); return ['示範夥伴 07', '示範夥伴 19', '示範夥伴 33', '還沒同意公開'].filter(s => shown.includes(s)); });
    check(`${tag} consent 不是 true 的人，名字不會出現在畫面上`, hidden.length === 0, hidden);
    const tally = await page.evaluate(() => ({ joined: document.getElementById('c-joined').textContent, goal: document.getElementById('c-goal').textContent, bar: document.querySelector('#c-bar i').style.width }));
    check(`${tag} 計數器畫出 COUNTERS（40／200）`, tally.joined === '40' && tally.goal === '200' && tally.bar === '20%', tally);
    if (sz.mobile) check(`${tag} 手機可點的東西都 ≥ 44×44px`, (await page.evaluate(tapScan)).length === 0, await page.evaluate(tapScan));

    await page.screenshot({ path: `${OUT}/${tag}-top.png` });
    await page.screenshot({ path: `${OUT}/${tag}-full.png`, fullPage: true });

    // ---- 互動＋網路請求監聽（DEMO=true 不准發任何對外請求） ----
    const reqs = [];
    page.on('request', r => { if (!/fonts\.(googleapis|gstatic)\.com/.test(r.url())) reqs.push(r.method() + ' ' + r.url()); });
    // 找資源
    await page.fill('#q', 'AI');
    let n = await page.evaluate(() => document.querySelectorAll('#results > li').length);
    const cnt = await page.textContent('#r-count');
    check(`${tag} 搜尋「AI」有結果`, n > 0, cnt);
    await page.fill('#q', '');
    await page.click('#faces [data-face="charity"]');
    const charity = await page.evaluate(() => [...document.querySelectorAll('#results .tags')].every(t => t.textContent.includes('真公益')));
    check(`${tag} 換臉：真公益只顯示有「真公益」臉的人`, charity);
    await page.click('#domains [data-domain="偏鄉教育"]');
    const edu = await page.evaluate(() => ({ n: document.querySelectorAll('#results > li').length, need: document.getElementById('r-need').textContent }));
    check(`${tag} 領域：真公益＋偏鄉教育`, edu.n === 2, edu);
    const multi = await page.evaluate(() => { const c = [...document.querySelectorAll('#results .pcard')].find(x => x.textContent.includes('示範夥伴 28')); return !!c; });
    check(`${tag} 一人多臉：同一人在不同臉都找得到（不是複製資料）`, multi);
    await page.click('#r-clear');
    const all = await page.evaluate(() => ({ shown: document.querySelectorAll('#results > li').length, more: document.getElementById('r-more').hidden }));
    check(`${tag} 清除條件後顯示 6 位＋「再看」按鈕`, all.shown === 6 && all.more === false, all);
    await page.click('#r-more');
    check(`${tag} 再看 6 位`, (await page.evaluate(() => document.querySelectorAll('#results > li').length)) === 12);
    await page.fill('#q', '找不到的東西zzz');
    check(`${tag} 沒結果時引導去許願池`, await page.isVisible('#r-empty'));
    await page.fill('#q', '');
    if (sz.mobile) check(`${tag} 找資源區互動後 ≥ 44px`, (await page.evaluate(() => (window.__tap = null, 0))) === 0 && (await page.evaluate(tapScan)).length === 0, await page.evaluate(tapScan));

    // 人物卡（牆上點亮的格子）
    await page.click('#seat-grid button.cell[data-no="12"]');
    await page.waitForSelector('#dlg[open]');
    check(`${tag} 點亮著的格子 → 看到那位的卡`, (await page.textContent('#dlg-h')).includes('示範夥伴 12'));
    check(`${tag} 彈窗字 ≥ 20px`, (await page.evaluate(fontScan)).length === 0, await page.evaluate(fontScan));
    if (sz.mobile) check(`${tag} 彈窗可點的東西 ≥ 44px`, (await page.evaluate(tapScan, '#dlg')).length === 0, await page.evaluate(tapScan, '#dlg'));
    await page.screenshot({ path: `${OUT}/${tag}-dlg-person.png` });
    // 引薦請求
    await page.click('#dlg [data-intro]');
    await page.click('#if button[type=submit]');
    check(`${tag} 引薦表單空白送出會提示`, await page.isVisible('#i-errsum'));
    await page.fill('#i-name', '測試');
    await page.fill('#i-contact', 'test@example.com');
    await page.fill('#i-msg', '想請他幫忙');
    await page.screenshot({ path: `${OUT}/${tag}-dlg-intro.png` });
    await page.click('#if button[type=submit]');
    await page.waitForTimeout(200);
    check(`${tag} 引薦送出 → 已收到（示範）`, (await page.textContent('#dlg-body')).includes('已收到（示範）'));
    check(`${tag} 彈窗（送出後）字 ≥ 20px`, (await page.evaluate(fontScan)).length === 0, await page.evaluate(fontScan));
    await page.click('#dlg [data-close]');
    // 結果卡上的引薦按鈕
    await page.click('#results [data-intro]');
    check(`${tag} 人物卡的「請大樹團隊幫我引薦」有回饋（開出引薦表單）`, await page.isVisible('#if'));
    await page.click('#dlg .dlg-x');
    // 許願池
    await page.click('#wf button[type=submit]');
    check(`${tag} 許願空白送出會提示`, (await page.textContent('#w-err')).length > 0);
    await page.fill('#w-text', '想找會剪片的人，幫我們做招生影片');
    await page.click('#wf button[type=submit]');
    await page.waitForTimeout(200);
    const wish = await page.evaluate(() => ({ ok: document.getElementById('w-ok').textContent, first: document.querySelector('#wishes li').textContent }));
    check(`${tag} 許願送出 → 已收到（示範），池子多一則`, wish.ok.includes('已收到（示範）') && wish.first.includes('剪片'), wish);
    // 入選卡分享（這台 Chromium 沒有 Web Share，也沒給剪貼簿權限 → 要退回「手動複製網址」）
    await page.click('#showcase [data-share="3"]');
    await page.waitForTimeout(200);
    const share = await page.evaluate(() => document.querySelector('[data-share="3"]').nextElementSibling.textContent + '|' + (document.querySelector('.share-url') || {}).value);
    check(`${tag} 分享失敗時有提示＋網址`, /長按|已複製/.test(share) && share.includes('#seat-003'), share);
    // 加入表單
    await page.click('#jf button[type=submit]');
    const errs = await page.evaluate(() => document.querySelectorAll('#j-errsum li').length);
    check(`${tag} 加入表單空白送出列出 5 個要補的地方`, errs === 5, errs);
    check(`${tag} 錯誤清單裡的 # 連結都找得到位置`, (await page.evaluate(anchorScan)).length === 0, await page.evaluate(anchorScan));
    if (sz.mobile) check(`${tag} 加入表單（有錯誤時）可點的東西 ≥ 44px`, (await page.evaluate(tapScan, '#join')).length === 0, await page.evaluate(tapScan, '#join'));
    await page.fill('#j-name', '測試夥伴');
    await page.selectOption('#j-domain', 'AI 落地');
    await page.fill('#j-line', '我能幫忙測試');
    await page.fill('#j-link', 'https://example.com');
    await page.fill('#j-contact', '0912345678');
    await page.check('#j-consent');
    await page.click('#jf button[type=submit]');
    await page.waitForTimeout(200);
    check(`${tag} 加入送出 → 已收到（示範）`, (await page.textContent('#j-done-eye')) === '已收到（示範）' && await page.isVisible('#j-done'));
    check(`${tag} 所有互動後，字仍 ≥ 20px`, (await page.evaluate(fontScan)).length === 0, await page.evaluate(fontScan));
    const ov2 = await page.evaluate(() => document.documentElement.scrollWidth <= document.documentElement.clientWidth);
    check(`${tag} 所有互動後，頁面仍沒有左右多出來`, ov2);
    await page.waitForTimeout(300);
    check(`${tag} DEMO=true：上面所有送出都沒有發出任何網路請求`, reqs.length === 0, reqs);
    check(`${tag} 沒有 JavaScript 錯誤`, jsErr.length === 0, jsErr);
    await ctx.close();
  }

  if (!BLOCK_FONTS) {
    // ---- 分享成功的兩條路：有 Web Share、有剪貼簿 ----
    console.log('\n=== 分享按鈕 ===');
    let ctx = await browser.newContext({ viewport: { width: 400, height: 860 }, isMobile: true, hasTouch: true });
    let page = await ctx.newPage();
    await page.addInitScript(() => { navigator.share = async d => { window.__shared = d; }; });
    await page.goto(BASE); await page.click('#showcase [data-share="1"]'); await page.waitForTimeout(100);
    const sd = await page.evaluate(() => window.__shared);
    check('有 Web Share 時用系統分享（標題、網址正確）', sd && sd.title === '我入選了大樹軍火庫 No.001' && /#seat-001$/.test(sd.url), sd);
    await ctx.close();
    ctx = await browser.newContext({ viewport: { width: 1440, height: 900 }, permissions: ['clipboard-read', 'clipboard-write'] });
    page = await ctx.newPage(); await page.goto(BASE);
    await page.click('#showcase [data-share="32"]'); await page.waitForTimeout(200);
    const clip = await page.evaluate(() => navigator.clipboard.readText());
    check('沒有 Web Share 時改成複製網址', /#seat-032$/.test(clip) && (await page.textContent('[data-share="32"] + .share-msg')).includes('已複製'), clip);
    // 分享出去的網址：打開直接看到那位的卡
    await page.goto(BASE + '#seat-012'); await page.waitForSelector('#dlg[open]');
    check('分享網址 #seat-012 打開就跳出那位的卡', (await page.textContent('#dlg-h')).includes('示範夥伴 12'));
    check('分享網址打開時，背後的頁面停在創始席牆', await page.evaluate(() => { const t = document.getElementById('wall').getBoundingClientRect().top; return t > -20 && t < 200; }));
    { const p2 = await ctx.newPage(); await p2.goto(BASE + '#seat-003'); await p2.waitForSelector('#dlg[open]');
      check('直接打開 #seat-003（新分頁）也會跳出那位的卡、停在牆', (await p2.textContent('#dlg-h')).includes('示範夥伴 03') && await p2.evaluate(() => { const t = document.getElementById('wall').getBoundingClientRect().top; return t > -20 && t < 200; }));
      await p2.close(); const p3 = await ctx.newPage(); await p3.goto(BASE + '#seat-007'); await p3.waitForTimeout(300);
      check('沒同意公開的 #seat-007（新分頁）不會打開任何卡', !(await p3.evaluate(() => document.getElementById('dlg').open)));
      await p3.close(); }
    await page.screenshot({ path: `${OUT}/deeplink-desktop.png` });
    await page.locator('#card').screenshot({ path: `${OUT}/cards-desktop.png` });
    const ratio = await page.evaluate(() => [...document.querySelectorAll('.tcard')].map(c => { const r = c.getBoundingClientRect(); return +(r.width / r.height).toFixed(3); }));
    check('入選卡接近直式 4:5（寬÷高 ≈ 0.8）', ratio.every(r => r > 0.74 && r <= 0.81), ratio);
    await ctx.close();

    // ---- DEMO=false：會照榮樹下欄位格式打 /api/works/contact ----
    console.log('\n=== DEMO = false（模擬正式上線，API 用假的回應） ===');
    const live = src.replace('const DEMO = true;', 'const DEMO = false;');
    ctx = await browser.newContext({ viewport: { width: 1440, height: 900 } });
    page = await ctx.newPage();
    const posts = [];
    await page.route(BASE, r => r.fulfill({ body: live, contentType: 'text/html; charset=utf-8' }));
    await page.route('**/api/works/contact', r => { posts.push(JSON.parse(r.request().postData())); r.fulfill({ status: 200, contentType: 'application/json', body: '{"ok":true}' }); });
    await page.goto(BASE);
    check('DEMO=false 時不顯示「示範數字」標籤', await page.evaluate(() => document.getElementById('c-demo').hidden));
    await page.fill('#w-text', '想找會剪片的人'); await page.click('#wf button[type=submit]'); await page.waitForTimeout(300);
    await page.click('#results [data-intro]'); await page.fill('#i-name', '王測試'); await page.fill('#i-contact', '0912345678'); await page.click('#if button[type=submit]'); await page.waitForTimeout(300);
    await page.click('#dlg [data-close]');
    await page.fill('#j-name', '測試夥伴'); await page.selectOption('#j-domain', '偏鄉教育'); await page.fill('#j-line', '我能幫忙'); await page.fill('#j-contact', 'a@b.co'); await page.check('#j-consent');
    await page.click('#jf button[type=submit]'); await page.waitForTimeout(300);
    const keys = 'site,name,phone,email,item,message,website';
    check('送了 3 次（許願、引薦、加入）', posts.length === 3, posts.length);
    check('每次欄位都跟榮樹下「預約合作」一樣：site,name,phone,email,item,message,website', posts.every(p => Object.keys(p).join(',') === keys), posts.map(p => Object.keys(p).join(',')));
    console.log(JSON.stringify(posts, null, 1));
    check('正式送出成功顯示「已送出」', (await page.textContent('#j-done-eye')) === '已送出');
    await ctx.close();
    // 伺服器失敗時的提示
    ctx = await browser.newContext({ viewport: { width: 400, height: 860 } });
    page = await ctx.newPage();
    await page.route(BASE, r => r.fulfill({ body: live, contentType: 'text/html; charset=utf-8' }));
    await page.route('**/api/works/contact', r => r.fulfill({ status: 500, body: 'x' }));
    await page.goto(BASE);
    await page.fill('#w-text', '想找會剪片的人'); await page.click('#wf button[type=submit]'); await page.waitForTimeout(300);
    check('API 失敗時許願池顯示「暫時沒成功」', (await page.textContent('#w-err')).includes('暫時沒成功'));
    await ctx.close();
  }
  await browser.close();
  const fail = report.filter(r => !r.ok);
  console.log(`\n共 ${report.length} 項，通過 ${report.length - fail.length}，失敗 ${fail.length}`);
  process.exit(fail.length ? 1 : 0);
})().catch(e => { console.error(e); process.exit(2); });
```

</details>
