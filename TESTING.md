# Plan de Pruebas y Control de Calidad - GALA-AI

## 1. Introducción
Este documento detalla la estrategia de validación para asegurar la integridad de los datos financieros, la precisión de la IA y la estabilidad de la infraestructura de GALA-AI. El objetivo es garantizar un error marginal en el cálculo de impuestos y una latencia óptima en la interfaz de WhatsApp.

## 2. Tipos de Pruebas y Metodología

### 2.1 Pruebas Unitarias (Unit Testing)
Se centran en la lógica pura de Python, aislada de bases de datos o APIs externas.
- **Módulo Crítico:** `app/services/tax_calculator.py`.
- **Casos de prueba:** - Cálculo de IVA (21%, 10%, 4%).
  - Cálculo de retenciones de IRPF.
  - Validación de formatos de CIF/NIF españoles.
- **Herramienta:** `pytest`.

### 2.2 Pruebas de Integración (Integration Testing)
Verifican el flujo de datos entre los distintos componentes del sistema.
- **Flujo A:** Recepción de Webhook de WhatsApp -> Almacenamiento en S3.
- **Flujo B:** Extracción de datos -> Persistencia en MongoDB Atlas.
- **Flujo C:** Consulta de movimientos Salt Edge -> Registro en `BankTransactions`.
- **Herramienta:** `pytest-asyncio` (para gestionar la asincronía de FastAPI).

### 2.3 Evaluación de Modelos de Lenguaje (LLM Eval)
Dado que el motor de extracción es probabilístico, realizamos pruebas de precisión sobre un **Golden Dataset**.
- **Dataset:** 50 imágenes patrón de tickets y facturas (manuscritos, térmicos y digitales).
- **Métricas:** - **CER (Character Error Rate):** Objetivo < 2% en texto impreso.
  - **F1-Score en Categorización:** Objetivo > 90% de acierto en tipos de gasto AEAT.
- **Procedimiento:** Comparación automatizada de la salida del LLM contra el JSON de referencia mediante la librería `deepeval` o scripts personalizados.

### 2.4 Pruebas de Estrés y Carga (Performance Testing)
Aseguran que el sistema no se degrade bajo uso concurrente.
- **Escenario:** Simulación de 50 usuarios enviando facturas simultáneamente.
- **KPI Objetivo:** Latencia P95 < 5 segundos.
- **Herramienta:** `Locust`.

---

## 3. Ejecución de Tests

### 3.1 Suite Automática
Para ejecutar todos los tests de la suite (excepto carga y LLM eval):
```bash
pytest --cov=app tests/
