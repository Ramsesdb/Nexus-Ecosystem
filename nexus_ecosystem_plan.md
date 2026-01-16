# Nexus Ecosystem: Infraestructura de IA Distribuida y Domótica Cognitiva

## 📄 Resumen Ejecutivo
Un ecosistema integral de Full Stack que unifica servicios móviles, gestión del conocimiento personal y automatización del hogar bajo una arquitectura híbrida (Nube/Local).

El sistema centraliza la inferencia de Inteligencia Artificial mediante un Gateway propietario, alimentando tanto a una aplicación móvil de consumo masivo (Gexu) como a un asistente doméstico contextual (Smart Home). El objetivo es democratizar el acceso a LLMs avanzados eliminando barreras de costo y latencia, mientras se mantiene la privacidad de los datos personales en servidores Self-Hosted.

---

## 🎯 Motivación: La Domótica Semántica
El objetivo es superar las limitaciones de los asistentes tradicionales (Alexa, Google Assistant) que funcionan como **ejecutores de comandos** ("Haz X"). El Nexus Ecosystem busca crear un **intérprete de intenciones** ("Entiende qué quiero y haz lo necesario").

### Diferencia Clave: Intención vs. Comando
*   **Alexa (Rígida):**
    *   *Usuario:* "Alexa, hace calor."
    *   *Alexa:* "No encontré ningún dispositivo llamado 'hace calor'."
    *   *Resultado:* Frustración.
*   **Nexus (Inteligente):**
    *   *Usuario:* "Chamo, me estoy asando aquí en la sala."
    *   *Sistema:* Analiza "Asando" = Calor, Ubicación = Sala.
    *   *Acción:* Enciende el aire acondicionado en modo Turbo.
    *   *Respuesta:* "Listo, prendí el aire de la sala para que refresque rápido."

---

## 🧩 Arquitectura del Sistema

### Capa 0: La Infraestructura (El Suelo)
*   **Fase 1 (Nube):** VPS Microsoft Azure (2 vCPU, 8GB RAM, 30GB SSD) gestionado con Coolify.
*   **Fase 2 (Home Lab):** Dell Optiplex 3060 SFF (i5-8500, 16GB RAM) en local.
*   **Red:** Cloudflare Tunnel para exposición segura sin abrir puertos.

### Capa 1: Gestión y Orquestación (El Capataz)
*   **Software:** Coolify.
*   **Función:** Panel de control PaaS (Platform as a Service) para despliegue de contenedores y bases de datos.

### Capa 2: Motor de Inteligencia (AI Gateway)
*   **Componente:** Nexus AI Gateway (basado en Bun/TypeScript).
*   **Características:**
    *   **Key Pooling:** Rotación de claves para Groq, Cerebras y Gemini.
    *   **Balanceo de Carga:** Priorización por velocidad y disponibilidad.
    *   **API Standard:** Expone una interfaz compatible con OpenAI.

### Capa 3: El Cerebro (La Mente)
*   **Software:** Dify.ai (Community Edition).
*   **Funciones:**
    *   **RAG (Retrieval-Augmented Generation):** Acceso a manuales, notas y documentos personales (Weaviate).
    *   **Agentes:** Interpretación de lenguaje natural y toma de decisiones.

### Capa 4: El Sistema Nervioso (Los Brazos)
*   **Software:** n8n (Workflow Automation).
*   **Flujos:**
    *   Conecta las decisiones de Dify con las herramientas reales (Home Assistant, Notion, Telegram).
    *   Ejemplo: `Dify ("Modo Cine") -> n8n Webhook -> Home Assistant`.

### Capa 5: El Cuerpo Físico (IoT)
*   **Software:** Home Assistant (HA) + Zigbee2MQTT.
*   **Hardware:**
    *   Sensores Zigbee (Puerta, Movimiento).
    *   Actuadores (Interruptores Sonoff, IR Blasters).
    *   **Voz:** Integración híbrida con Alexa (TTS via Alexa Media Player) y micrófonos locales (ESP32/Atom Echo).

### Capa 6: Interfaces (Los Sentidos)
*   **Telegram:** Chat directo con el agente.
*   **Voz:** Comandos verbales en la casa.
*   **Gexu App:** Aplicación móvil que consume la inteligencia del sistema.

---

## 🛤️ Hoja de Ruta (Roadmap)

1.  **Semana 1: Infraestructura Base (✅ Completado)**
    *   Configurar VPS Azure + Coolify.
    *   Desplegar Nexus AI Gateway con pool de keys en el servidor.
2.  **Semana 2: El Cerebro (Próximo)**
    *   Instalar Dify + n8n en el VPS de Azure.
    *   Conectar Dify al Gateway.
3.  **Semana 3: Interfaces de Chat**
    *   Crear Bot de Telegram en n8n conectado a Dify.
4.  **Semana 4: Integración de Conocimiento**
    *   Conectar Notion y bases de conocimiento.
5.  **Futuro (On-Premise):**
    *   Migración al Dell Optiplex.
    *   Despliegue de Home Assistant y Zigbee.

---

## 💼 Estrategia de Portafolio

Este ecosistema se desglosa en 4 proyectos demostrables para GitHub/LinkedIn:

1.  **Gateway de IA de Alta Disponibilidad:** Backend en Bun/TS con balanceo de carga.
2.  **Asistente Personal Semántico:** Agentes RAG con Dify/n8n.
3.  **Gexu (Mobile Product):** App consumidora del Gateway con UX pulida.
4.  **Infraestructura Domótica Local-First:** Configuración DevOps/IoT con Docker y HA.

---

## 🛠️ Stack Tecnológico
*   **Infra:** Docker, Coolify, Microsoft Azure, Ubuntu.
*   **Backend:** TypeScript, Bun, Node.js.
*   **AI:** OpenAI API Standard, RAG, Prompt Engineering.
*   **IoT:** Home Assistant, MQTT, Zigbee.
*   **Mobile:** Kotlin/Compose (Gexu).
