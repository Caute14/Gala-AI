# Manual de Usuario y Guía de Experiencia (UX) - GALA-AI

## 1. Filosofía de Interfaz
GALA-AI no utiliza menús complejos ni aplicaciones externas. La interfaz es **conversacional y asincrónica**. El usuario interactúa con su contabilidad de la misma forma que habla con un contacto de confianza por WhatsApp.

## 2. Flujo de Onboarding (Bienvenida)
Cuando un usuario inicia el servicio por primera vez, el sistema activa el siguiente protocolo de bienvenida:

1. **Saludo Inicial:** Presentación de la IA y resumen de valor ("Ahorra 10 horas al mes en papeleo").
2. **Registro de Perfil:** Solicitud del CIF y nombre fiscal para configurar la base de datos.
3. **Prueba de Concepto:** Invitación a enviar el primer ticket para demostrar la velocidad de extracción.
4. **Vinculación Bancaria:** Enlace seguro para conectar la cuenta mediante Salt Edge (Opcional pero recomendado).

## 3. Comandos y Consultas Frecuentes
Aunque GALA-AI utiliza Procesamiento de Lenguaje Natural (NLP), se recomiendan los siguientes patrones de interacción para obtener resultados óptimos:

### Registro de Gastos e Ingresos
- **Acción:** Enviar una foto, captura de pantalla o PDF.
- **Respuesta de la IA:** "He detectado una factura de [Proveedor] por [Importe]€. ¿Es correcto?".
- **Tip de usuario:** Asegúrate de que el CIF y el Total sean legibles.

### Consultas de Estado Fiscal
- **Consulta:** "¿Cuánto IVA llevo este trimestre?"
- **Consulta:** "¿Cuál es mi previsión de IRPF para el próximo pago?"
- **Respuesta de la IA:** Resumen numérico detallando IVA repercutido, soportado y el saldo neto resultante.

### Auditoría y Conciliación
- **Consulta:** "¿Tengo algún gasto pendiente de ticket?"
- **Respuesta de la IA:** Listado de los últimos movimientos bancarios que no han sido vinculados a una factura digitalizada.

## 4. Guía de "Buenas Prácticas" para el Usuario
Para maximizar la precisión de la IA (KPI >98%), el usuario debe seguir estas pautas:
- **Iluminación:** Evitar sombras sobre los tickets térmicos de gasolinera.
- **Encuadre:** No es necesario que la foto sea perfecta, pero los cuatro bordes del documento deben ser visibles.
- **Documentos Multipage:** Para facturas de varias páginas, enviar un único archivo PDF en lugar de varias fotos.

## 5. Seguridad y Confianza (Trust Center)
Información clave que el usuario debe conocer:
- **Privacidad Bancaria:** GALA-AI solo tiene permisos de **LECTURA**. El sistema jamás podrá realizar transferencias ni mover fondos.
- **Protección de Datos:** Todos tus documentos están cifrados bajo estándares bancarios AES-256.
- **Validez Legal:** Las imágenes procesadas sirven como copia digital de respaldo, pero se recomienda conservar los originales según la normativa de la AEAT.

## 6. Resolución de Problemas (FAQ)
- **"La IA ha leído mal un dato":** El usuario puede responder al mensaje de confirmación con el dato correcto (ej: "No son 50€, son 60€") y la IA aprenderá de la corrección.
- **"No reconoce un ticket":** Puede deberse a tinta borrada. En ese caso, introducir el gasto manualmente escribiendo: "Gasto manual: [Concepto] [Importe]".
- **"Quiero darme de baja":** Escribir "Baja" para eliminar el vínculo bancario y los datos según el derecho al olvido (RGPD).

---
**Soporte Técnico:** Si la IA no responde, escribe "SOPORTE" para contactar con un humano.
