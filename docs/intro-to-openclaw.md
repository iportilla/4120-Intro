# Introduction to OpenClaw
### A Beginner's Guide to Your First Agentic AI Assistant

---

## What Is an AI Agent?

You've probably used AI tools that answer questions — you type something, it responds. That's a chatbot. An **AI agent** is different. It doesn't just respond; it *acts*. It can read your files, run commands, search the web, send messages, and chain multiple steps together to complete a goal — all on its own.

Think of the difference this way:

```mermaid
flowchart LR
    subgraph Chatbot["💬 Chatbot (e.g. ChatGPT web)"]
        U1[You ask a question] --> A1[AI answers]
    end

    subgraph Agent["🦞 AI Agent (e.g. OpenClaw)"]
        U2[You give a goal] --> A2[AI plans steps]
        A2 --> A3[AI reads your files]
        A3 --> A4[AI runs a command]
        A4 --> A5[AI sends you a message]
        A5 --> A6[Goal complete ✓]
    end

    style Chatbot fill:#ecf0f1,stroke:#bdc3c7
    style Agent fill:#eaf4fb,stroke:#2980b9
```

OpenClaw is an open-source AI agent that runs **on your own machine**. Your data stays local. You choose the AI model. You control what it can and can't do.

---

## How OpenClaw Works

OpenClaw has three main parts working together:

```mermaid
graph TD
    You([👤 You]) -->|send a message| CH[📱 Channel\nSlack · Telegram · Discord\niMessage · WhatsApp · Teams]
    CH -->|delivers message| GW[⚙️ Gateway\nRunning on your machine]
    GW -->|reads instructions| SK[🧩 Skills\nWhat the agent knows how to do]
    GW -->|thinks & reasons| LLM[🧠 AI Model\nClaude · GPT-4o · Ollama]
    GW -->|takes action| AC[🔧 Actions\nRead files · Run commands\nSearch web · Call APIs]
    AC -->|results| GW
    GW -->|sends reply| CH
    CH -->|you see the answer| You

    style You fill:#2c3e50,color:#fff
    style CH fill:#4A154B,color:#fff
    style GW fill:#c0392b,color:#fff
    style SK fill:#e67e22,color:#fff
    style LLM fill:#2980b9,color:#fff
    style AC fill:#27ae60,color:#fff
```

- **Channel** — where you talk to it (Slack, Telegram, iMessage, etc.)
- **Gateway** — the engine running on your computer that connects everything
- **Skills** — modular add-ons that teach the agent new abilities
- **AI Model** — the brain doing the reasoning (you supply the API key)
- **Actions** — real things it does: reading files, running scripts, calling web APIs

---

## A Real Example: Slack Bot with Document Search

Here's a practical setup — an OpenClaw bot in Slack that answers questions from *your own documents*, not the internet.

### The Setup

```mermaid
flowchart TD
    subgraph Your Mac
        GW[OpenClaw Gateway]
        SK[RAG Skill\nlocal-file-rag-basic]
        DOCS[📁 Your Documents\nPDFs · Notes · Reports]
        GW <--> SK
        SK <--> DOCS
    end

    subgraph Slack
        CH[#channel or DM]
    end

    subgraph Anthropic Cloud
        LLM[Claude Sonnet]
    end

    You([👤 You]) -->|"What does the Q3 report say\nabout revenue targets?"| CH
    CH -->|WebSocket / Socket Mode| GW
    GW -->|semantic search| SK
    SK -->|relevant passages + filenames| GW
    GW -->|question + context| LLM
    LLM -->|grounded answer| GW
    GW -->|"According to Q3_report.pdf:\nRevenue target is $4.2M..."| CH
    CH --> You

    style Your Mac fill:#fdfefe,stroke:#aab
    style Slack fill:#4A154B,color:#fff
    style Anthropic Cloud fill:#2c3e50,color:#fff
```

### What This Feels Like in Practice

You DM the bot in Slack:

> *"What are the grading criteria for Business Analytics?"*

The bot searches your local PDF syllabus, finds the relevant section, and replies with a cited answer — without ever sending your document to a third-party server.

---

## What Are Skills?

Skills are the key to making OpenClaw useful for *your* specific needs. Each skill is a small instruction file (a `SKILL.md`) that teaches the agent how to handle a particular type of task.

```mermaid
mindmap
  root((OpenClaw Skills))
    Documents
      Read PDFs
      Search notes
      RAG over local files
      Summarize reports
    Communication
      Slack messages
      Send emails
      Discord posts
      Calendar invites
    Development
      Run code
      Check GitHub PRs
      Review pull requests
      Run test suites
    Research
      Web search
      Summarize articles
      Fact-check claims
    Productivity
      Manage tasks
      Draft documents
      Analyze spreadsheets
      Schedule reminders
```

You install skills from **ClawHub** — a community marketplace with thousands of skills — using a single command:

```bash
clawhub install local-file-rag-basic
```

---

## OpenClaw vs. Other AI Tools

```mermaid
quadrantChart
    title AI Tools — Control vs Capability
    x-axis Low Control --> High Control
    y-axis Low Capability --> High Capability
    quadrant-1 Powerful but you own it
    quadrant-2 Powerful but cloud-dependent
    quadrant-3 Limited and cloud-dependent
    quadrant-4 Limited but private
    ChatGPT Web: [0.25, 0.60]
    Claude.ai: [0.30, 0.70]
    GitHub Copilot: [0.35, 0.55]
    Siri / Alexa: [0.20, 0.25]
    OpenClaw + Claude: [0.85, 0.80]
    OpenClaw + Ollama: [0.95, 0.55]
```

The top-right quadrant is where OpenClaw lives — high capability, high control. When paired with a local model like Ollama, your data never leaves your machine at all.

---

## Beyond Slack: Other Ways to Use OpenClaw

Slack is just one channel. The same Gateway running on your machine can connect to many different surfaces simultaneously.

```mermaid
flowchart LR
    GW[⚙️ OpenClaw Gateway]

    GW <-->|chat| SL[💼 Slack\nTeam workflows\nDocument Q&A\nProject updates]
    GW <-->|chat| TG[✈️ Telegram\nPersonal assistant\nQuick lookups\nReminders]
    GW <-->|chat| DC[🎮 Discord\nCommunity bots\nModeration\nStudy groups]
    GW <-->|chat| IM[💬 iMessage\nOn-the-go access\nFamily assistant]
    GW <-->|chat| WA[📱 WhatsApp\nMobile workflows\nMultilingual support]

    style GW fill:#c0392b,color:#fff
    style SL fill:#4A154B,color:#fff
    style TG fill:#2980b9,color:#fff
    style DC fill:#5865F2,color:#fff
    style IM fill:#34C759,color:#fff
    style WA fill:#25D366,color:#fff
```

---

## Education Use Cases

OpenClaw is particularly powerful as a learning tool. Here are some ways students and educators use it:

```mermaid
flowchart TD
    subgraph Student["🎓 Student Use Cases"]
        S1[Upload course PDFs\nand syllabi]
        S2[Ask questions about\nlecture notes]
        S3[Get explanations from\nyour own textbooks]
        S4[Summarize readings\nbefore class]
        S5[Quiz yourself on\nmaterial you uploaded]
        S1 --> S2 --> S3
        S4 --> S5
    end

    subgraph Educator["🏫 Educator Use Cases"]
        E1[Load curriculum docs\nand rubrics]
        E2[Answer student FAQs\nautomatically via Slack]
        E3[Summarize student\nsubmissions]
        E4[Generate quiz questions\nfrom course material]
        E5[Keep answers grounded\nin your own content]
        E1 --> E2
        E1 --> E3
        E1 --> E4
        E4 --> E5
    end

    style Student fill:#eaf4fb,stroke:#2980b9
    style Educator fill:#eafaf1,stroke:#27ae60
```

### Example: Study Assistant

A student in a Business Analytics course loads their syllabus, textbook, and lecture notes into OpenClaw. Then in Slack or Telegram they ask:

> *"Explain the difference between predictive and descriptive analytics based on my course materials"*

The agent searches the uploaded PDFs and answers using *their professor's framing* — not a generic web answer.

---

## Key Concepts Recap

```mermaid
flowchart LR
    A[🧠 AI Model\nDoes the reasoning] --- B[⚙️ Gateway\nConnects everything]
    B --- C[🧩 Skills\nNew capabilities]
    B --- D[📱 Channel\nHow you talk to it]
    B --- E[📁 Your Data\nStays local]

    style A fill:#2980b9,color:#fff
    style B fill:#c0392b,color:#fff
    style C fill:#e67e22,color:#fff
    style D fill:#4A154B,color:#fff
    style E fill:#27ae60,color:#fff
```

| Concept | What It Means |
|---------|--------------|
| **Agent** | AI that takes actions, not just answers |
| **Gateway** | The engine running on your machine |
| **Skill** | A module that adds a new capability |
| **Channel** | Where you interact (Slack, Telegram, etc.) |
| **RAG** | Retrieval-Augmented Generation — answers grounded in your documents |
| **Local-first** | Your data stays on your machine |

---

## Getting Started

```mermaid
journey
    title Your First OpenClaw Setup
    section Install
      Install Node.js 24: 5: You
      Run install script: 5: You
      Run onboard wizard: 4: You, OpenClaw
    section Connect
      Add Anthropic API key: 3: You
      Create Slack app: 3: You
      Configure tokens: 3: You, OpenClaw
    section Load Your Docs
      Install RAG skill: 5: OpenClaw
      Copy PDFs to documents folder: 5: You
      Test a query in Slack: 5: You, OpenClaw
    section Use It Daily
      Ask questions about your docs: 5: You
      Add new documents anytime: 5: You
      Install more skills as needed: 4: You
```

The whole setup takes about 30–45 minutes. After that, your AI assistant is always on, always private, and always working from *your* knowledge — not the internet's.

---

*Built with OpenClaw v2026.6.6 · Claude Sonnet 4.6 · local-file-rag-basic skill*
