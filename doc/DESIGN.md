# Documentación de Diseño Arquitectónico - GALA-AI

## 1. Arquitectura de Sistema (High-Level Design)
GALA-AI utiliza una arquitectura de microservicios contenerizados orientada a eventos, desplegada sobre **AWS**.

### 1.1 Stack Tecnológico
- **Runtime:** Docker & Docker Compose.
- **Backend Framework:** FastAPI (Asíncrono).
- **Servidor ASGI:** Uvicorn.
- **Lenguaje:** Python 3.11+.
- **Infraestructura:** AWS EC2 (Computación) + S3 (Almacenamiento de imágenes).

### 1.2 Diagrama de Flujo de Datos
1. **Ingesta:** El usuario envía un mensaje/imagen vía WhatsApp -> Webhook en FastAPI.
2. **Procesamiento:** FastAPI delega la imagen a PaddleOCR y el texto resultante a GPT-4o mini.
3. **Persistencia:** Los datos extraídos y validados se almacenan en MongoDB Atlas.
4. **Notificación:** Se devuelve una respuesta estructurada al usuario a través de la API de Meta.

## 2. Diseño de Datos (Persistence Layer)
Se ha optado por **MongoDB** (NoSQL) debido a la naturaleza semi-estructurada de los documentos fiscales y la necesidad de escalabilidad horizontal.

### 2.1 Modelo de Colecciones

#### Colección: `Users`
| Campo | Tipo | Descripción |
|:---|:---|:---|
| `_id` | ObjectId | Identificador único. |
| `whatsapp_id` | String (Indexed) | ID de teléfono del usuario. |
| `tax_details` | Object | CIF, Nombre Fiscal y domicilio. |
| `salt_edge_token` | Binary | Token de acceso bancario (Cifrado AES-256). |

#### Colección: `Documents` (Big Data Core)
| Campo | Tipo | Descripción |
|:---|:---|:---|
| `user_id` | String (Indexed) | Relación con el usuario. |
| `s3_url` | String | Enlace al archivo original en AWS S3. |
| `extracted_data` | Object | JSON con CIF, Base, IVA y Total. |
| `category` | String | Etiqueta fiscal (Suministros, I+D, etc.). |
| `status` | String | `pending`, `validated`, `reconciled`. |
| `audit_trail` | Object | Puntuación de confianza y modelo de IA usado. |

#### Colección: `BankTransactions`
| Campo | Tipo | Descripción |
|:---|:---|:---|
| `transaction_id` | String | ID único de Salt Edge. |
| `amount` | Decimal | Importe del cargo/abono. |
| `description` | String | Concepto bancario (Raw text). |
| `linked_doc_id` | ObjectId | Referencia al documento conciliado en `Documents`. |

## 3. Diseño de Inteligencia Artificial (AI Pipeline)
El cerebro del sistema se basa en un pipeline de inferencia optimizado para minimizar latencia y costes.

- **OCR Engine:** PaddleOCR (Pre-procesamiento de imagen: reescalado y binarización).
- **Orquestador:** LangChain para la gestión de memoria de corto plazo (contexto de la conversación).
- **LLM:** GPT-4o mini con un *System Prompt* restrictivo especializado en el Plan General Contable español.
- **Lógica de Reintentos:** Si la confianza del OCR es < 70%, el sistema solicita automáticamente una nueva captura al usuario.

## 4. Diseño de Seguridad y Privacidad
- **Cifrado en Reposo:** Implementación de la librería `cryptography` (Fernet) para el cifrado AES-256 de datos bancarios.
- **Cifrado en Tránsito:** Comunicación forzada mediante protocolos HTTPS/TLS 1.3 gestionados por Cloudflare.
- **Aislamiento:** La base de datos MongoDB Atlas solo acepta conexiones desde la IP elástica de la instancia AWS (IP Whitelisting).

## 5. Integraciones Externas (APIs)
- **WhatsApp Cloud API:** Interfaz de usuario mediante Webhooks asíncronos.
- **Salt Edge API:** Conectividad Open Banking bajo normativa PSD2.
- **OpenAI API:** Motor de procesamiento de lenguaje natural y categorización.
