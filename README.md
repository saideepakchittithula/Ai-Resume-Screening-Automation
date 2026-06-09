
<div align="center">
<img width="1774" height="887" alt="title" src="https://github.com/user-attachments/assets/5b8bac5f-eec0-4da6-bcb8-929f9de4464f" />


**An end-to-end recruitment automation pipeline that handles resume screening, AI-driven interviews, candidate scoring, and email notifications — without manual intervention.**

[![n8n](https://img.shields.io/badge/Built%20with-n8n-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io)
[![Gemini](https://img.shields.io/badge/AI-Google%20Gemini%202.5%20Pro-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://deepmind.google/technologies/gemini/)
[![Google Sheets](https://img.shields.io/badge/Data-Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://sheets.google.com)
[![Gmail](https://img.shields.io/badge/Email-Gmail%20API-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](https://gmail.com)
[![JavaScript](https://img.shields.io/badge/Code-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

</div>

---

## 📋 Project Overview

This project automates the initial recruitment pipeline for an **AI Automation Engineer** role using n8n, Google Gemini, Google Workspace APIs, and JavaScript.

The system takes a candidate from **application submission to qualification decision** entirely without human involvement — covering resume analysis, JD matching, personalized interview question generation, answer evaluation, scoring, and automated email communication.

Built as a portfolio project to demonstrate real-world AI automation engineering skills including LLM integration, multi-agent workflow design, structured output parsing, and API orchestration.

---

## 📌 Problem Statement

Initial recruitment screening is one of the most time-intensive and repetitive responsibilities in talent acquisition. Recruiters routinely:

- Read through large volumes of resumes that do not meet the job requirements
- Write and send the same screening questions to every shortlisted candidate
- Manually score responses with no consistent rubric
- Track candidate progress by updating spreadsheets by hand
- Send follow-up and rejection emails one at a time

This creates bottlenecks, inconsistency in evaluation, and limits how many candidates a small team can realistically process. The problem becomes harder to manage as application volume grows.

---

## 💡 Solution

The AI-Powered Recruitment Automation System replaces the manual initial screening process with an automated two-phase pipeline:

- **AI Resume Screening** — Gemini 2.5 Pro reads each resume, extracts skills and experience, and scores the candidate against the Job Description
- **JD Matching** — Each resume receives a structured match score (0–1) with reasoning, used to route candidates automatically
- **Dynamic Interview Question Generation** — Qualified candidates receive 5 personalized interview questions generated from their own resume content
- **AI-Based Answer Evaluation** — Candidate responses are evaluated by the AI and scored per question with structured output
- **Automated Score Calculation** — JavaScript aggregates individual scores into a total, which determines final qualification status
- **Google Sheets Integration** — All candidate data, scores, notes, and statuses are written to a live tracking sheet in real time
- **Automated Email Notifications** — Qualified and rejected candidates both receive appropriate emails automatically via Gmail API

---

## ✨ Key Features

- Two-phase pipeline: resume screening followed by AI interview round
- Conditional routing — candidates branch based on JD match score
- Structured JSON output from all AI agents using Output Parsers
- Personalized interview questions tailored to each candidate's resume
- Per-question AI scoring with total score aggregation in JavaScript
- Full candidate tracking in Google Sheets with no manual data entry
- Automated Gmail notifications at every decision point

---

## 🔄 Workflow Overview

| Stage | Node / Tool | Description |
|-------|-------------|-------------|
| 1 | Form Trigger | Candidate submits name, email, phone, resume (PDF), years of experience |
| 2 | Google Drive | Resume uploaded and stored; file ID extracted |
| 3 | Google Sheets | Candidate record created with basic details |
| 4 | Google Drive + PDF Extractor | Resume downloaded and parsed to plain text |
| 5 | AI Agent (Gemini) | Resume analysed against JD; match score (0–1) returned |
| 6 | IF Node | Score ≥ threshold → Phase 2; below threshold → rejection email |
| 7 | AI Agent1 (Gemini) | Generates 5 personalised interview questions |
| 8 | Form | Dynamic interview form delivered to candidate |
| 9 | JavaScript | Formats answers; prepares scoring payload |
| 10 | AI Agent2 (Gemini) | Evaluates each answer; scores out of 10 |
| 11 | IF1 Node | Total score ≥ threshold → qualified; below → not qualified |
| 12 | Google Sheets + Gmail | Results stored; qualification or rejection email sent |

---

## 🏗️ System Architecture

```
PHASE 1 — RESUME SCREENING
──────────────────────────────────────────────────────────

Form Submission
    │
    ▼
Upload to Google Drive → Extract Resume ID
    │
    ▼
Create / Update Row in Google Sheets
    │
    ▼
Download Resume → Extract PDF Text
    │
    ▼
AI Agent (Gemini + Structured Output Parser)
    │   Scores resume against Job Description (0–1)
    │
    ▼
IF Score ≥ threshold?
    ├── YES → Update Sheet (Qualified) → Phase 2
    └── NO  → Update Sheet (Rejected) → Rejection Email (Gmail)


PHASE 2 — AI INTERVIEW
──────────────────────────────────────────────────────────

AI Agent1 (Gemini + Structured Output Parser)
    │   Generates 5 personalised interview questions
    │
    ▼
Dynamic Interview Form → Candidate submits answers
    │
    ▼
JavaScript → Formats responses, prepares scoring input
    │
    ▼
AI Agent2 (Gemini + Structured Output Parser)
    │   Evaluates each answer, scores out of 10
    │
    ▼
IF Total Score ≥ threshold?
    ├── YES → Update Sheet (Final Qualified) → Congrats Email (Gmail)
    └── NO  → Update Sheet (Final Rejected) → Rejection Email (Gmail)
```

---
## 📁 Repository Structure

```text
AI-Recruitment-Automation
│
├── README.md
├── workflow
│   └── recruitment_automation.json
│
├── screenshots
│   ├── step1_candidate_form.png
│   ├── step2_n8n_workflow.png
│   ├── step3_ai_questions.png
│   ├── step4_google_sheet.png
│   └── step5_qualification_email.png
│
└── docs
    └── architecture_diagram.png
```
---

## 📸 Demo

### Candidate Application Form
### Step-1
<img width="1536" height="1024" alt="ChatGPT Image Jun 9, 2026, 10_57_49 PM" src="https://github.com/user-attachments/assets/96d3f410-e91d-4dd3-a4bd-c0d553b96705" />


### n8n Automation Workflow
### Step-2
![n8n Workflow](screenshots/step2_n8n_workflow.png)


### AI Interview Question Generation
### Step-3
<img width="1536" height="1024" alt="step3" src="https://github.com/user-attachments/assets/df77a14b-195d-41e8-bede-dafc485cddea" />





### Candidate Evaluation Dashboard (Google Sheets)
### Step-4
<img width="1536" height="1024" alt="step4" src="https://github.com/user-attachments/assets/32735f59-c842-4649-b14c-d47e82e5fbc2" />


### Automated Qualification Email
### Step-5
<img width="1536" height="1024" alt="step5" src="https://github.com/user-attachments/assets/c8269d33-3f09-4a3f-8558-2f4ab4b09b64" />


---

## 🛠️ Tech Stack

| Category | Tool / Technology |
|----------|------------------|
| **Workflow Automation** | n8n (self-hosted) |
| **AI / LLM** | Google Gemini 2.5 Pro via LangChain nodes |
| **Output Parsing** | n8n Structured Output Parser (JSON schema) |
| **File Storage** | Google Drive API |
| **Data Tracking** | Google Sheets API |
| **Email Automation** | Gmail API |
| **Scripting** | JavaScript (score aggregation, data formatting) |
| **Integration** | Webhooks, REST APIs, OAuth2 |
| **Prompt Design** | Structured prompt engineering for consistent AI output |

---

## 🚀 Key Automation Logic

### Resume Qualification

Candidates are evaluated against the job description using Google Gemini. The AI returns:

* Match Score (0–1)
* Matching Skills
* Missing Skills
* Qualification Reasoning

### Interview Evaluation

Each candidate answer is scored from 0–10 based on:

* Technical Accuracy
* Problem Solving Ability
* Communication Clarity
* Relevant Experience

### Final Decision

```text
Total Score = Q1 + Q2 + Q3 + Q4 + Q5

If Total Score ≥ 30
    → Qualified

Else
    → Rejected
```

The final status is automatically updated in Google Sheets and an email notification is sent through Gmail.

---

## 🔮 Planned Enhancements

- [ ] AI voice interview round (ElevenLabs + Whisper)
- [ ] Multi-round interview automation
- [ ] ATS integration
- [ ] Real-time analytics dashboard (Looker Studio)
- [ ] WhatsApp notifications via Twilio
- [ ] Multi-job posting support

---

## 🧠 Skills Demonstrated

| Domain | Skills |
|--------|--------|
| **AI & LLM** | Prompt Engineering · Structured Output Parsing · Multi-Agent Design · Google Gemini API |
| **Automation** | n8n · Workflow Orchestration · Conditional Logic · Event-Driven Architecture |
| **API Integration** | Google Drive API · Google Sheets API · Gmail API · REST APIs · OAuth2 · Webhooks |
| **Development** | JavaScript · JSON Schema · Data Transformation · Process Automation |
| **Domain** | Recruitment Workflow Automation · HR Tech · End-to-End Pipeline Design |

---

## 👨‍💻 Author

**Sai Deepak Chittithula**  
AI Automation Engineer — specialising in n8n, LLM integration, and intelligent workflow design

📧 [saideepakchittithula7898@gmail.com](mailto:saideepakchittithula7898@gmail.com)

---

