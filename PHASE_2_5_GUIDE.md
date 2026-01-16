# 🧭 Phase 2.5: Configuration & Integration Guide

> **Última actualización**: 16 Enero 2026
> **Prerequisito**: Fase 2 completada (servicios desplegados y accesibles)

---

## 📋 Checklist Rápido

| # | Paso | Prioridad | Estado |
|---|------|-----------|--------|
| 1 | Crear cuenta admin en Open WebUI | P0 | ⏳ |
| 2 | Crear cuenta owner en n8n | P0 | ⏳ |
| 3 | Conectar Open WebUI → Nexus Gateway | P0 | ⏳ |
| 4 | Configurar RAG Embeddings | P1 | ⏳ |
| 5 | Configurar Cloudflare Access (SSO) | P1 | ⏳ |
| 6 | Crear Webhook Router en n8n | P1 | ⏳ |
| 7 | Crear Tool en Open WebUI | P1 | ⏳ |
| 8 | Verificación final | P0 | ⏳ |

---

## 1. Open WebUI Setup

### 1.1 Crear Cuenta de Administrador

1. Abre [https://brain.ramsesdb.tech](https://brain.ramsesdb.tech)
2. Haz clic en **Sign Up**
3. Crea tu cuenta (ej. `admin@ramsesdb.tech`)

> [!IMPORTANT]
> La **primera cuenta** creada se convierte automáticamente en **Super Admin**.
> Hazlo ANTES de configurar Cloudflare Access.

### 1.2 Conectar a Nexus Gateway

1. Ve a **Settings (⚙️)** → **Admin Settings** → **Connections**
2. En la sección **OpenAI API**:

| Campo | Valor |
|-------|-------|
| **URL** | `http://nexus-gateway:3000/v1` |
| **API Key** | Tu `NEXUS_API_KEY` del `.env` de Coolify |

3. Clic en **Verify Connection**
4. ✅ Deberías ver los modelos: `llama-3.3-70b-versatile`, `gemini-2.0-flash-exp`, etc.

### 1.3 Configurar RAG Embeddings

> [!NOTE]
> El Gateway NO soporta `/v1/embeddings`. Usamos OpenAI directo para esto.

1. Ve a **Settings** → **Admin Settings** → **Documents**
2. En **Embedding Model Engine**: Selecciona `OpenAI`
3. En **OpenAI API Config**:

| Campo | Valor |
|-------|-------|
| **API Base URL** | `https://api.openai.com/v1` |
| **API Key** | Tu key de OpenAI (la de `OPENAI_EMBEDDINGS_KEY`) |
| **Model** | `text-embedding-3-small` |

4. **Chunk Size**: `1000`
5. **Chunk Overlap**: `200`
6. Guarda cambios

---

## 2. n8n Setup

### 2.1 Crear Cuenta Owner

1. Abre [https://flows.ramsesdb.tech](https://flows.ramsesdb.tech)
2. Sigue el wizard de setup inicial
3. Crea tu cuenta de propietario

### 2.2 Agregar Variable de Entorno

Para autenticar llamadas desde Open WebUI, necesitas definir el token:

1. Ve a **Settings** → **Variables**
2. Crea una nueva variable:
   - **Key**: `N8N_WEBHOOK_TOKEN`
   - **Value**: Un token seguro (genera uno con `openssl rand -hex 32`)

---

## 3. Seguridad: Cloudflare Access

> [!CAUTION]
> **Sin este paso, cualquiera puede crear cuentas en tus paneles.**
> Configúralo DESPUÉS de crear tus cuentas admin.

### 3.1 Crear Application en Cloudflare Zero Trust

1. Ve a [Cloudflare Zero Trust Dashboard](https://one.dash.cloudflare.com/)
2. **Access** → **Applications** → **Add an Application**
3. Tipo: **Self-hosted**
4. Configuración:

| Campo | Valor |
|-------|-------|
| **Application Name** | `Nexus Brain` |
| **Session Duration** | `24h` |
| **Application Domain** | `brain.ramsesdb.tech` |

5. Repite para `flows.ramsesdb.tech`

### 3.2 Crear Policy

1. **Rule name**: `Admin Access`
2. **Action**: `Allow`
3. **Include**:
   - Emails: `tu-email@gmail.com`
   - O: Emails ending in `@tu-dominio.com`

---

## 4. Integración: Open WebUI ↔ n8n

### 4.1 n8n: Crear Workflow Router

1. Crea nuevo workflow: `OpenWebUI_Router`
2. Agrega nodo **Webhook**:
   - **Method**: `POST`
   - **Path**: `openwebui`
   - **Authentication**: `Header Auth`
   - **Credential**: Crea nueva `Header Auth`:
     - Name: `Authorization`
     - Value: `Bearer {{ $env.N8N_WEBHOOK_TOKEN }}`
3. Agrega nodo **Switch**:
   - Mode: `Rules`
   - Routing value: `{{ $json.body.workflow }}`
   - Casos: `telegram`, `notion`, `home_assistant`, etc.
4. Agrega nodo **Respond to Webhook** al final de cada rama
5. **Activa** el workflow

> **URL Interna**: `http://n8n:5678/webhook/openwebui`

### 4.2 Agregar Variables en Open WebUI (Coolify)

En Coolify, agrega estas variables al servicio `open-webui`:

```env
N8N_WEBHOOK_URL=http://n8n:5678/webhook/openwebui
N8N_WEBHOOK_TOKEN=el-mismo-token-que-pusiste-en-n8n
```

Reinicia el contenedor después de agregar las variables.

### 4.3 Open WebUI: Crear Tool

1. Ve a **Workspace** → **Tools** → **+ Create Tool**
2. Configuración:

| Campo | Valor |
|-------|-------|
| **Name** | `n8n_action` |
| **Description** | `Ejecuta workflows de automatización en n8n` |

3. **Code**:

```python
"""
Tool para ejecutar workflows de n8n desde Open WebUI.
Requiere variables de entorno: N8N_WEBHOOK_URL, N8N_WEBHOOK_TOKEN
"""
import os
import requests
import json

class Tools:
    def __init__(self):
        self.webhook_url = os.getenv("N8N_WEBHOOK_URL")
        self.token = os.getenv("N8N_WEBHOOK_TOKEN")

    def execute_workflow(
        self,
        workflow_name: str,
        payload: dict
    ) -> str:
        """
        Ejecuta un workflow de n8n.

        :param workflow_name: Nombre del workflow (ej: 'send_telegram')
        :param payload: Datos a enviar al workflow
        :return: Respuesta del workflow en JSON
        """
        if not self.webhook_url or not self.token:
            return json.dumps({
                "ok": False,
                "error": "Missing N8N_WEBHOOK_URL or N8N_WEBHOOK_TOKEN"
            })

        headers = {
            "Authorization": f"Bearer {self.token}",
            "Content-Type": "application/json"
        }

        data = {
            "workflow": workflow_name,
            "data": payload
        }

        try:
            response = requests.post(
                self.webhook_url,
                json=data,
                headers=headers,
                timeout=30
            )
            response.raise_for_status()
            return json.dumps({"ok": True, "result": response.json()})
        except requests.RequestException as e:
            return json.dumps({"ok": False, "error": str(e)})
```

4. **Guardar**
5. Habilitar la tool en el modelo que uses (Settings del modelo → Tools)

---

## 5. Verificación Final

### 5.1 Checklist de Pruebas

| Prueba | Cómo verificar | ✅ |
|--------|----------------|---|
| **Chat básico** | Pregunta "Hola" en Open WebUI | ⏳ |
| **Gateway routing** | Revisa headers `X-Nexus-Provider` en respuesta | ⏳ |
| **RAG funciona** | Sube un PDF y pregunta sobre su contenido | ⏳ |
| **n8n webhook** | Pide "ejecuta workflow de prueba" | ⏳ |
| **Portfolio chat** | Prueba "Ask Ramses" en [ramsesdb.tech](https://ramsesdb.tech) | ⏳ |

### 5.2 Comandos de Debug

```bash
# Ver logs del Gateway
docker logs nexus-gateway --tail 50

# Ver logs de Open WebUI
docker logs open-webui --tail 50

# Test directo al Gateway
curl -X POST https://api.ramsesdb.tech/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TU_API_KEY" \
  -d '{"model":"llama-3.3-70b-versatile","messages":[{"role":"user","content":"ping"}]}'
```

---

## 📎 Referencias

- [Open WebUI Docs](https://docs.openwebui.com)
- [n8n Webhook Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)
- [Cloudflare Access](https://developers.cloudflare.com/cloudflare-one/policies/access/)
