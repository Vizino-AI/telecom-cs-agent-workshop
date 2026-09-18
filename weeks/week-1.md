# 第一堂：認識 Agent 三大要素：Context, Tool, Model

[← 回課程總覽](../README.md)

## 課程目標

建立「Agent = Model + Tool + Context」心智模型，學會判斷客服情境裡哪些資訊該放哪一塊。

## 開通帳號

無新帳號需求（n8n／Qdrant／Voyage AI／Supabase 都留到第二、三堂才開，見下方備註）。

## 需要的背景知識

- **API 是什麼**：串接外部系統的接口，Tool 為什麼要透過 API
- **No-code 自動化平台的概念**：為什麼用 n8n 取代寫程式

## 課堂內容

- 開場 15 分鐘：專案目標、三大要素框架、五堂課地圖
- 用 Blazz 情境拆解 Model／Tool／Context（Model 選型分工：Claude 處理高邏輯、GPT-4o 協作；分清楚哪些判斷交給 Model、哪些用節點寫死規則）
- 準備 Blazz 假資料（方案費率、合約、FAQ），標出屬於 Context 還是 Tool
- 畫第一版 Agent 架構圖（先框出 Model／Tool／Context 三塊，再細化）

### 90 分鐘 Rundown

| 時間 | 內容 |
| --- | --- |
| 0:00–0:15 | 開場總覽：專案目標、Agent 三大要素框架、五堂課地圖 |
| 0:15–0:40 | 用 Blazz 情境拆解三要素：Model 的重點是選型分工，以及哪些判斷交給 Model、哪些用節點寫死規則 |
| 0:40–1:10 | 準備 Blazz 假資料，標出屬於 Context 還是 Tool 的資料 |
| 1:10–1:30 | 畫出第一版 Agent 架構圖、交代作業 |

> n8n Cloud 註冊與介面導覽移到第三堂開場，這一堂不碰 n8n——free trial 只有 14 天，且要到第三堂才真正開始建 workflow，帳號留到那天再開，避免試用期提前燒掉。

## 課程 Deliverables

- 一版 Agent 架構圖（Model／Tool／Context 三塊）
- 整理到一半、標好分類方向的假資料

## 課後練習

把假資料整理成乾淨 JSON／CSV，並標出「哪些屬於 Context、哪些屬於 Tool 該查的資料」（可參考 [scenarios.md](../scenarios.md) 的三個核心客服情境範例）。

---

[下一堂：建立 Context →](week-2.md)
