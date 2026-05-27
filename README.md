# GitGrok

> An intelligent multi-agent system built on **n8n** that autonomously analyzes GitHub repositories, generates structured documentation, and answers codebase questions via a conversational interface.

![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=flat-square&logo=n8n)
![OpenAI](https://img.shields.io/badge/Powered%20by-GPT--4-412991?style=flat-square&logo=openai)
![Gemini](https://img.shields.io/badge/Powered%20by-Gemini-4285F4?style=flat-square&logo=google-gemini)
![Groq](https://img.shields.io/badge/Accelerated%20by-Groq-F55036?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

---

## 🔹 What is this?

**AI Code Buddy** is a multi-agent AI workflow that takes a GitHub repository URL and automatically:

- Summarizes what the project does
- Generates a Quick-Start guide from setup files
- Maps out the module architecture
- Documents all classes, functions, objects, and APIs
- Answers developer questions about the codebase in real-time
- Delivers outputs via Google Docs, Markdown files, or Email

No manual documentation writing. Just drop a repo link and get full docs.

---

## 🔹 Architecture

```
User Query
     │
     ▼
Orchestrator Agent
     │
     ├──► GitHub Agent
     │        ├── Github Model
     │        ├── Memory
     │        ├── Get File Tool
     │        ├── Get Repository Tool
     │        ├── List File Tool
     │        └── Get Repository Tree (Sub Workflow)
     │
     └──► Documentation Agent
              ├── Documentation Model
              ├── Memory
              ├── Send Mail Tool
              ├── Create Document Tool
              ├── Update Document Tool
              └── Create Markdown Tool (Readme Generator)
```

### Agents

| Agent | Role | Tools |
|-------|------|-------|
| **Orchestrator** | Routes tasks, analyzes code, generates docs | Memory, Github Agent, Documentation Agent |
| **GitHub Agent** | Reads repo files, metadata, file trees | `GetFileTool`, `GetRepoTool`, `ListFileTool` |
| **Document Agent** | Stores and delivers documentation | `CreateDocs`, `CreateMarkdown`, `SendMail`, `UpdateDocs` |

---

## 🔹 Features

- **Repo Intake** — Validates repo access, fetches metadata and full file tree
- **Project Summary** — Auto-detects stack, purpose, and key features
- **Quick-Start Guide** — Generates installation + run instructions from actual config files
- **Architecture Map** — Folder-level breakdown of module responsibilities
- **Code Entity Docs** — Documents classes, functions, constants, and REST API endpoints
- **QA Chatbot** — Ask anything about the codebase; get answers with file + line references
- **Multi-format Delivery** — Output to Google Docs, Markdown, or Email

---

## 🔹 Directory Structure

```
ai-code-buddy/
│
├── workflows/
│   ├── main_workflow.json          # Full n8n workflow export (importable)
│   ├── orchestrator_agent.json     # Orchestrator agent node config
│   ├── github_agent.json           # GitHub agent node config
│   └── document_agent.json         # Document agent node config
│
├── prompts/
│   ├── orchestrator_system.md      # Orchestrator system prompt
│   ├── github_agent_system.md      # GitHub agent system prompt
│   └── document_agent_system.md    # Document agent system prompt
│
├── docs/
│   ├── architecture.png            # Workflow architecture diagram
│   ├── demo.gif                    # Demo GIF of the chatbot in action
│   └── sample_output.md            # Example generated documentation
│
├── examples/
│   └── sample_repo_analysis.md     # Sample output for a real GitHub repo
│
├── .env.example                    # Required API keys (template)
├── README.md
└── LICENSE
```

---

##🔹 Getting Started

### Prerequisites

- [n8n](https://n8n.io/) (self-hosted or cloud)
- OpenAI API Key (GPT-4 access)
- GitHub Personal Access Token
- Google OAuth credentials (for Docs/Drive integration)

### Setup

**1. Clone the repo**
```bash
git clone https://github.com/<your-username>/ai-code-buddy.git
cd ai-code-buddy
```

**2. Configure environment**
```bash
cp .env.example .env
# Fill in your API keys
```

**3. Import workflow into n8n**
- Open your n8n instance
- Go to **Workflows → Import**
- Upload `workflows/main_workflow.json`

**4. Configure credentials in n8n**
- OpenAI API → paste your key
- Google Gemini API → paste your key
- Groq API → paste your key
- GitHub API → paste your Personal Access Token
- Google OAuth → connect your account

**5. Activate & Test**
- Enable the workflow
- Click **Open Chat** and paste any GitHub repo URL

---

## 🔹 Usage

```
You: https://github.com/vercel/next.js

🤖 Fetching repo metadata...
🤖 Scanning 1,200 files...
🤖 Generating documentation...

📦 PROJECT SUMMARY
Name     : next.js
Purpose  : React framework for production-grade web apps
Stack    : TypeScript, React, Node.js, Rust
Features : • SSR/SSG/ISR rendering modes
           • File-based routing
           • API routes
           • ...

[Quick-Start Guide]
[Architecture Map]
[Code Entity Docs]

Would you like me to save this to Google Docs or send via email?
```

---

## 🔹 Tech Stack

| Layer | Technology |
|-------|-----------|
| Workflow Orchestration | [n8n](https://n8n.io/) |
| AI Models | OpenAI GPT-4 |
| GitHub Integration | GitHub REST API |
| Document Storage | Google Docs / Drive |
| Email Delivery | Gmail via n8n |
| Memory | n8n Window Buffer Memory |

---

## 🔹 Contributing

1. Fork the repo
2. Create your branch: `git checkout -b feature/your-feature`
3. Commit changes: `git commit -m 'Add your feature'`
4. Push: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

MIT License — feel free to use, modify, and distribute.

---

## 👤 Author

**Aryan** — [@your-github](https://github.com/your-username)

*B.Sc. (Hons) Computer Science & Data Analytics, IIT Patna*

> ⭐ If this project helped you, consider giving it a star!
