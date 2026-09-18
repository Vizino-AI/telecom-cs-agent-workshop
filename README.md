# Blazz 電信客服 AI Agent 教學專案

一個五堂制的實作教學專案：跳過生成式 AI 與代理式 AI 的基礎理論，直接動手打造一個貼近真實電信業客服情境的 Multi-agent AI 客服系統（虛構電信公司 **Blazz**），讓學員獲得完整落地一個真實產品的成就感。

## 專案目標與定調

- 目標對象：已經有基礎 AI 課程背景、想跳過理論直接動手做出真實產品的學員
- 教學定調：跳過 Gen AI 與 Agentic AI 的基礎理論講解，直接動手實作
- 成品：貼近真實商業需求的「電信公司 AI 客服代理人（Multi-agent）」
- 核心價值：讓學員獲得打造真實上線產品的極大成就感

## 虛構情境設定

- 電信公司：**Blazz**
- AI 客服代理人暱稱：**Blake**（Voiceflow 對話前端與所有情境範例中，Agent 都以「Blake」的身份跟客戶對話）

## 課程總覽

五堂課、每堂 90 分鐘，建議節奏是每週兩堂（例如週二、四）。每堂的完整內容（課程目標、開通帳號、背景知識、課堂內容、Deliverables、課後練習、分鐘級 Rundown）都拆到獨立檔案：

| 堂次 | 主題 | 連結 |
| --- | --- | --- |
| 第一堂 | 認識 Agent 三大要素：Context, Tool, Model | [weeks/week-1.md](weeks/week-1.md) |
| 第二堂 | 建立 Context（RAG 靜態知識 ＋ Supabase 動態資料） | [weeks/week-2.md](weeks/week-2.md) |
| 第三堂 | Multi-agent 設計與建立工作流程 | [weeks/week-3.md](weeks/week-3.md) |
| 第四堂 | End-to-end 串接（網頁前端、後端、Logging） | [weeks/week-4.md](weeks/week-4.md) |
| 第五堂 | Hardening（錯誤處理、Rate-limiting、資安、Scalability） | [weeks/week-5.md](weeks/week-5.md) |

> 這門課的實際上課日期、堂數費用等商業條件跟學員身分資訊，記錄在本機的 `student.local.md`（未進版控，不會出現在這個 repo 裡）。

## 其他文件

- [三個核心客服情境範例](scenarios.md) — 假資料與 demo 設計的參考劇本
- [客服流程設計與系統架構](architecture.md) — 意圖分流、Human-in-the-loop、前端三通路規劃
- [工具總覽與技術決策](tools.md) — 每個工具的用途、選型理由、費用方案

## 技術棧一覽

- 核心自動化平台：n8n Cloud（No-code）
- 語言模型：Claude 3.5 Sonnet ＋ GPT-4o
- Embedding：Voyage AI（Anthropic 官方推薦的合作夥伴）
- 向量資料庫：Qdrant（或 Pinecone）
- 動態資料：Supabase（雲端 Postgres）
- 對話前端：Voiceflow（網頁 → WhatsApp → 電話，分階段）
- 真人介入：Slack

細節與選型理由見 [tools.md](tools.md)。

## 給 Claude Code 的提醒

開始任何跟這個教學專案相關的任務前，先讀 [`CLAUDE.md`](CLAUDE.md)。
