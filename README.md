# Chatbot Sena Inglés 🤖

**Proyecto final - Automatización de procesos con IA**  
SENA 2025 - Aprendices: [Meriyei Manosalva] & [Madeleine Torres]

## Descripción
Chatbot educativo de inglés en Telegram que adapta respuestas según nivel del estudiante, corrige ejercicios, enseña vocabulario y responde dudas usando IA local (Gemma 2 + Ollama).

**Todo 100% local, gratis y privado** – sin OpenAI, sin datos en la nube.

## Stack Tecnológico
- Ollama + Gemma 2 (2b/9b)
- n8n (flujos + Git Sync)
- Telegram Bot API
- Docker + Tailscale
- Google Sheets (opcional para niveles)

## Requerimientos Funcionales Cumplidos

| Código    | Requerimiento                          | Estado | Cómo lo hacemos con nuestro stack                                      |
|-----------|----------------------------------------|--------|-------------------------------------------------------------------------|
| RF01.1   | Nivel inglés (Bajo/Medio/Alto)         | SÍ     | Telegram Trigger → pregunta nivel → almacena en Google Sheets o variable n8n |
| RF01.2   | Adaptar respuestas                     | SÍ     | Switch node → si nivel Bajo → prompt simplificado a Ollama           |
| RF02.1   | Listas vocabulario por categoría       | SÍ     | JSON estático o Google Sheet → botones → envía lista                    |
| RF03.1   | Info SENA                              | SÍ     | Texto fijo o RAG con documento SENA en Ollama                          |
| RF04.1   | Conversación en inglés                 | SÍ     | Loop: Telegram Trigger → Ollama → Telegram Send                         |
| RF04.2   | Corrección + sugerencias               | SÍ     | Prompt: "Corrige esto y sugiere 3 palabras mejores: {{mensaje}}"        |
| RF04.3   | Subir PDF/texto (profesor)             | SÍ     | Telegram recibe archivo → n8n extrae texto → Ollama resume/explica      |
| RF05.1–2 | Enlaces cursos on-demand               | SÍ     | Comando /cursos o botón → envía lista predefinida                       |
| RF06.1   | Menú principal con botones             | SÍ     | Reply keyboard permanente: “Vocabulario”, “Practicar”, “SENA”, “Cursos”|
| RNF01    | Usabilidad + español claro             | SÍ     | Telegram + botones = súper simple                                       |
| RNF03    | Seguridad/anónimo                      | SÍ     | Solo guardamos chat_id + nivel → nada personal                          |
| RNF05     | Integración IA                         | SÍ     | Ollama HTTP node → 100% eficiente                                       |

## Setup rápido (para pruebas)
```bash
ollama pull gemma2:2b
ollama serve
# luego corre n8n con docker
docker run -d --name n8n -p 5678:5678 n8nio/n8n

# Acceder a n8n: http://localhost:5678

