# 從零完成作業：逐步操作指南

## 你最後要交什麼
1. LLM Wiki 專案（至少 5 份來源文件已放進 `raw/`，並有整理後 Wiki）。
2. 可瀏覽的 HTML 教學簡報。
3. Loop / Graph 設計圖與節點說明。
4. 真實執行紀錄與檢查結果。
5. 反思：最容易出錯的節點、檢查前移的地方、流程如何調整。

> 截止時間依課程公告：11/30 23:59；若有延長，以老師最新公告為準。

---

## Step 1｜建立工作環境（約 10–15 分鐘）
**你要做：**
1. 解壓縮本專案 ZIP。
2. 用 Antigravity 或 Claude Code 開啟 `random_walk_llm_wiki` 資料夾。
3. 確認看得到 `AGENTS.md`、`raw/`、`wiki/`、`deck.html`。
4. 若工具支援 Git，開啟終端機執行：
   `git init`
   `git add .`
   `git commit -m "initial project structure"`

**完成判準：** Agent 能讀取資料夾內的規則與檔案。

## Step 2｜先討論需求，不要立刻生成（約 10 分鐘）
**你要做：**
1. 開啟 `PROMPTS.md`，複製「Prompt A：需求訪談」。
2. 貼給 Agent。
3. 回答它提出的問題。若 Agent 沒問到來源格式、引用方式、矛盾處理、輸出格式、檢查項目，請主動補充。
4. 請 Agent 整理需求摘要。
5. 你確認摘要正確後，才讓它建立／修改專案規則。

**完成判準：** 你已確認需求摘要；不是 AI 自行假設需求。

## Step 3｜蒐集至少五份來源（約 30–60 分鐘）
建議來源如下（來源連結與用途也在 `SOURCES.md`）：
- S1：Hyndman & Athanasopoulos，《Forecasting: Principles and Practice》，ARIMA / Random walk model。
- S2：Stock & Watson，《Introduction to Econometrics》，random walk 與 stochastic trend。
- S3：Eugene F. Fama，〈Random Walks in Stock Market Prices〉（1995）。
- S4：Eugene F. Fama，〈The Behavior of Stock-Market Prices〉（1965）。
- S5：Rob J. Hyndman，〈Derivations of forecast variances for benchmark methods〉（2022）。

**你要做：**
1. 逐一開啟 `SOURCES.md` 的連結。
2. 將可下載的 PDF 下載；網頁來源可另存為 HTML 或 PDF。
3. 將五份原始文件放進 `raw/`，並用 `S1_...` 到 `S5_...` 命名。
4. 在 `evidence_cards/` 對應卡片補上實際閱讀位置（章節、頁碼或網頁標題）。
5. 不要只把網址貼進 raw；必須保存可閱讀的來源內容。

**完成判準：** `raw/` 至少有五份可打開、可閱讀的來源文件。

## Step 4｜Ingest：一次處理一份來源（約 30–60 分鐘）
**你要做：**
1. 複製 `PROMPTS.md` 的「Prompt B：單篇 Ingest」。
2. 一次提供一份 raw 文件給 Agent。
3. 要求 Agent 先產生／更新對應 evidence card，再更新 Wiki。
4. 每篇處理完，檢查是否有作者、標題、章節／頁碼、支持主張、限制。
5. 每次更新 `log.md`，記下處理了哪份來源、更新哪些 Wiki 頁面。

**完成判準：** 五份來源都有 evidence card；Wiki 中的重要內容可回溯到來源。

## Step 5｜檢查 Wiki（約 20 分鐘）
**你要做：**
1. 逐頁閱讀 `wiki/`。
2. 檢查公式是否正確、變數是否解釋、引用是否存在。
3. 特別確認「隨機漫步」不是「股價每天固定上漲／下跌」，也不是「所有股票價格都已被證明完全符合隨機漫步」。
4. 確認漂移模型與無漂移模型沒有混用。
5. 請 Agent 執行 `PROMPTS.md` 的「Prompt C：Wiki 審查」。

**完成判準：** 無未標示的無來源主張；不確定內容標記待查證；每個公式假設清楚。

## Step 6｜產生簡報大綱（約 10 分鐘）
**你要做：**
1. 複製「Prompt D：簡報大綱」。
2. 要求每頁列出教學目標、核心訊息、使用的 Wiki 頁面、來源 ID。
3. 逐頁確認大綱是否符合初學者的學習順序。
4. 若某個重要概念沒有來源支持，先回到 Ingest，不要直接讓 AI 補寫。

**完成判準：** 每一頁都能指出它使用哪一頁 Wiki、哪一份來源。

## Step 7｜生成 HTML 簡報（約 20–40 分鐘）
**你要做：**
1. 複製「Prompt E：HTML 生成」。
2. 指定輸出檔案為 `deck.html`。
3. 要求 Agent 以 Wiki 為主要知識來源，禁止無依據補充。
4. 開啟 `deck.html`，用瀏覽器測試按鈕與鍵盤方向鍵。
5. 點選互動模擬，確認圖形會更新。

**完成判準：** 9 頁左右、可切換、引用清楚、公式可讀、模擬能執行。

## Step 8｜Graph 與 Loop 設計（約 15 分鐘）
參考 `workflow.mmd`。你要能說明：
- Graph 管理整體順序與退回路徑。
- 每個節點內可有小 Loop，例如逐頁稿件檢查、HTML 渲染修正。
- 程式檢查負責頁數、連結、引用標記、互動功能等可機械驗證項目。
- 獨立 AI 審查負責內容是否忠於來源、公式解釋是否講反、是否漏掉大綱重點。
- 每個 Loop 最多 3 輪；若來源不足就停止並列出缺口。

**完成判準：** 你能指出每個節點輸入、輸出、檢查方式、失敗時退回哪一節點。

## Step 9｜實際測試與記錄（約 15–25 分鐘）
**你要做：**
1. 照 `CHECKLIST.md` 逐項測試。
2. 在 `log.md` 寫實際結果，不要預先填「全部通過」。
3. 若有錯，記錄錯誤、修正節點、重測結果。
4. 截圖保存：Agent 需求訪談、raw 五份文件、Wiki、HTML 簡報、檢查結果。

**完成判準：** 有可核對的實際紀錄與截圖。

## Step 10｜完成報告與提交（約 20 分鐘）
**你要做：**
1. 複製 `REPORT_TEMPLATE.md`，填入姓名、學號、系級、實際連結。
2. 把 Graph 圖、執行紀錄、檢查表與反思放入報告。
3. 反思必須根據真實過程：哪裡最常錯、為何將檢查前移、流程如何改動。
4. 用指定命名格式命名：`學校簡稱_學號_系級_姓名_隨機漫步`。
5. 最後確認 Wiki 與 HTML 連結能讓老師開啟。

---

## 建議時間分配
| 工作 | 預估時間 |
|---|---:|
| 環境與需求討論 | 25 分鐘 |
| 蒐集五份來源 | 30–60 分鐘 |
| Ingest 與 Wiki 整理 | 60–90 分鐘 |
| Wiki 檢查與簡報大綱 | 30 分鐘 |
| HTML 生成與測試 | 40–60 分鐘 |
| Graph、紀錄、報告 | 40 分鐘 |
