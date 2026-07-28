# 🤖 Ecosistema de Automatización IA Autónomo para Soporte B2B

> **Entrega Final:** Proyecto Integrador de Automatización con IA  
> **Arquitecto de Flujos:** [Tu Nombre y Apellido]  
> **Estado del Proyecto:** 🟢 En Producción (100% Funcional con HITL y Resiliencia)

---

## 📌 Descripción del Proyecto

Este ecosistema resuelve de extremo a extremo la **atención y resolución de tickets de soporte técnico y facturación B2B**. 

El sistema intercepta solicitudes mediante un Webhook de entrada, valida los datos del cliente en **Airtable**, clasifica la urgencia y genera una respuesta profesional utilizando un **Modelo de Lenguaje (LLM)**. Para prevenir el *"Efecto Metralleta"* y garantizar la seguridad de la comunicación, el flujo implementa un punto de **validación humana (Human-in-the-Loop)** antes de enviar la respuesta final vía **Gmail**.

---

## 🏗️ Arquitectura del Sistema
