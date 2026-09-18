# 第二堂：建立 Context

[← 回課程總覽](../README.md)

## 課程目標

懂 Context 的兩種樣貌——RAG 處理靜態知識、Supabase 處理動態資料——而且兩者都先直接打 API，不靠 n8n。

## 開通帳號

- **Qdrant Cloud**：免費（Free tier，永久額度）
- **Voyage AI**：新戶通常有免費試用額度，用完後轉為依用量計費
- **Supabase**：免費方案（Free tier，教學規模夠用），用量大或要更多功能才需升級付費
- Postman（可選）：免費版即可；用 curl 則完全不用開帳號

## 需要的背景知識

- **HTTP 協定基礎**：request／response、method（GET/POST）、endpoint、header、body
- **HTTPS 與 API Key／Bearer Token 驗證**：為什麼呼叫 API 要帶金鑰、資料為什麼要加密傳輸
- **JSON 資料格式**：API 溝通的共通語言
- **向量／Embedding 的概念**：語意搜尋
- **關聯式資料庫基本概念**：資料表、欄位、row（Supabase 用得到）

## 課堂內容

- 複習作業、Q&A
- Context 來源與形式：靜態知識 vs. 動態資料 vs. 對話歷史
- 向量資料庫概念快速說明，簡單比較 Qdrant／Pinecone（點到為止，不深入細節）
- **動手做 RAG，不透過 n8n**：Postman／curl 呼叫 Voyage AI，把 Blazz 合約／FAQ 轉向量存進 Qdrant，再用同一組 API 查詢測試一次
- **動手做動態資料**：開 Supabase，建一張簡單的假帳務／帳戶資料表（對應「動態資料」），把第一堂準備的帳務／方案假資料實際存進去

### 90 分鐘 Rundown

| 時間 | 內容 |
| --- | --- |
| 0:00–0:10 | 複習作業、Q&A |
| 0:10–0:20 | Context 來源與形式：靜態知識 vs. 動態資料 vs. 對話歷史 |
| 0:20–0:28 | 向量資料庫概念快速說明，簡單比較 Qdrant／Pinecone（點到為止） |
| 0:28–0:55 | 動手做：用 Postman／curl 直接呼叫 Voyage AI，把 Blazz 合約與 FAQ 轉成向量存進 Qdrant Cloud（不透過 n8n） |
| 0:55–1:10 | 動手做：用同一組 API 查詢，拿問題向量換回最相關原文，實際體驗 RAG 的檢索結果 |
| 1:10–1:25 | 動手做：開 Supabase，建一張簡單的假帳務／帳戶資料表，存進動態資料 |
| 1:25–1:30 | 交代作業 |

> **為什麼不直接用 n8n 做這段**：n8n 的 Embeddings／Vector Store 節點確實比手動打 API 更快上手，但目的是讓學員一開始就懂「這其實就是兩個 HTTP API」，而不是只會「在 n8n 裡拖節點查資料」——n8n 好用，但不是唯一的路，之後換掉也不影響對 RAG 原理的理解。第三堂會馬上把這組 API 換成 n8n 節點，讓學員看到節點只是包住同一件事的外殼。

## 課程 Deliverables

- 一個可查詢的 Qdrant collection，裝好 Blazz 合約／FAQ 的 embedding，API 測過能查到正確原文片段
- 一張裝好假帳務資料的 Supabase 資料表（第三堂帳務 Agent 會呼叫）

## 課後練習

列出 5 個測試問題與預期答案，抄出用 API 直接測出來的答錯或答不出來案例，並記錄是「Context 不足」還是「檢索方式」的問題。

---

[← 上一堂：認識 Agent 三大要素](week-1.md) ｜ [下一堂：Multi-agent 設計與建立工作流程 →](week-3.md)
