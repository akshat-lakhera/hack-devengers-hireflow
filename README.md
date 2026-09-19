# TalentDossier (TD) — Autonomous Recruiter Intelligence Workspace
> **Built for the Devengers Hackathon 2026**  
> *Full-Stack Autonomous Applicant Screening, Evidence Grounding & Recruiter Workspace*

[![CI Quality Gate](https://github.com/akshat-lakhera/hack-devengers-hireflow/actions/workflows/ci.yml/badge.svg)](https://github.com/akshat-lakhera/hack-devengers-hireflow/actions/workflows/ci.yml)
[![Deploy to GitHub Pages](https://github.com/akshat-lakhera/hack-devengers-hireflow/actions/workflows/deploy.yml/badge.svg)](https://github.com/akshat-lakhera/hack-devengers-hireflow/actions/workflows/deploy.yml)

TalentDossier is an **Autonomous AI Recruiter Intelligence System** created for the **Devengers Hackathon 2026**. Built to eliminate manual applicant review and candidate hallucination, TalentDossier equips recruiters with an autonomous multi-step screening engine, client-side 384-dimensional vector similarity search, structured technical interview kits, and an active ReAct recruiter copilot that executes tools directly on the workspace.

---

## Workspace Showcase

### 1. Three-Column Recruiter Workspace
An interactive IDE-inspired recruiter dashboard featuring real-time candidate triage cards, grounded executive dossiers with project citations, and a quick actions rail.

![TalentDossier Recruiter Workspace](docs/screenshots/dashboard-workspace.png)

---

### 2. Autonomous Screener Agent (Multi-Step Pipeline Triage)
Autonomous agent that evaluates all candidates against role specifications, classifies them into decisive hiring stages (`Interview Ready`, `Needs Review`, `Rejected`), and logs immutable audit notes.

![Autonomous Screener Agent](docs/screenshots/autonomous-screener-agent.png)

---

### 3. Recruiter Agent Copilot (Workspace Tool Calling)
Grounded natural language recruiting agent capable of querying candidate resumes and executing real workspace actions (`compare_candidates`, `update_candidate_status`, `open_interview_kit`, `add_note`, `filter_pipeline`).

![Recruiter Agent Copilot](docs/screenshots/recruiter-copilot.png)

---

### 4. Head-to-Head Candidate Comparison Matrix
Side-by-side benchmarking matrix evaluating two candidates across match scores, experience, and differential technical requirements.

![Candidate Comparison Matrix](docs/screenshots/candidate-compare-matrix.png)

---

## Core System Capabilities

### 1. Autonomous Screener Agent
- **4-Step Execution Pipeline**:
  1. `Ingest Blueprint`: Ingests role parameters, must-have skills, and 384-dimensional dense vectors.
  2. `Evidence Triage`: Verifies qualification coverage across projects, work history, and verified proof points.
  3. `Decisive Classification`: Autonomously advances candidates to **Interview Ready**, holds for **Needs Review**, or screens out to **Rejected**.
  4. `Audit Commit`: Writes timestamped justification notes and immutable audit trail records directly to candidate dossiers.
- **Dual-Engine Transparent Attribution**:
  - *Frontier LLM Agent Mode*: Live reasoning via Groq (`llama-3.3-70b-versatile`), Google Gemini (`gemini-1.5-flash`), or OpenAI (`gpt-4o-mini`).
  - *Local Deterministic Rule Engine*: Client-side verification fallback with 100% honest attribution (zero fabricated claims).

### 2. Recruiter Agent Copilot (7 Workspace Tools)
Equipped with active agency through 7 executable tools:
1. `compare_candidates`: Opens side-by-side comparison matrix for designated applicants.
2. `update_candidate_status`: Promotes or rejects candidates in real time.
3. `select_candidate`: Loads the candidate's executive dossier into the workspace.
4. `open_interview_kit`: Launches the technical interview kit with confidential rubrics.
5. `add_note`: Appends recruiter intelligence notes to the candidate's permanent file.
6. `filter_pipeline`: Filters candidates by keyword or skill in real time.
7. `autonomous_screen_pipeline`: Dispatches the multi-step screener agent.
- **Visual ReAct Receipts**: Each tool call displays an interactive receipt badge in the chat stream with the agent's thought process, parameters, and live UI status.

### 3. Structured Technical Interview Kit
- **Confidential Rubric Protection**: Text-to-Speech (TTS) speaks only the interview question aloud, never leaking interviewer rubrics or internal scoring criteria.
- **Live Voice Dictation (STT)**: Web Speech API integration captures interviewer notes and candidate answers in real time.
- **Auto-Synced Answer Persistence**: Answers and interviewer evaluations persist directly to the database.

### 4. Dual-Layer Storage & Hybrid Vector Engine
- **Local IndexedDB Vector Store**: Zero setup required. Every candidate is automatically embedded into a 384-dimensional dense vector space for sub-millisecond semantic search.
- **Supabase Cloud Sync (pgvector)**: Enterprise database support with automated background sync, vector similarity search (`match_candidates` RPC), and schema migration script (`public/schema.sql`).
- **Zero Data Loss Guarantee**: Automatic migration ensures candidate records and role configurations remain intact across updates.

---

## System Architecture

```
                               ┌─────────────────────────────────────────┐
                               │         TalentDossier Front-End         │
                               │   (React 19 + TypeScript + Vite + CSS)  │
                               └────────────────────┬────────────────────┘
                                                    │
                 ┌──────────────────────────────────┴──────────────────────────────────┐
                 ▼                                                                     ▼
   ┌───────────────────────────┐                                         ┌───────────────────────────┐
   │    Local Storage Layer    │                                         │    Frontier AI Engine     │
   ├───────────────────────────┤                                         ├───────────────────────────┤
   │ • IndexedDB Vector Store  │                                         │ • Groq LLaMA 3.3 70B      │
   │ • 384-dim Dense Vectors   │                                         │ • Google Gemini 1.5 Flash │
   │ • Cosine Similarity Engine│                                         │ • OpenAI GPT-4o-mini      │
   │ • Persistent Local Config │                                         │ • ReAct Workspace Tools   │
   └─────────────┬─────────────┘                                         └─────────────┬─────────────┘
                 │                                                                     │
                 ▼                                                                     ▼
   ┌───────────────────────────┐                                         ┌───────────────────────────┐
   │    Cloud Database Sync    │                                         │   Interview Intelligence  │
   ├───────────────────────────┤                                         ├───────────────────────────┤
   │ • Supabase PostgreSQL     │                                         │ • Web Speech STT Audio    │
   │ • pgvector 384-dim Embed  │                                         │ • SpeechSynthesis TTS     │
   │ • Hybrid Search RPC       │                                         │ • Confidential Rubrics    │
   └───────────────────────────┘                                         └───────────────────────────┘
```

---

## Quick Start

### Prerequisites
- Node.js 18+ (Node 20+ recommended)
- npm or pnpm

### Installation

```bash
# Clone the repository
git clone https://github.com/akshat-lakhera/hack-devengers-hireflow.git
cd hack-devengers-hireflow

# Install dependencies
npm install

# Start local development server
npm run dev
```

The application will be running at `http://127.0.0.1:5173/`.

### Production Build

```bash
npm run build
npm run preview
```

### Linting & Type Checking

```bash
npm run lint
npx tsc -b
```

---

## Submission Details
- **Project Name**: TalentDossier (TD)
- **Repository**: [https://github.com/akshat-lakhera/hack-devengers-hireflow](https://github.com/akshat-lakhera/hack-devengers-hireflow)
- **Hackathon Track**: Devengers Hackathon 2026
- **Team**: Devengers
- **Architecture**: Autonomous Recruiter Intelligence Workspace with Multi-Step Agent Triage & Vector Embeddings
