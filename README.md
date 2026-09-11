# make-automation-registrodegastos
El proceso registra gastos a través de mensajes de audio en Telegram. El sistema procesa la voz, interpreta la información relevante y la organiza automáticamente en una planilla de Google Sheets.

<img width="1041" height="202" alt="Flujo-Make-Registrodegastos" src="https://github.com/user-attachments/assets/39bf8c9e-c373-487d-a2e7-42c3ffa5f41c" />


## 🛠️ Herramientas y Tecnologías
* **Make** (Plataforma de automatización)
* **Telegram Bot** (Interfaz de recepción y descarga del audio)
* **OpenAI (Whisper)** (Transcripción del audio a texto)
* **Google Gemini AI** (Extracción y estructuración de datos clave: monto, categoría y concepto)
* **JSON Parser** (Procesamiento y parseo del formato de datos)
* **Google Sheets** (Base de datos para el registro de gastos)

## 🔄 Flujo del Proceso
1. **Captura:** El usuario envía un mensaje de voz al bot de Telegram (ej: *"Gasté 1500 pesos en el supermercado"*).
2. **Descarga:** Make recibe la actualización y descarga el archivo de audio desde Telegram.
3. **Transcripción:** El audio pasa por OpenAI (Whisper) para convertirse en texto.
4. **Análisis con IA (Gemini):** Google Gemini procesa el texto transcrito para interpretar el monto, concepto y categoría en un formato estructurado.
5. **Parseo JSON:** Se transforma la respuesta de Gemini en variables utilizables.
6. **Almacenamiento:** Se agrega automáticamente una nueva fila en Google Sheets con los datos parseados.

7. ## ⚙️ Configuración del Prompt (Gemini)

Para que la extracción de datos funcione correctamente, el módulo de **Google Gemini AI** requiere un prompt del sistema (*System Prompt*) con la estructura deseada.

### Ejemplo de Prompt utilizado:
> "Analiza la siguiente transcripción de audio e identifica el monto, concepto y categoría del gasto. Además, considera que el nombre de la mascota del usuario es **[Nombre de tu mascota]** (para asignar gastos de veterinaria o alimentos automáticamente). Devuelve la respuesta estrictamente en formato JSON."

*Nota: Al importar el blueprint, asegurate de personalizar los datos fijos del prompt (como el nombre de tu mascota o añadir categorías propias) dentro del módulo de Gemini.*
