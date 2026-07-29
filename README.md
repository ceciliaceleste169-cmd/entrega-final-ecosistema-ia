





# 🤖 Ecosistema de Automatización IA Autónomo para Soporte B2B

> **Entrega Final:** Proyecto Integrador de Automatización con IA
> **Arquitecto de Flujos:** : Cecilia Ayala
> **Estado del Proyecto:** 🟢 En Producción (100% Funcional con HITL y Resiliencia)

---

## 📌 Descripción del Proyecto

Este ecosistema resuelve de extremo a extremo la **atención y resolución de tickets de soporte técnico y facturación B2B**.

El sistema intercepta solicitudes mediante un Webhook de entrada, valida los datos del cliente en **Airtable**, clasifica la urgencia y genera una respuesta profesional utilizando un **Modelo de Lenguaje (LLM)**. Para prevenir el *"Efecto Metralleta"* y garantizar la seguridad de la comunicación, el flujo implementa un punto de **validación humana (Human-in-the-Loop)** antes de enviar la respuesta final vía **Gmail**.

---

## 🏗️ Arquitectura del Sistema

* **Entrada:** Webhook de captura de datos en tiempo real.
* **Procesamiento:** Validar Datos ➔ Buscar Cliente ➔ Registrar Entrada en Airtable.
* **Razonamiento IA:** Agente de IA (Groq - Llama 3.3 70B) con bifurcación de ruta de éxito o ruta de error.
* **Control (HITL):** Formatear Respuesta ➔ Guardar Borrador ➔ Notificación Supervisor ➔ Esperar Aprobación (Wait Node).
* **Salida:** Responder a Cliente vía Gmail ➔ Actualizar estado a "Enviado" en Airtable.

### 🧩 Componentes y Stack Tecnológico

* **Orquestador Principal:** `n8n`
* **Base de Datos / Memoria:** `Airtable` (Tablas vinculadas: *Clientes* y *Tickets*)
* **Motor de Razonamiento (LLM):** `Groq` (`llama-3.3-70b-versatile`)
* **Canal de Salida / Notificaciones:** `Gmail` (Notificación de aprobación + Respuesta al cliente)

---

## 🛡️ Seguridad, Resiliencia y Control (HITL)

1. **Human-in-the-Loop (HITL):** Ningún correo sale al cliente final sin supervisión. El sistema envía una notificación al supervisor con un enlace de aprobación (*Wait Node*). Solo tras la confirmación humana, el correo es despachado.
2. **Ruta de Fallos (Error Handling):** Si el nodo de IA supera su cuota o la API falla, la ruta de error desvía el flujo automáticamente al nodo **`Alerta de Error`**, notificando al equipo técnico sin interrumpir el orquestador ni perder datos.
3. **Minimización de Datos:** Únicamente se pasan al LLM los campos estrictamente necesarios (`asunto` y `mensaje`), protegiendo información sensible o confidencial del cliente.

---

## 📊 Matriz de Optimización de Costos

Tarea / Nodo,Modelo Seleccionado,Razón Técnica,Ahorro Estimado
Clasificación y Redacción,Llama-3.3-70b (Groq Cloud),"Alta velocidad de inferencia, excelente sintaxis en español y costo $0.",100% de Ahorro (Tier Gratuito).
Casos Complejos / Análisis Denso,Claude 3.5 Sonnet / GPT-4o,Razonamiento avanzado para contratos o análisis contextual profundo.,Pago por consumo puntual.
Procesamiento Masivo Histórico,OpenAI Batch API,Procesamiento asíncrono para análisis nocturno de tickets.,50% de Descuento en tokens.
---

## 🔗 Enlaces Obligatorios de la Entrega

* 📊 **Dashboard de Control (Airtable Shared View):** [Ver Dashboard en Airtable](https://airtable.com/appP4OVp4EV87OloH/shrj2WeUKg25v4w57)
* 📱 **Base de Datos en Modo Lectura:** [Ver Base de Datos](https://airtable.com/appP4OVp4EV87OloH/shrj2WeUKg25v4w57)
* 🎥 **Video Demostración de Funcionamiento:** [Ver Video en Google Drive](https://drive.google.com/file/d/1Oo2A1C4shbeKLHYBMgSw6coeT2UA4r0A/view?usp=sharing)
* 📄 **Documentación Técnica PDF:** [Documentacion_Tecnica.pdf](./Documentacion_Tecnica.pdf)
* ⚙️ **Flujo de trabajo exportado (JSON):** [n8n.json](./n8n.json)
---

## 🖼️ Evidencias de Ejecución

### 1. Flujo Completo Ejecutado en n8n

### 2. Registro Completo y Sincronizado en Airtable

### 3. Notificación de Aprobación Humana (HITL)

---

## 📋 Check de Seguridad Pre-Despliegue

* [x] **Filtros contra bucles infinitos:** Configurados mediante estados unívocos en la base de datos (*Pendiente*, *Procesado*, *Enviado*).
* [x] **Tipos de datos validados:** Comparación estricta en nodos de validación (String vs String, Number vs Number).
* [x] **Prompts Dinámicos:** El prompt del Agente utiliza variables del sistema sin valores hardcodeados (`{{ $json.asunto }}`, `{{ $json.mensaje }}`).
* [x] **Credenciales Protegidas:** Variables de entorno y llaves de API omitidas en las capturas y repositorios públicos.
