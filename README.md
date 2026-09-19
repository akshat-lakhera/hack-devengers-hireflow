# TalentDossier - AI-Powered Autonomous Recruiter
> **HackDevengers Open Innovation Hackathon 2026**
> *Built in 24 hours. Solves a real hiring problem. Runs autonomously.*

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Vercel-black?logo=vercel)](https://hack-devengers-hackathon-lyart.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?logo=github)](https://github.com/akshat-lakhera/hack-devengers-hireflow)

> **Live Demo**: https://hack-devengers-hackathon-lyart.vercel.app

---

## The Problem We Solved

Hiring is broken. Recruiters at fast-growing companies receive 200-500 resumes per role. Manual screening takes 6-8 hours per batch. Bias creeps in. Strong candidates get missed because someone got fatigued on resume #187.

**TalentDossier automates the entire screening pipeline** - from the moment a candidate applies to the moment a decision email lands in their inbox - with one human checkpoint to keep accountability intact.

---

## What We Built

A **fully autonomous AI recruiting agent** with a continuous loop architecture:

```
Candidate Applies -> Agent Detects (instantly) -> Agent Evaluates (autonomously)
      -> Agent Drafts Decision + Email -> Recruiter Reviews (1 click) -> Email Sent
```

No manual sorting. No spreadsheets. No missed candidates. The recruiter only touches the loop at the final step.

---

## Setup Instructions

### 1. Run Locally (Zero Config)

```bash
git clone https://github.com/akshat-lakhera/hack-devengers-hireflow.git
cd hack-devengers-hireflow
npm install
npm run dev
# Open http://localhost:5173
```

Two demo candidates (Liam Zhang + Priya Sharma) are auto-loaded on first run.

---

### 2. See the Agent Work (under 2 minutes)

1. Open the app -> click **"Autonomous Agent"** in the top nav
2. Click **"Activate Loop"** -> **"Simulate Portal Inflow"**
3. Watch the agent autonomously process 3 candidates from LinkedIn, Greenhouse, and Indeed - scoring, classifying, and drafting emails for each
4. Go to the **Human Review Action Deck** -> click **Approve** on any candidate

---

### 3. Enable Live AI Reasoning (Optional - Groq is free)

1. Get a free API key from https://console.groq.com
2. In the app: click the **AI model badge** in the top nav -> **AI Settings**
3. Paste your Groq API key -> **Save**

The agent now uses real LLaMA-3.3-70B reasoning instead of the rule engine.

---

### 4. Enable Real Email Dispatch (Optional - EmailJS free tier)

TalentDossier uses **EmailJS** to send real candidate emails from the browser. No backend server needed. Free tier: 200 emails/month.

**Setup (5 minutes):**

1. Create a free account at https://emailjs.com

2. **Add Email Service:**
   - Dashboard -> Email Services -> Add New Service -> Gmail
   - Authorize with your Gmail account
   - Copy the **Service ID** (e.g. `service_abc1234`)

3. **Create Email Template:**
   - Dashboard -> Email Templates -> Create New Template
   - Use these variables in your template:
     ```
     To: {{to_email}}
     Subject: {{subject}}
     Body: {{message}}
     ```
   - Copy the **Template ID** (e.g. `template_xyz5678`)

4. **Get Public Key:**
   - Top-right menu -> Account -> API Keys -> copy **Public Key**

5. **Connect to TalentDossier:**
   - In the app: click the **envelope icon** in the top nav
   - Fill in Service ID + Template ID + Public Key
   - Click **Test Connection** -> green checkmark = ready
   - Click **Save Changes**

Emails now send in real time when you approve candidates. Dispatch log appears in the Outbox tab.

---

## Key Features

### What the Agent Does Autonomously
- Monitors an application queue (career portal, webhooks from LinkedIn/Greenhouse/Lever/Indeed)
- Extracts candidate information from raw resume text or PDF
- Builds a dynamic 7-step execution plan (DAG) per candidate batch
- Scores each candidate against a custom role blueprint (must-have skills, seniority, team type)
- Classifies each as: `Interview Ready` / `Needs Review` / `Rejected`
- Drafts personalized emails for each outcome
- Stages everything for 1-click human approval - nothing fires without recruiter sign-off

### AI Engine
- Supports **Groq LLaMA-3.3 70B**, **Google Gemini 1.5 Flash**, or **OpenAI GPT-4o-mini** - switch at runtime
- Falls back to a built-in deterministic rule engine when no API key is present
- Every reasoning step is logged (Thought -> Action -> Observation) in a live terminal view

### Human-in-the-Loop Controls
- Staged decision queue - every AI classification requires recruiter approval before executing
- Full email preview before dispatch (subject + body)
- 1-click approve, dismiss, or batch approve all
- If EmailJS credentials are missing: inline key capture modal with live connection test

### Recruiter Workspace
- 3-column resizable workspace (drag the dividers)
- Deep-dive candidate dossier: verified evidence, interview probe questions, notes, audit trail
- Side-by-side comparison matrix for any 2 candidates
- Original resume viewer (PDF embed + full text with keyword highlighting)
- AI recruiter copilot: type natural language, it executes workspace actions

---

## Technical Implementation

| Component | Technology |
|---|---|
| Frontend | React 19 + TypeScript + Vite |
| Agent Runtime | Custom ReAct loop + DAG Planner - pure TypeScript, no framework |
| AI Providers | Groq API, Google Gemini API, OpenAI API - all optional, switchable live |
| Storage (local) | IndexedDB - in-browser vector store, works offline, zero config |
| Storage (cloud) | Supabase PostgreSQL + pgvector - 384-dim semantic similarity search |
| Resume Parsing | pdfjs-dist - client-side, no server needed |
| Voice Interface | Web Speech API - TTS reads interview questions, STT captures answers |
| Email Dispatch | EmailJS (real browser-to-email, 200/month free) |

No backend server required. The entire application runs in the browser.

---

## Real-World Impact

- Manual screening: ~6-8 hours per 100 resumes
- TalentDossier: ~4 minutes of recruiter time (just the approval clicks) for the same batch
- Agent processing: under 10 seconds per candidate

---

## Architecture: The Autonomous Loop

```
                    +--------------------------------------------------+
                    |              AUTONOMOUS AGENT LOOP               |
                    |                                                  |
  Application  -->  |  PERCEIVE          PLAN              ACT         |
  submitted         |  --------          ----              ---         |
                    |  Detect new    ->  Build 7-step  ->  Execute     |
  (LinkedIn,        |  application       DAG per batch    each step   |
   Greenhouse,      |  from queue                                      |
   Indeed)          |                        |                         |
                    |                   HUMAN GATE                     |
                    |                   ----------                     |
                    |               Stage decision  <-- Recruiter      |
                    |               for approval        reviews        |
                    |                    |                             |
                    |               Approved? Yes --> Email sent       |
                    |                         No  --> Dismissed        |
                    +--------------------------------------------------+
```

---

## Submission

| | |
|---|---|
| **Project Title** | TalentDossier |
| **Hackathon** | HackDevengers Open Innovation Hackathon 2026 |
| **Live Demo** | https://hack-devengers-hackathon-lyart.vercel.app |
| **GitHub** | https://github.com/akshat-lakhera/hack-devengers-hireflow |
| **Domain** | AI / Autonomous Agents / HR Tech |
| **Tech** | React 19, TypeScript, Groq, Gemini, OpenAI, IndexedDB, Supabase pgvector |
| **Built During** | 24-hour hackathon window |
