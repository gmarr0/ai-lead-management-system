# 🔧 AI-Powered Lead Management System
### Built for a Local Welding Training Business

![Workflow](assets/workflow.svg)

---

## Overview

A fully automated, AI-powered lead capture and response system built for a local welding training company. When a prospective student or client submits an inquiry through the branded web form, the system:

- **Classifies the lead** using a local AI model
- **Generates a personalized response** tailored to their inquiry type
- **Logs the lead** to a live Google Sheet dashboard
- **Sends a professional branded email** within seconds
- **Pushes an instant notification** to the owner's phone via Pushover
- **All traffic secured** through a Cloudflare Tunnel (HTTPS, zero exposed ports)

Zero SaaS fees. Fully self-hosted. Runs 24/7 without human intervention.

---

## Live Form Preview

![Form Preview](assets/form-preview.svg)

---

## Automated Email Responses

![Email Preview](assets/email-preview.svg)

---

## How It Works

```
Form Submission
      │
      ▼
AI Classification (Ollama / LLaMA 3)
      │
      ├── Beginner  (MIG / STICK)
      ├── Advanced  (TIG)
      ├── Client    (Local Welding Work)
      ├── Kids      (Workshop Parents)
      └── Custom    (General Inquiries)
            │
            ▼
    Google Sheets Log  +  Pushover Alert  +  Branded Email
```

### Pipeline Steps

| Step | Node | What it does |
|------|------|-------------|
| 1 | n8n Form Trigger | Captures name, phone, email, class interest, message |
| 2 | Basic LLM Chain | Sends inquiry to local Ollama AI for classification |
| 3 | Code in JavaScript | Parses AI JSON output, extracts category + response |
| 4 | Edit Fields | Structures clean data fields for downstream nodes |
| 5 | Append to Google Sheets | Logs full lead record to live dashboard |
| 6 | Pushover | Sends instant push notification to owner's phone |
| 7 | Switch (5 routes) | Routes to the correct email based on AI category |
| 8 | Send an Email (×5) | Delivers personalized branded HTML email to lead |

---

## The 5 Lead Categories

| Category | Triggered By | Email Tone |
|----------|-------------|------------|
| **Beginner** | MIG or STICK selected | Welcoming, encouraging, highlights real job-site training |
| **Advanced** | TIG selected | Focused, professional, emphasizes precision and career growth |
| **Client** | Local Client Work selected | Business-forward, owner follows up personally |
| **Kids** | Kids WorkShop selected | Warm to parents, emphasizes safety and fun |
| **Custom** | Unclear inquiry | Friendly, personal follow-up promised |

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation Engine | [n8n](https://n8n.io) (self-hosted) |
| AI Model | [Ollama](https://ollama.ai) + LLaMA 3 (local, on-device) |
| Secure Tunnel | [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/) |
| Lead Database | Google Sheets (live dashboard) |
| Push Notifications | [Pushover](https://pushover.net) |
| Email Delivery | Gmail via SMTP |
| Server | Self-hosted (local machine) |

---

## Security

All public traffic is routed through a **Cloudflare Tunnel**:

- ✅ HTTPS encrypted end-to-end
- ✅ Server IP never exposed
- ✅ No open firewall ports required
- ✅ Protected by Cloudflare's global network
- ✅ Lead data and personal info secured in transit

The AI model (Ollama) runs **entirely on-device** — no lead data is ever sent to an external AI API.

---

## Key Results

- ⚡ Lead response time: **under 30 seconds** from form submission to inbox
- 📊 100% of leads automatically logged — nothing falls through the cracks
- 📱 Owner gets a push notification for every lead in real time
- 💰 **$0/month** in automation software costs — fully self-hosted open source stack
- 🔒 Enterprise-grade security on a small business budget

---

## Project Structure

```
/
├── assets/
│   ├── workflow.svg          # Animated pipeline diagram
│   ├── form-preview.svg      # Form UI illustration
│   └── email-preview.svg     # Email template preview
├── docs/
│   └── architecture.md       # Detailed architecture notes
└── README.md
```

---

## About This Project

Built as part of the **JPARO Systems** portfolio — a local automation and AI systems practice building real tools for real small businesses.

This system was designed, built, tested, and deployed in a single session — demonstrating that enterprise-grade lead automation doesn't require expensive SaaS tools or a large development team.

---

> *"Every future client gets their own subdomain and you control the whole stack. That's a real business."*

---

**JPARO Systems** · AI Automation · Self-Hosted Infrastructure · Small Business Solutions
