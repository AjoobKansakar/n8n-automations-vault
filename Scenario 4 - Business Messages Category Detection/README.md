# 🧭 Scenario 4: Customer Feedback Category & Routing Automation

An automated AI-driven classification pipeline that processes incoming customer feedback, translates multilingual messages into English, summarizes sentiment, and dynamically routes each item to the appropriate departmental queue using rule-based switching.

---

## 🔄 Workflow Architecture

```text
[Manual / Batch Trigger]
           │
           ▼
[Code Node (JavaScript)] (Ingest feedback array)
           │
           ▼
[Basic LLM Chain + Gemini] (Summarize, translate, & classify)
           │
           ▼
     [Switch Node] (Rule-based condition routing)
      ├──► Output 0: SALES TEAM
      ├──► Output 1: REVIEWS
      ├──► Output 2: SPAM
      └──► Output 3: COMPLAINTS
