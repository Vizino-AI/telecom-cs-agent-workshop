# 第三堂：Multi-agent 設計與建立工作流程

[← 回課程總覽](../README.md)

## 課程目標

學會用 n8n，把多個專責 Agent 串成一個會分流、會交接的工作流程。

## 開通帳號

- **n8n Cloud**：14 天免費試用，到期若要續用需付月費（實際方案與費用視當時報價而定）

## 需要的背景知識

- **Webhook 是什麼**：n8n 如何接收外部觸發
- **條件判斷／流程控制的邏輯**：Switch／Set 節點背後其實是 if-else
- **呼叫 REST API 查資料庫的概念**：串接第二堂建好的 Supabase

## 課堂內容

- 註冊 n8n Cloud、環境與介面導覽
- 對照一下：n8n 的 Embeddings／Vector Store 節點，做的就是上一堂用 Postman／curl 打過的同一組 API——讓學員看懂節點是外殼，不是黑盒子
- 複習作業、討論 RAG 測試結果
- Multi-agent 架構設計：為什麼要拆成多個 Agent（意圖分流、技術客服、帳務客服）
- 用 n8n 的 Switch／Set 節點建立意圖分流骨架
- 幫每個子 Agent 決定它專屬的 Context 與 Tool（例如帳務 Agent 用 n8n 節點查第二堂建好的 Supabase 資料表）
- 串起完整的 Multi-agent 工作流程，並用簡單案例測試交接是否順暢

### 90 分鐘 Rundown

| 時間 | 內容 |
| --- | --- |
| 0:00–0:10 | 註冊 n8n Cloud、環境與介面導覽 |
| 0:10–0:20 | 對照 n8n 節點 vs 上一堂手動打的 API：Embeddings／Vector Store 節點做的就是同一組呼叫 |
| 0:20–0:40 | Multi-agent 架構設計：為什麼拆成多個 Agent、客服流程設計方法論 |
| 0:40–1:00 | 用 Switch／Set 節點建立意圖分流骨架 |
| 1:00–1:20 | 幫每個子 Agent 決定專屬 Context 與 Tool（帳務 Agent 查第二堂建好的 Supabase），串起完整工作流程 |
| 1:20–1:30 | 測試跨 Agent 交接情境、交代作業 |

## 課程 Deliverables

n8n 裡一條能動的 Multi-agent workflow（意圖分流 ＋ 對應 Context／Tool ＋ RAG 節點對接 ＋ 帳務 Agent 查得到 Supabase 假資料）。

## 課後練習

設計 3 個跨 Agent 的測試情境（例如先問技術問題、又轉問帳務），記錄交接是否正確。

---

[← 上一堂：建立 Context](week-2.md) ｜ [下一堂：End-to-end 串接 →](week-4.md)
