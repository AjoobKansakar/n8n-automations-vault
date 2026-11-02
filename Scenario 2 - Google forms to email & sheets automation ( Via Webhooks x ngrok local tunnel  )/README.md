# ⚡ User Onboarding Via Google Forms to Sheets & Email (Webhook integration)

An automated event-driven pipeline that captures new user registrations via Google Forms, logs applicant data to Google Sheets, and uses Google Gemini LLM to draft and send personalized onboarding emails in real time.

---

## 🔄 Workflow Architecture

```text
[Google Form / Webhook] 
       │
       ├──► [Google Sheets] (Append registration record)
       │
       └──► [Basic LLM Chain + Gemini] ──► [SMTP Email Node] (Send custom welcome email)
