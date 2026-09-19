# TalentDossier — AI-Powered Autonomous Recruiter
> **HackDevengers Open Innovation Hackathon 2026**  
> *Built in 24 hours. Solves a real hiring problem. Runs autonomously.*

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Vercel-black?logo=vercel)](https://hack-devengers-hackathon-lyart.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?logo=github)](https://github.com/akshat-lakhera/hack-devengers-hireflow)

> 🌐 **Live Demo**: [https://hack-devengers-hackathon-lyart.vercel.app](https://hack-devengers-hackathon-lyart.vercel.app)

---

## The Problem We Solved

Hiring is broken. Recruiters at fast-growing companies receive 200–500 resumes per role. Manual screening takes 6–8 hours per batch. Bias creeps in. Strong candidates get missed because someone got fatigued on resume #187.

**TalentDossier automates the entire screening pipeline** — from the moment a candidate applies to the moment a decision email lands in their inbox — with one human checkpoint to keep accountability intact.

---

## What We Built

A **fully autonomous AI recruiting agent** with a continuous loop architecture:

```
Candidate Applies → Agent Detects (instantly) → Agent Evaluates (autonomously)
      → Agent Drafts Decision + Email → Recruiter Reviews (1 click) → Email Sent
```

No manual sorting. No spreadsheets. No missed candidates. The recruiter only touches the loop at the final step — review and approve.

---

## Live Demo / How to Run

```bash
git clone https://github.com/akshat-lakhera/hack-devengers-hireflow.git
cd hack-devengers-hireflow
npm install
npm run dev
# Open http://localhost:5173
```

**Quickest way to see the agent work (under 2 minutes):**
1. Open the app → click **"Autonomous Agent"** (top nav bar)
2. Click **"Activate Loop"** → **"Simulate Portal Inflow"**
3. Watch the agent autonomously process 3 candidates from LinkedIn, Greenhouse, and Indeed — scoring, classifying, and drafting emails for each — without you doing anything
4. Review each decision in the **Human Review Action Deck** → 1-click approve

---

## Key Features

### What the Agent Does Autonomously
- Monitors an application queue (career portal, webhooks from LinkedIn/Greenhouse/Lever/Indeed)
- Extracts candidate information from raw resume text or PDF
- Builds a dynamic execution plan per candidate batch (7-step DAG)
- Scores each candidate against a custom role blueprint (must-have skills, seniority, team type)
- Classifies each as: `Interview Ready` / `Needs Review` / `Rejected`
- Drafts personalized emails for each outcome
- Stages everything for 1-click human approval — nothing fires without recruiter sign-off

### AI Engine
- Supports **Groq LLaMA-3.3 70B**, **Google Gemini 1.5 Flash**, or **OpenAI GPT-4o-mini** — switch at runtime
- Falls back to a built-in deterministic rule engine when no API key is present — works offline, zero hallucination
- Every reasoning step is logged (Thought → Action → Observation) in a live terminal view

### Human-in-the-Loop Controls
- Staged decision queue — every AI classification requires recruiter approval before executing
- Full email preview before dispatch (subject + body)
- 1-click approve, dismiss, or batch approve all
- If SMTP credentials are missing: inline key capture modal with live connection test
- If recruiter closes without providing key: persistent "Email Not Sent" alert with candidate name + email on record

### Recruiter Workspace
- 3-column resizable workspace (like VS Code — drag the dividers)
- Deep-dive candidate dossier with verified evidence, interview probe questions, notes, audit trail
- Side-by-side comparison matrix for any 2 candidates
- Original resume viewer (PDF embed + full text with keyword highlighting)
- AI-powered recruiter copilot: type natural language, it executes workspace actions

### Email Automation
- Sends personalized acceptance, interview invite, shortlist, or rejection emails to candidate's email extracted from their resume
- Context-aware content: references the candidate's actual skills and projects in the email body
- Full dispatch log with delivery receipt IDs

---

## Technical Implementation

| Component | Technology |
|---|---|
| Frontend | React 19 + TypeScript + Vite |
| Agent Runtime | Custom ReAct (Reason+Act) loop + DAG Planner — written from scratch in TypeScript |
| AI Providers | Groq API, Google Gemini API, OpenAI API — all optional, switchable live |
| Storage (local) | IndexedDB — in-browser vector store, works offline, zero config |
| Storage (cloud) | Supabase PostgreSQL + pgvector — 384-dim semantic similarity search |
| Resume Parsing | pdfjs-dist — client-side, no server needed |
| Voice Interface | Web Speech API — TTS reads interview questions, STT captures answers |
| Email Dispatch | SMTP (Gmail App Password / SendGrid) |

**No backend server required.** The entire application — including the agent, vector storage, PDF parsing, and LLM orchestration — runs in the browser.

---

## Real-World Impact

**Time saved per hiring cycle:**
- Manual screening: ~6 hours per 100 resumes
- TalentDossier: ~4 minutes of recruiter time (just the approval click) for the same batch
- Agent processing: <10 seconds per candidate

**Who benefits:**
- Startups with small HR teams who can't afford ATS enterprise contracts
- Recruiters overwhelmed by volume during growth spurts
- Candidates — faster response time, less bias in initial screening

**Scalability:**
- Supabase pgvector backend scales to tens of thousands of candidates
- Agent daemon runs continuously — no batch jobs to schedule
- Webhook integration with Greenhouse, Lever, LinkedIn Apply, Indeed means it plugs directly into existing hiring stacks
- Role blueprints are portable — one recruiter can run 5 different roles in parallel

---

## Architecture: The Autonomous Loop

```
                    ┌──────────────────────────────────────────────────────┐
                    │                 AUTONOMOUS AGENT LOOP                │
                    │                                                      │
  Application  ──→  │  PERCEIVE              PLAN               ACT        │
  submitted         │  ────────              ────               ───        │
                    │  Detect new     →  Build 7-step     →  Execute each  │
  (Career portal,  │  application       DAG per batch       step in order  │
   LinkedIn,        │  from queue                                           │
   Greenhouse,      │                                                      │
   Indeed)          │                        ↓                             │
                    │               HUMAN GATE                             │
                    │               ──────────                             │
                    │               Stage decision    ←── Recruiter        │
                    │               for approval          reviews (1-click) │
                    │                    │                                 │
                    │               Approved?                              │
                    │               Yes ──→ Email sent to candidate        │
                    │               No  ──→ Dismissed, logged              │
                    └──────────────────────────────────────────────────────┘
```

---

## Submission

| | |
|---|---|
| **Project Title** | TalentDossier |
| **Team** | Devengers |
| **Hackathon** | HackDevengers Open Innovation Hackathon 2026 |
| **GitHub Repository** | [github.com/akshat-lakhera/hack-devengers-hireflow](https://github.com/akshat-lakhera/hack-devengers-hireflow) |
| **Domain** | AI / Autonomous Agents / HR Tech |
| **Tech** | React 19 · TypeScript · Groq · Gemini · OpenAI · IndexedDB · Supabase pgvector |
| **Built During** | 24-hour hackathon window |
