---
nombre: current-topic-4geeks
descripción: Consulta el calendario de clases de 4Geeks para indicar en qué tema/lección está el usuario hoy y a qué curso certificado pertenece.
---

## Cuándo Usar
Cuando el usuario pregunte "¿Qué tema estamos viendo?", "¿En qué lección voy?", "¿Qué curso certificado toca hoy?" o similar.

## Prerrequisitos
- Conexión activa a Google Calendar (vía Zapier)
- Calendario "Clases 4Geeks" con eventos del temario
- Conocimiento de la correspondencia entre temas del calendario y cursos certificados del syllabus

## Cómo funciona
1. Consultar el calendario "Clases 4Geeks" para obtener eventos de hoy.
2. Si no hay evento hoy, informar que hoy no hay clase.
3. Si hay evento, extraer el nombre del tema.
4. Buscar el nombre del tema en el mapeo tema→curso certificado y devolver ambos.

## Mapeo tema → Curso certificado
- Capacitar al agente → Advanced personal assistants with Openclaw
- Fundamentos de Ingenieria de IA → AI Engineering Fundamentals
- Ingenieria de contexto → AI Engineering Fundamentals
- Comunicación efectiva con la IA → AI Engineering Fundamentals
- Desarrollar reglas y habilidades (Skills) → AI Engineering Fundamentals
- Programando en backend con Python → Backend development with Coding Agents
- Trabajar con listas y diccionarios de Python → Coding fundamentals with Python
- Organizar el código fuente con funciones y diccionarios → Coding fundamentals with Python
- Definir la arquitectura del backend → Backend development with Coding Agents
- Responder solicitudes de frontend con APIs → Backend development with Coding Agents
- Gestionando documentos en el backend → Backend development with Coding Agents
- Crear un agente básico con python y una API → Backend development with Coding Agents
- Almacenar datos en bases de datos ligeras → Backend development with Coding Agents
- Autenticación en backend → Backend development with Coding Agents
- Gestión de sesiones en frontend → Backend development with Coding Agents
- Gestión de errores y debbuging → Error handling, debugging and testing
- Pruebas unitarias → Error handling, debugging and testing
- Intro a bases de datos relacionales → Managing relational databases with FastAPI
- Manipulando tablas relacionales → Managing relational databases with FastAPI
- Mapeando tablas de una BD a objetos usando ORMs → Managing relational databases with FastAPI
- Desarrollo de aplicaciones en contenedores → Container applications with Docker
- Medir el desempeño de una app web → Application telemetry
- Optimizar la respuesta del backend → Application telemetry
- Cachear respuestas → Application telemetry
- Entendiendo la telemetría → Application telemetry
- Recolectando telemetría → Application telemetry
- Manipular datos de telemetría → Application telemetry
- Preparar datos de telemetría para reportes → Application telemetry
- Intro a pipelines de datos → Implementing Data Pipelines
- Construir un pipeline de datos → Implementing Data Pipelines
- Mejorar tu data Pipeline → Implementing Data Pipelines
- Procesos en segundo plano → Asynchronous processing and offloading
- Entendiendo las colas → Asynchronous processing and offloading
- Procesos asíncronos con colas de mensajes → Asynchronous processing and offloading
- Usar modelos de predicción → Models training & RAG
- Preparar datos para entrenamiento → Models training & RAG
- Modelos de clasificación → Models training & RAG
- Modelos de regresión → Models training & RAG
- Evaluar modelo de entrenado → Models training & RAG
- Ajustar hiperparámetros → Models training & RAG
- Integrar modelos → Models training & RAG
- RAG y base de conocimientos → Models training & RAG
- Crear agentes → Agentic Engineering
- Conectar agentes a sistemas con MCPs → Agentic Engineering
- Dar memoria a agentes → Agentic Engineering
- Asegurar agentes → Agentic Engineering
- Sistemas multiagentes → Agentic Engineering
- Multiagentes de automejora → Agentic Workflows
- Sistemas multiagentes con control y reinicio → Agentic Workflows
- Comunicaciones en tiempo real unidireccionales → Real-Time Communication
- Comunicaciones en tiempo real Bidireccionales → Real-Time Communication
- Vulnerabilidades comunes → Secure AI Applications
- Gobierno de la IA y prácticas seguras → Secure AI Applications

## Casos Especiales
- Sin clase hoy: informar y decir cuándo es la próxima clase.
- Fin de semana: puede no haber clase, comprobar el calendario igualmente.
- Evento no mapeado: devolver el nombre del tema y marcar el curso como "por determinar".