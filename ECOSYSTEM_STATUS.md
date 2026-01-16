# 🚀 Nexus Ecosystem Status & Dashboard

**Last Updated:** 2026-01-16 14:01
**Overall Status:** Phase 2 Complete ✅ (Intelligence Layer Deployed)

> **Fix Applied:** Added `healthcheck: disable: true` and `traefik.docker.network=coolify` labels to resolve "no available server" routing issue.

---

## 🌐 Quick Links (Producción)

| Componente | Estado | URL / Acceso | Repo |
| :--- | :--- | :--- | :--- |
| **Portfolio** | 🟢 Live | [ramsesdb.tech](https://ramsesdb.tech) | [GitHub](https://github.com/ramsesdb/portafolio) |
| **Nexus AI Gateway** | 🟢 Live | [api.ramsesdb.tech](https://api.ramsesdb.tech/health) | [GitHub](https://github.com/ramsesdb/nexus-ai-gateway) |
| **Coolify Panel** | 🟢 Online | `http://<VPS_IP>:8000` | N/A |
| **Open WebUI** | 🟢 Live | [brain.ramsesdb.tech](https://brain.ramsesdb.tech) | N/A |
| **n8n** | 🟢 Live | [flows.ramsesdb.tech](https://flows.ramsesdb.tech) | N/A |

---

## 🏗️ Infrastructure Specs (Azure VPS)

*   **IP:** `<REDACTED>` *(configured in Coolify)*
*   **CPU:** 2 vCPUs
*   **RAM:** 8 GB
*   **Storage:** 30 GB
*   **OS:** Linux (Ubuntu) via Coolify

---

## 📋 To-Do List (Roadmap)

### ✅ Phase 1: Foundation (Completed)
- [x] **Project Analysis:** Analyzed Gexu, Porta, and AI_infi.
- [x] **Nexus Gateway Deployment:** Running on Azure with Coolify.
- [x] **Portfolio Update:** Added Gateway project, fixed details.
- [x] **Portfolio Deployment:** Deployed to Vercel + Custom Domain (`ramsesdb.tech`).

### ✅ Phase 2: Deployment (Completed)
- [x] **Deploy Open WebUI:** Installed on Coolify (`brain.ramsesdb.tech`).
- [x] **Deploy n8n:** Installed on Coolify (`flows.ramsesdb.tech`).
- [x] **Unified Stack:** All services running in single Docker network.
- [x] **DNS Configuration:** All subdomains pointing to VPS.
- [x] **Traefik Fix:** Added `healthcheck: disable` and network labels.

### ⏳ Phase 2.5: Configuration & Integration (In Progress)
- [x] **Create Admin Account:** Open WebUI → `brain.ramsesdb.tech`
- [x] **Create Owner Account:** n8n → `flows.ramsesdb.tech`
- [x] **Configure Gateway Connection:** OpenAI settings in Open WebUI
- [x] **Configure RAG:** Using local SentenceTransformers (Free)
- [x] **Test Chat:** Verify AI responds correctly
- [x] **Webhook Router:** Create n8n webhook for Open WebUI
- [x] **Portfolio Integration:** Verify "Ask Ramses" works
- [x] **Disable Public Signups:** Prevent strangers from creating accounts

### 🔮 Phase 3: Home Lab Integration (Next)
- [ ] **Connect Gexu App:** Point Gexu Android app to the Azure Gateway URL.
- [ ] **Knowledge Base:** Upload personal docs to Open WebUI RAG.
- [ ] **Home Lab Setup:** Install Proxmox on Dell Optiplex (see PHASE_3_HOMELAB_PLAN.md).

### 📌 Future Improvements (Backlog)
- [ ] **Cloudflare Access (SSO):** Move DNS to Cloudflare for Zero Trust protection on `brain.*` and `flows.*`.

---

## 📝 Notes & Credentials (Reference)

*   **Portafolio Domain:** Managed via Namecheap + Vercel.
*   **Gateway Access:** Protected by Authorization Header (Check `.env` in Coolify).
*   **Coolify User:** *(configured in Coolify dashboard)*
