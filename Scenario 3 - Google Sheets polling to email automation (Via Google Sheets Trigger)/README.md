# 📬 Scenario 3: New Users onboarding Email Generation Via Google form/Sheet Trigger

An asynchronous, fail-safe automation pipeline that triggers directly from Google Sheets updates, processes applicant submissions through Google Gemini LLM, and dispatches personalized onboarding emails.

---

## 💡 The "Mailbox" Architecture Concept

Unlike synchronous webhooks that fail if the n8n host server is offline or experiencing downtime, this workflow implements a **persistent buffer queue (Polling Trigger)**:

1. **Persistent Buffer:** Google Forms automatically syncs submissions straight into Google Sheets natively on Google’s infrastructure.
2. **Offline Tolerance:** If the local Docker host or n8n instance is offline, submissions safely queue up inside the spreadsheet.
3. **Catch-Up Processing:** The moment n8n restarts, the **Google Sheets Trigger** detects all unprocessed `rowAdded` events and batch-processes them sequentially without data loss.

---

## 🔄 Workflow Pipeline

```text
[Google Form] ──(Native Sync)──► [Google Sheet]
                                       │
                              (rowAdded Trigger)
                                       ▼
                       [Basic LLM Chain + Gemini]
                                       │
                               (Custom Prompt)
                                       ▼
                              [Send Email (SMTP)]
