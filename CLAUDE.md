# Project: Blazz 電信客服 AI Agent 教學專案

## 背景

本專案是 Katness 規劃的一對一教學專案：帶學員從零打造一個貼近真實電信業客服情境的 Multi-agent AI 客服系統（虛構電信公司 **Blazz**）。

課程總覽、專案目標與定調在 [`README.md`](./README.md)；每堂 90 分鐘 Rundown、開通帳號、背景知識、Deliverables、課後練習拆在 [`weeks/`](./weeks/) 底下一堂一個檔案；系統架構與流程圖在 [`architecture.md`](./architecture.md)；三個核心客服情境範例在 [`scenarios.md`](./scenarios.md)；工具選型與費用方案在 [`tools.md`](./tools.md)。**開始任何跟這個教學專案相關的任務前，先讀 `README.md`。**

學員的真實姓名、背景與商業條件（價格、堂數、實際上課日期）記在本機的 `student.local.md`——這個檔案被 `.gitignore` 排除，不進版控、不會出現在 GitHub repo 裡。README／weeks／CLAUDE.md 裡一律用「學員」稱呼，**不要把學員的真實姓名或身分細節寫進任何會進版控的檔案**。需要商業條件或日期時，去讀 `student.local.md`（若不存在，先跟 Katness 要）。

## 技術棧與慣例

- 核心自動化平台：**n8n Cloud**（No-code，靠 Webhook／OAuth 授權，不架自己的伺服器）—— free trial 只有 14 天，**帳號留到第三堂才開**（第一、二堂不碰 n8n，避免試用期提前燒掉）
- 語言模型：**Claude 3.5 Sonnet**（高邏輯工作流、意圖判斷、RAG 回覆生成）＋ **GPT-4o**（協作／備援）
- 對話前端：**Voiceflow**，分階段串接 —— 第四堂課堂先做網頁，WhatsApp 與電話排進第四堂的回家作業由學員自行串接
- 向量資料庫／RAG：**Qdrant**（或 Pinecone）＋ **Voyage AI**（embedding，Anthropic 官方推薦的合作夥伴——Anthropic 自己不提供 embedding API，盡量把整個技術棧留在 Anthropic 生態系內）；教學上刻意**不讓 n8n 是唯一路徑**——第二堂先用 Postman／curl 直接呼叫 Voyage AI 與 Qdrant 動手做一次，讓學員懂 RAG 的本質就是兩個獨立 HTTP API，第三堂才示範 n8n 節點只是包住同一組呼叫的外殼。原因：n8n（甚至 Voiceflow）都可能被更新的工具取代，不希望學員留下「查資料只能靠 n8n」的印象
- 動態資料：**Supabase**（雲端 Postgres，免費方案）——存帳務／帳戶狀態這類會變動的資料；教學上偏好雲端代管服務勝過 self-hosted，跟其他工具（n8n Cloud、Qdrant Cloud、Voiceflow）的雲端優先原則一致，第二堂開帳號建表、第三堂讓帳務 Agent 查詢
- 真人介入（Human-in-the-loop）：**Slack**（Blazz 內部客服／工程團隊）
- 開發輔助：Claude Code／Cursor —— 目的是維持整體 **No-code 實作體驗**，除非學員確實需要，避免產出之後要自己維護的大量自訂程式碼；生成的東西應該是「學員看得懂、能自己改」的等級
- 雖標榜 no-code，仍需要基本軟體架構知識（API、HTTP/HTTPS、JSON、Webhook 等）——`weeks/*.md` 每堂都列了「需要的背景知識」欄位，同一個概念在多堂課會用到就重複列出

## 虛構情境設定

- 電信公司：**Blazz**
- AI 客服代理人暱稱：**Blake**（Voiceflow 對話前端與所有情境範例中，Agent 都以「Blake」的身份跟客戶對話）
- 三個核心客服劇本（詳見 [`scenarios.md`](./scenarios.md)）：
  1. 帳務查詢與方案推薦（Billing & Upsell）—— API 查詢 + 邏輯判斷
  2. 網路斷線技術排解（Tech Support）—— RAG + Slack Human-in-the-loop
  3. 解約退費與客訴挽留（Cancellation & Retention）—— 情緒偵測 + 挽留話術 + Email
- 設計假資料、測試案例、demo 情境時，優先參考這三個劇本

## 給 Claude Code 的提醒

- 這是**教學專案**：產出的假資料、n8n workflow 範例、prompt 草稿等，複雜度要「適合現場帶著學員一起看懂、一起改」，不要過度工程化或引入用不到的框架
- 修改課綱、系統設計或情境時，同步更新對應的檔案（`README.md` / `weeks/*.md` / `architecture.md` / `scenarios.md` / `tools.md`），不要讓文件之間的資訊兜不起來
- 內容原本彙整在單一的 `cx-agent-planning.md`，2026-09-18 拆成 `README.md` ＋ `weeks/` ＋ `architecture.md` ＋ `scenarios.md` ＋ `tools.md` 多檔架構，並把學員身分／商業條件移到不進版控的 `student.local.md`，方便發布到公開的程式碼託管平台
- 任何牽涉費用、堂數、時程的變動，先跟 Katness 確認；且一律寫進 `student.local.md`，不要寫進會進版控的檔案
