# 工具總覽與技術決策

[← 回課程總覽](../README.md)

向量資料庫簡單說，就是把文字轉成「語義向量」後儲存、並用「語義相似度」搜尋的資料庫，把 Blazz 的合約條款、FAQ 內容先轉成一串數字（embedding），使用者問問題時也轉成同樣的數字，再去找「意思最接近」的那幾段內容回傳給 AI 當參考，這就是 RAG（Retrieval-Augmented Generation）的核心。Embedding API 跟 Qdrant 是兩個各自獨立、互不認識的雲端服務，只要向量維度對得上就能任意搭配——[第二堂](weeks/week-2.md)會先直接呼叫這兩個服務的 API 建好向量資料庫，讓學員看懂原理，[第三堂](weeks/week-3.md)再用 n8n 現成節點（或 HTTP Request 節點）把同一組呼叫串起來，Pinecone 是 Qdrant 之外另一個常見選項。

> 🔧 **Embedding 供應商決定用 Voyage AI**：整個專案盡量留在 Anthropic 生態系內——Claude 負責生成、Voyage AI 負責 embedding。要注意 Claude（Anthropic）本身不提供 embedding API，**Voyage AI 是 Anthropic 官方推薦搭配的獨立合作夥伴**（不是 Anthropic 自家產品，但為官方指定首選），呼叫方式一樣是打 API，跟前面第二堂「直接打 API」的作法完全吻合。若 n8n 沒有 Voyage AI 專用節點，第三堂就用 n8n 的 HTTP Request 節點直接呼叫，效果相同。

> 🔧 **動態資料為什麼選 Supabase**：Context 除了靜態知識（RAG）之外，還有帳務／帳戶狀態這類會變動的「動態資料」，本質上就是存在資料庫裡。Supabase 是雲端代管的 Postgres，免費方案就夠教學規模用，走的是雲端優先、不自架的原則，跟 n8n Cloud、Qdrant Cloud 一致。第二堂開帳號建表，第三堂讓帳務 Agent 用 n8n 節點查詢。

> 🔧 **為什麼不讓 n8n 是唯一路徑**：n8n（甚至 Voiceflow）都可能被更新的工具取代，不希望學員留下「查資料只能靠 n8n」的印象。第二堂先用 Postman／curl 直接呼叫 Voyage AI 與 Qdrant 動手做一次，讓學員懂 RAG 的本質就是兩個獨立 HTTP API，第三堂才示範 n8n 節點只是包住同一組呼叫的外殼。

## 工具清單

| 分類 | 工具 | 用途 |
| --- | --- | --- |
| 自動化平台 | n8n Cloud | 核心後端邏輯、工作流編排、Webhook／OAuth 整合（第三堂才開帳號） |
| 語言模型 | Claude 3.5 Sonnet | 高邏輯工作流、意圖判斷、RAG 回覆生成 |
| 語言模型 | GPT-4o | 與 Claude 協作、部分任務比較與備援 |
| 開發輔助 | Claude Code／Cursor | 自然語言微調、生成假資料，維持 No-code 體驗 |
| API 測試 | Postman／curl | 第二堂直接呼叫 Voyage AI、Qdrant，動手做一次 RAG 的底層原理 |
| Embedding | Voyage AI | 文字轉向量，Anthropic 官方推薦的合作夥伴（Anthropic 自己不提供 embedding API） |
| 對話前端 | Voiceflow | 設計對話流程，分階段部署網頁／WhatsApp／電話三通路 |
| 向量資料庫 | Qdrant（或 Pinecone） | 儲存 Blazz 合約與 FAQ 的 embedding，供 RAG 檢索 |
| 關聯式資料庫 | Supabase | 雲端 Postgres，存帳務／帳戶狀態等動態資料，第二堂建表、第三堂讓帳務 Agent 查詢 |
| 團隊協作 | Slack | Blazz 內部 Human-in-the-loop 真人審核介入 |
| Email 服務 | n8n Email／SMTP 節點 | 自動寄送客服表單與通知 |
| 本機備課環境 | Docker | 自架 n8n 練習 Advanced AI（LangChain）節點 |

## 備課策略

- 利用本機端 Docker 架設 n8n 進行踩坑練習
- 熟練 Advanced AI（LangChain）節點的資料流動
- 結合全端經驗與 AI 工具快速搭建測試用的後端 API
- 目標：帶領學員實作時，能順暢展現系統整合的真實感
