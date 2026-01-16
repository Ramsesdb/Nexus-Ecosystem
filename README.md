# 🚀 Nexus Ecosystem

> A self-hosted AI infrastructure platform combining intelligent routing, workflow automation, and RAG-powered personal assistants.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker)](deploy/)

---

## 🌟 Overview

The **Nexus Ecosystem** is my personal AI platform that connects multiple LLM providers, automation workflows, and interfaces into a unified system. It powers everything from my portfolio's AI chat to my personal Jarvis assistant on Telegram.

### Features

- 🔀 **Multi-Provider AI Gateway** - Route requests across Groq, Gemini, Claude, OpenRouter with automatic failover
- 🧠 **RAG-Powered Chat** - Open WebUI with document search and knowledge base
- ⚙️ **Workflow Automation** - n8n for orchestrating AI workflows and integrations
- 🤖 **Personal Assistant (Jarvis)** - Telegram bot for voice/text AI interactions
- 🏠 **Home Lab Ready** - Designed for cloud + local hybrid deployment

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    NEXUS ECOSYSTEM                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐       │
│  │ 🚀 NEXUS     │    │ 🧠 OPEN      │    │ ⚙️ N8N       │       │
│  │ GATEWAY      │◄───┤ WEBUI        │◄───┤              │       │
│  │              │    │              │    │              │       │
│  │ • Multi-LLM  │    │ • Chat UI    │    │ • Webhooks   │       │
│  │ • Fallback   │    │ • RAG Docs   │    │ • Workflows  │       │
│  │ • Telemetry  │    │ • Functions  │    │ • Bots       │       │
│  └──────────────┘    └──────────────┘    └──────────────┘       │
│         │                                                        │
│         ▼                                                        │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │   ☁️ LLM PROVIDERS: Groq • Gemini • Claude • OpenRouter   │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📂 Project Structure

```
nexus-ecosystem/
├── deploy/
│   └── nexus-stack-docker-compose.yml  # Production Docker Compose
├── ECOSYSTEM_STATUS.md                  # Current deployment status
├── IMPLEMENTATION_PLAN_2026.md          # Detailed roadmap
├── JARVIS_FEATURES.md                   # Personal assistant features
├── PHASE_2_5_GUIDE.md                   # Configuration guide
├── PHASE_3_HOMELAB_PLAN.md              # Home lab setup plan
├── .env.example                         # Environment template
└── README.md                            # This file
```

---

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose
- A VPS or local server (8GB+ RAM recommended)
- API keys for LLM providers (Groq, Gemini, etc.)

### Deployment

1. Clone this repository:
   ```bash
   git clone https://github.com/Ramsesdb/nexus-ecosystem.git
   cd nexus-ecosystem
   ```

2. Copy and configure environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

3. Deploy with Docker Compose:
   ```bash
   cd deploy
   docker-compose -f nexus-stack-docker-compose.yml up -d
   ```

---

## 🔗 Related Projects

| Project | Description |
|---------|-------------|
| [Nexus AI Gateway](https://github.com/Ramsesdb/nexus-ai-gateway) | The multi-provider LLM proxy powering this ecosystem |
| [Portfolio](https://github.com/Ramsesdb/portafolio) | My personal portfolio using this AI stack |

---

## 📖 Documentation

- [Implementation Plan](IMPLEMENTATION_PLAN_2026.md) - Full roadmap and architecture details
- [Phase 2.5 Guide](PHASE_2_5_GUIDE.md) - Post-deployment configuration
- [Jarvis Features](JARVIS_FEATURES.md) - Personal assistant capabilities
- [Home Lab Plan](PHASE_3_HOMELAB_PLAN.md) - Future local deployment strategy

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| **AI Gateway** | Bun + TypeScript |
| **Chat UI** | Open WebUI |
| **Automation** | n8n |
| **Orchestration** | Docker Compose |
| **Hosting** | Azure VPS + Coolify |

---

## 📝 License

MIT License - feel free to use this as inspiration for your own AI infrastructure!

---

## 👤 Author

**Ramses De La Cruz** - [ramsesdb.tech](https://ramsesdb.tech)

- GitHub: [@Ramsesdb](https://github.com/Ramsesdb)
- LinkedIn: [Ramses De La Cruz](https://linkedin.com/in/ramses-de-la-cruz)
