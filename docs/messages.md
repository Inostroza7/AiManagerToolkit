# Módulo de Mensajes

Este módulo proporciona una estructura flexible para manejar conversaciones y mensajes en aplicaciones de chat o sistemas de procesamiento de lenguaje natural.

## Características

- Soporte para diferentes tipos de contenido (texto e imágenes)
- Clases para manejar mensajes del sistema, usuario y asistente
- Sistema de plantillas para crear mensajes fácilmente
- Manejo de historial de conversaciones con límite opcional
- Conversión fácil entre objetos de Python y representaciones de diccionario
- Logging integrado para un mejor seguimiento y depuración

## Instalación

Para usar este módulo, asegúrate de tener Python 3.6 o superior instalado. Luego, simplemente copia el archivo `messages.py` a tu proyecto.

## Uso

### Importación

```python
from messages import SystemMessage, UserMessage, AssistantMessage, Message, History
from messages import SystemTemplate, UserTemplate, AssistantTemplate
from messages import TextContent, ImageUrlContent
```

### Creación de mensajes básicos

```python
# Crear un mensaje del sistema
system_msg = SystemMessage("Eres un asistente útil.")

# Crear un mensaje del usuario
user_msg = UserMessage("Hola, ¿cómo estás?")

# Crear un mensaje del asistente
assistant_msg = AssistantMessage("¡Hola! Estoy bien, gracias por preguntar. ¿En qué puedo ayudarte hoy?")

# Crear mensajes con múltiples tipos de contenido
user_msg_with_image = UserMessage("Mira esta imagen", "https://ejemplo.com/imagen.jpg")
```

### Uso de plantillas

```python
# Crear una plantilla de usuario
user_template = UserTemplate("Mi nombre es {name} y tengo {age} años.")

# Usar la plantilla
user_msg = user_template(name="Juan", age=30)
```

### Manejo de conversaciones

```python
# Iniciar una conversación
conversation = Message("Eres un asistente útil.")

# Añadir mensajes a la conversación
conversation.add_message("Hola, ¿cómo estás?")
conversation.add_message(AssistantMessage("¡Hola! Estoy bien, gracias por preguntar. ¿En qué puedo ayudarte hoy?"))

# Obtener la conversación completa
full_conversation = conversation.get_full_conversation()
```

### Uso del historial

```python
# Crear un historial con un límite de 5 interacciones
history = History([], limit=5)

# Añadir mensajes al historial
history.add_message({"role": "user", "content": "Hola"})
history.add_message({"role": "assistant", "content": "¡Hola! ¿En qué puedo ayudarte?"})

# Obtener el historial
current_history = history.get_history()
```

## Clases principales

### `Content`
Clase base abstracta para tipos de contenido.

### `TextContent` y `ImageUrlContent`
Clases para manejar contenido de texto y URLs de imágenes.

### `BaseMessage`
Clase base abstracta para todos los tipos de mensajes.

### `SystemMessage`, `UserMessage`, y `AssistantMessage`
Clases para representar mensajes del sistema, usuario y asistente.

### `PromptTemplate`
Clase base para crear plantillas de mensajes.

### `SystemTemplate`, `UserTemplate`, y `AssistantTemplate`
Clases para crear plantillas específicas para cada tipo de mensaje.

### `History`
Clase para manejar el historial de conversación.

### `Message`
Clase principal para manejar mensajes y conversaciones.

## Logging

El módulo utiliza logging para registrar información importante y errores. Asegúrate de configurar el logging en tu aplicación para aprovechar esta funcionalidad.

## Contribuciones

Las contribuciones son bienvenidas. Por favor, abre un issue para discutir cambios mayores antes de hacer un pull request.

## Licencia

[MIT License](https://opensource.org/licenses/MIT)