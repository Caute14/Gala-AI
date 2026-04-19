# GALA-AI 
### Asistente Contable Inteligente para Autónomos vía WhatsApp

GALA-AI es una solución de **FinTech e Inteligencia Artificial** diseñada para automatizar la gestión fiscal y financiera de los trabajadores autónomos en España. Utilizando tecnologías de **Big Data y LLM**, el sistema permite la digitalización de facturas, la conciliación bancaria y la previsión de impuestos en tiempo real.

---

## Características Principales

- **Ingesta Conversacional:** Procesamiento de imágenes y PDFs vía WhatsApp Cloud API.
- **Extracción Inteligente:** Extracción de datos fiscales con precisión >98% (PaddleOCR + GPT-4o mini).
- **Open Banking:** Sincronización bajo normativa PSD2 a través de Salt Edge.
- **Conciliación Automática:** Matching inteligente entre cargos bancarios y facturas.
- **Seguridad Bancaria:** Cifrado de datos sensibles en reposo mediante AES-256.

---

## Stack Tecnológico

- **Backend:** FastAPI (Python 3.11+) & Uvicorn.
- **Base de Datos:** MongoDB Atlas.
- **Infraestructura:** Docker & AWS (EC2, S3).
- **IA/ML:** OpenAI API & PaddleOCR.

---

## Instalación y Configuración

### 1. Variables de Entorno
El sistema requiere un archivo `.env` en la raíz del proyecto para gestionar las credenciales de forma segura. **Nota:** Este archivo está incluido en `.gitignore` para evitar fugas de seguridad.

```env
# API Keys
OPENAI_API_KEY=tu_clave_aquí
WHATSAPP_TOKEN=tu_token_de_meta
SALT_EDGE_APP_ID=tu_id
SALT_EDGE_SECRET=tu_secret

# Database & Security
MONGODB_URI=mongodb+srv://...
SECRET_KEY_AES=tu_llave_de_32_caracteres
