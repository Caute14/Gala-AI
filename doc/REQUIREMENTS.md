# Documentación de Requisitos - GALA-AI 

## 1. Introducción
Este documento define el alcance, las capacidades y las restricciones de GALA-AI, un asistente de contabilidad inteligente basado en WhatsApp para autónomos.

## 2. Requisitos Funcionales (RF)
| ID | Nombre | Descripción | Prioridad |
|:---|:---|:---|:---|
| RF-01 | Ingesta Multimodal | Recepción de imágenes (JPG/PNG) y PDFs vía WhatsApp Cloud API. | P0 (Crítica) |
| RF-02 | Extracción Inteligente | Extracción de CIF, Fecha, Base, IVA y Total mediante PaddleOCR y GPT-4o mini. | P0 (Crítica) |
| RF-03 | Clasificación AEAT | Categorización automática de gastos según el Plan General Contable para autónomos. | P1 (Alta) |
| RF-04 | Open Banking | Sincronización de movimientos bancarios mediante Salt Edge API. | P1 (Alta) |
| RF-05 | Conciliación Automática | Matching entre facturas extraídas y cargos bancarios reales. | P1 (Alta) |
| RF-06 | Informes Fiscales | Cálculo en tiempo real de modelos 303 (IVA) y 130 (IRPF). | P2 (Media) |

## 3. Requisitos No Funcionales (RNF)
- **RNF-01 (Seguridad):** Cifrado de datos sensibles en reposo mediante AES-256.
- **RNF-02 (Rendimiento):** Latencia de respuesta de la API (Uvicorn) < 5s por documento.
- **RNF-03 (Disponibilidad):** Uptime del sistema del 99.5% alojado en AWS.
- **RNF-04 (Escalabilidad):** Arquitectura basada en Docker para soporte multi-usuario.
- **RNF-05 (Privacidad):** Cumplimiento estricto de RGPD y enmascaramiento de datos bancarios.

## 4. Historias de Usuario Principales
1. **Digitalización rápida:** "Como autónomo, quiero enviar una foto de un ticket para que se guarde y clasifique automáticamente."
2. **Control fiscal:** "Como usuario, quiero consultar mi IVA acumulado trimestral mediante un mensaje de texto."
3. **Auditoría de gastos:** "Como profesional, quiero que el sistema me avise si hay un gasto bancario sin factura asociada."

## 5. Restricciones
- Dependencia de la API de Meta (WhatsApp) para la interfaz de usuario.
- Los documentos manuscritos deben tener una legibilidad mínima para garantizar el 85% de precisión.
- Los datos fiscales se limitan a la normativa vigente en España (AEAT).
