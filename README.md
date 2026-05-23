# bot-generador-entornos-docker🤖🚀🐳
> Proyecto integrador · DAM · Sistemas Informáticos 

Bot de Telegram con IA diseñado para recibir una descripción en lenguaje natural y generar automáticamente un entorno Docker personalizado. El objetivo del proyecto es automatizar la creación y despliegue de servicios mediante tecnologías de contenedores y herramientas de inteligencia artificial.

```
"Necesito un entorno para una app Python con PostgreSQL y Redis"
                            ↓
              🔄 Generación automática
              URL: http://localhost:8080
              DB: postgres:5432 · Redis: 6379
              Credenciales: admin / admin1234
```

---

## 🏛️ Arquitectura

```txt
┌──────────────┐   POST    ┌───────────────────┐   prompt   ┌──────────┐
│   Telegram   │ ────────▶ │ Cloudflare Tunnel │ ─────────▶ │   n8n    │
│  (BotFather) │           │ (sin abrir puertos)│           │ workflow │
└──────────────┘           └───────────────────┘           └────┬─────┘
                                                                │
                                           ┌────────────────────┼────────────────┐
                                           ▼                    ▼                ▼
                                      ┌─────────┐         ┌───────────┐    ┌──────────┐
                                      │  Groq   │         │ OpenHands │    │ docker   │
                                      │ Llama 3 │         │  agent    │    │ socket   │
                                      └─────────┘         └───────────┘    └──────────┘
                                         (IA)              (despliega)      (ejecuta)
```

**Componentes del sistema:**

- **Telegram Bot** — interfaz de usuario creada mediante BotFather.
- **Cloudflare Tunnel** — permite exponer servicios localmente sin abrir puertos en el router.
- **n8n** — encargado de orquestar el flujo completo del sistema.
- **Groq** — proveedor gratuito de IA encargado de generar archivos `docker-compose.yml`.
- **OpenHands** — agente con acceso al socket Docker para ejecutar despliegues.

La arquitectura está diseñada para exponer únicamente el puerto de n8n al host, manteniendo el resto de servicios dentro de una red interna segura.

---

## 🚀 Cómo arrancar el proyecto

### Requisitos previos

- Docker Engine
- Docker Compose v2
- Cuenta gratuita en:
  - Groq
  - Telegram
  - Cloudflare

---

### 1. Clonar el repositorio

```bash
git clone https://github.com/TU_USUARIO/bot-generador-entornos-docker.git

cd bot-generador-entornos-docker
```

---

### 2. Configurar variables de entorno

```bash
cp .env.example .env
```

Editar el archivo `.env` con las siguientes credenciales:

- `GROQ_API_KEY`
- `TELEGRAM_BOT_TOKEN`
- `CLOUDFLARE_TUNNEL_TOKEN`
- `WEBHOOK_URL`

---

### 3. Levantar los servicios

```bash
mkdir -p workspace

docker compose up -d
```

---

### 4. Configurar el workflow de n8n

1. Abrir:

```txt
http://localhost:5678
```

2. Crear usuario administrador.

3. Importar el workflow:

```txt
Workflows → Import from File
```

Seleccionar:

```txt
n8n-workflow/bot-docker.json
```

4. Configurar credenciales:

**Groq API**

```txt
Authorization: Bearer ${GROQ_API_KEY}
```

**Telegram API**

Pegar el token generado mediante BotFather.

5. Activar el workflow.

---

### 5. Probar el bot

Enviar un mensaje:

```txt
Necesito un nginx con php
```

El sistema realizará:

1. Generación automática del `docker-compose.yml`
2. Despliegue mediante OpenHands
3. Devolución del resultado al usuario

Comandos previstos:

```txt
/listar
/parar <nombre>
/eliminar <nombre>
```

---

## 📁 Estructura del repositorio

```txt
bot-generador-entornos-docker/
├── docker-compose.yml
├── .env.example
├── .gitignore
├── README.md
├── docs/
│   ├── GUIA-PASO-A-PASO.md
│   ├── system-prompt.md
│   └── capturas/
├── n8n-workflow/
│   └── bot-docker.json
└── workspace/
```

---

## 🎯 Cumplimiento de la rúbrica

| Nivel | Requisito | Estado |
|-------|-----------|:------:|
| Nivel 1 | docker-compose funcional | 🔄 En desarrollo |
| Nivel 1 | IA gratuita conectada | 🔄 En desarrollo |
| Nivel 1 | Prompt configurado | 🔄 En desarrollo |
| Nivel 1 | README y repositorio | ✅ Completado |
| Nivel 2 | Persistencia mediante volúmenes | 🔄 En desarrollo |
| Nivel 2 | OpenHands despliega automáticamente | 🔄 En desarrollo |
| Nivel 3 | Integración con Telegram | 🔄 En desarrollo |
| Nivel 3 | Túnel local Cloudflare | 🔄 En desarrollo |
| Nivel 3 | Gestión de contenedores | 🔄 En desarrollo |

---

## 🎬 Demostración

📹 Vídeo de demostración: Pendiente de incorporación

📸 Capturas del desarrollo y pruebas disponibles en:

```txt
docs/capturas/
```

---

## 📝 Información académica

Proyecto realizado como práctica integradora para el módulo de Sistemas Informáticos del ciclo DAM.

---

## 👥 Equipo de trabajo

👩‍💻 **Jory Litsy Castro Rodríguez**  
👩‍💻 **Patricia Aguado Marín**

👨‍🏫 **Profesor:** Héctor Oviedo  
🎓 **Módulo:** Sistemas Informáticos · DAM  
📅 **Curso:** 2025/2026  
🤖🐳 **Proyecto:** Bot Generador de Entornos Docker

---

## 📜 Licencia

Proyecto educativo desarrollado con fines académicos.
