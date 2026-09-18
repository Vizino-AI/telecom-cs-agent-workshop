# 第四堂：End-to-end 串接（前端先只做網頁、後端、Logging）

[← 回課程總覽](../README.md)

## 課程目標

把整個系統接成一個真人能用的網頁客服，並建立看得懂系統在做什麼的 Logging。

## 開通帳號

- **Voiceflow**：有免費方案（功能／用量有限，教學規模夠用），正式上線或用量變大時可能要升級付費方案
- **Slack**：免費建立 workspace 即可，Human-in-the-loop 用到的功能免費版就夠
- Email／SMTP：沿用現有 email 帳號或 n8n 內建節點，通常不用另外開新帳號
- （課後作業會用到）**Twilio**：WhatsApp／電話串接需要，有免費試用額度，正式使用電話號碼／發送量需月費＋用量計費

## 需要的背景知識

- **Webhook（雙向）**：Voiceflow 前端呼叫 n8n 後端、n8n 再回覆前端
- **SMTP／Email 協定基本概念**：為什麼要設定寄件伺服器
- **Log／事件紀錄的基本概念**：誰在什麼時候做了什麼

## 課堂內容

- 複習作業與交接測試結果
- 前端：用 Voiceflow 設計對話介面，**第一版先只串接「網頁」一個通路（Web Widget）**，把完整流程跑通再擴充其他通路
- 後端：Email 客服表單自動寄送、Slack Human-in-the-loop（Blazz 內部真人審核介入）
- Logging：設計對話與決策的紀錄機制（誰問了什麼、Agent 判斷了什麼、有沒有轉真人），方便之後除錯與優化
- 把網頁前端、後端、Logging 串成一條完整的 end-to-end 流程並實測

### 90 分鐘 Rundown

| 時間 | 內容 |
| --- | --- |
| 0:00–0:10 | 複習作業與交接測試結果 |
| 0:10–0:35 | 前端：Voiceflow 設計對話介面，先串接「網頁」一個通路 |
| 0:35–1:00 | 後端：Email 客服表單、Slack Human-in-the-loop 設計 |
| 1:00–1:20 | Logging 設計，串成完整 end-to-end 流程並實測 |
| 1:20–1:30 | 交代作業（記錄坑點；回家自行串接 WhatsApp／電話並測試一致性；設計奧客情境腳本、脆弱環節） |

## 課程 Deliverables

一個能在網頁上對話、串到後端（Email＋Slack）並有 Logging 的 end-to-end demo。

## 課後練習

1. 測試網頁版對話流程，記錄串接時遇到的坑
2. **回家自行把同一套 Voiceflow 對話邏輯串接 WhatsApp（WhatsApp Business API／Twilio）與電話／IVR 通路**，測試網頁／WhatsApp／電話三個通路行為是否一致，處理通路特有的差異（例如電話沒有畫面、WhatsApp 訊息長度限制）——原本規劃成獨立一堂課，現改為課後自行練習，上課時間留給 Hardening
3. 設計 3–5 個奧客情境腳本，並列出目前系統最脆弱的 3 個環節

---

[← 上一堂：Multi-agent 設計與建立工作流程](week-3.md) ｜ [下一堂：Hardening →](week-5.md)
