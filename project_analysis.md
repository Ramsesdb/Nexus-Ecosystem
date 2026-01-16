# Project Analysis Report

## 1. Gexu (Android)
**Path:** `c:\Users\ramse\AndroidStudioProjects\gexu`
**Type:** Android Application (Mihon Fork)
**Tech Stack:** Kotlin, Jetpack Compose, Gradle, SQLDelight, WorkManager.

### Overview
Gexu is a highly advanced fork of the Mihon manga reader, specifically enhanced with **"Gexu AI"**, a context-aware assistant. It follows a Clean Architecture pattern (`core`, `domain`, `data`, `presentation`).

### Key Features
- **AI Integration:** deep integration with Gemini, OpenAI, Anthropic, and OpenRouter.
- **Context Awareness:** "Gexu AI" knows what you are reading (Series, Chapter, Author) to prevent spoilers and provide relevant answers.
- **RAG & Vector Search:** Implements local vector search for library data.
- **Visual Intelligence:** "Circle-to-Search" functionality for analyzing panels/pages.
- **Privacy:** All AI keys are stored locally; history is stateless/in-memory.

### Health & Status
- **Active Development:** Significant changes in Dec 2025/Jan 2026.
- **Clean Code:** Adheres to strict linting (`spotless`).
- **Architecture:** Robust separation of concerns.

---

## 2. Porta (Next.js Portfolio)
**Path:** `c:\Users\ramse\OneDrive\Documents\porta`
**Type:** Web Application
**Tech Stack:** Next.js 16.1.1 (React 19), TailwindCSS v4, TypeScript, Framer Motion.

### Overview
A thoroughly modern personal portfolio website leveraging the absolute latest web technologies.

### Key Features
- **Cutting Edge:** Uses Next.js 16 (Canary/Latest) and React 19.
- **Styling:** TailwindCSS v4 (PostCSS).
- **Internationalization:** Full support via `next-intl`.
- **Performance:** Integrated with generic Vercel Analytics and Speed Insights.
- **Animation:** Uses Framer Motion for UI transitions.

### Health & Status
- **Modern:** Dependencies are up-to-date.
- **Clean Structure:** Standard App Router organization.

---

## 3. AI_infi (Nexus AI Gateway)
**Path:** `c:\Users\ramse\OneDrive\Documents\vacas\AI_infi`
**Type:** Backend Service / Proxy
**Tech Stack:** Bun, TypeScript, Nixpacks.

### Overview
**"Nexus AI Gateway v1.0"** is a high-performance, fault-tolerant proxy server for AI providers written in Bun. It acts as a unified entry point for LLM requests.

### Key Features
- **Multi-Provider:** Supports Groq, Gemini, OpenRouter, and Cerebras.
- **Smart Routing:**
  - **Health-Aware Load Balancing:** Scores providers based on latency and success rate.
  - **Circuit Breaker:** Automatically disables failing providers to prevent cascading failures.
  - **Prioritization:** Cerebras (Fastest) > Groq > OpenRouter > Gemini.
- **Reliability:** Exponential backoff and retry mechanism for failed requests.
- **Security:** Master Key authentication and CORS control.
- **Deployment:** Configured with `nixpacks` for easy deployment (likely Coolify/Railway).

### Health & Status
- **Production Ready:** Includes graceful shutdown, detailed logging, and health checks (`/health`).
- **Performance:** Optimized for speed using Bun.
