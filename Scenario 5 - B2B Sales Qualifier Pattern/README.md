# 🎯 B2B Sales Lead Qualifier & Automated Routing

An event-driven lead qualification workflow that captures form submissions via webhooks, acknowledges applicants with an instant welcome email, and validates lead quality by filtering and saving only verified business domains into a Google Sheets CRM.

---

## 🔄 Workflow Architecture

```text
[Google Form + Apps Script]
           │
           ▼ (HTTP POST via ngrok)
       [Webhook]
           │
           ▼
     [Send Email] (Immediate welcome acknowledgement)
           │
           ▼
      [If Node] (Domain verification: Doesn't Contains @gmail.com?)
      ├──► True (Business Domain):  [Append row in sheet] ──► Qualified Lead Saved
      └──► False (Public Webmail):  [Drop / No Action]   ──► Excluded from CRM
