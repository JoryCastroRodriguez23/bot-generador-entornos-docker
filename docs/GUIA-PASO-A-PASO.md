# Guía paso a paso — Bot Generador de Entornos Docker

## Objetivo

Crear un bot de Telegram con inteligencia artificial capaz de:

- Recibir solicitudes mediante lenguaje natural.
- Generar automáticamente archivos docker-compose.yml.
- Desplegar entornos Docker personalizados.
- Gestionar contenedores activos.
- Permitir acceso externo mediante túneles seguros.

## Tecnologías utilizadas

- Docker
- Docker Compose
- n8n
- OpenHands
- Telegram Bot API
- Groq
- Cloudflare Tunnel
- GitHub

## Flujo del sistema

Usuario → Telegram → n8n → IA → OpenHands → Docker → Respuesta

## Funcionalidades

- Generación automática de entornos
- Despliegue automático
- Persistencia mediante volúmenes
- Gestión de contenedores
- Integración con Telegram
- Acceso remoto seguro
