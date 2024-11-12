# Azure AI Toolkit Documentation

Este documento proporciona una guía detallada sobre cómo utilizar las clases `AzureAI` y `AsyncAzureAI` para interactuar con los servicios de Azure OpenAI.

## Tabla de Contenidos
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Inicialización](#inicialización)
- [Chat Completions](#chat-completions)
- [Streaming](#streaming)
- [Salida Estructurada](#salida-estructurada)
- [Embeddings](#embeddings)
- [Speech to Text (STT)](#speech-to-text-stt)
- [Text to Speech (TTS)](#text-to-speech-tts)
- [Manejo de Errores](#manejo-de-errores)

## Instalación

```bash
pip install aimanagertoolkit
```

## Configuración

Crea un archivo `.env` en la raíz de tu proyecto con las siguientes variables:

```env
AZURE_OPENAI_ENDPOINT="https://your-resource-name.openai.azure.com/"
AZURE_OPENAI_API_KEY="your-api-key"
AZURE_OPENAI_API_VERSION="2024-02-15-preview"
AZURE_OPENAI_DEPLOYMENT="your-model-deployment-name"
AZURE_OPENAI_EMBEDDINGS_MODEL="text-embedding-3-small"
```

## Inicialización

### Versión Síncrona

```python
from azure_ai_toolkit import AzureAI

# Inicialización básica
ai = AzureAI()

# Inicialización con parámetros personalizados
ai = AzureAI(
    model="gpt-4",
    temperature=0.7,
    max_tokens=1000,
    response_format={"type": "json_object"}
)
```

### Versión Asíncrona

```python
from azure_ai_toolkit import AsyncAzureAI
import asyncio

# Inicialización básica
async def main():
    ai = AsyncAzureAI()
    # Tu código asíncrono aquí

asyncio.run(main())
```

## Chat Completions

### Versión Síncrona

```python
# Ejemplo básico
messages = [
    {"role": "system", "content": "Eres un asistente útil."},
    {"role": "user", "content": "¿Cuál es la capital de Francia?"}
]

response = ai.chat(messages)
print(response.choices[0].message.content)

# Con parámetros adicionales
response = ai.chat(
    messages=messages,
    temperature=0.8,
    response_format={"type": "text"}
)
```

### Versión Asíncrona

```python
async def chat_example():
    messages = [
        {"role": "system", "content": "Eres un asistente útil."},
        {"role": "user", "content": "¿Cuál es la capital de Francia?"}
    ]
    
    response = await ai.chat(messages)
    print(response.choices[0].message.content)
```

## Streaming

### Versión Síncrona

```python
messages = [
    {"role": "user", "content": "Cuéntame una historia corta."}
]

# El texto se imprimirá a medida que se recibe
ai.stream(messages)
```

### Versión Asíncrona

```python
async def stream_example():
    messages = [
        {"role": "user", "content": "Cuéntame una historia corta."}
    ]
    
    async for chunk in ai.stream(messages):
        print(chunk, end="")
```

## Salida Estructurada

### Definición del Esquema

```python
from pydantic import BaseModel
from typing import List

class ResponseSchema(BaseModel):
    title: str
    points: List[str]

# Definir el formato de respuesta
response_format = {
    "type": "object",
    "properties": {
        "title": {"type": "string"},
        "points": {"type": "array", "items": {"type": "string"}}
    }
}
```

### Versión Síncrona

```python
messages = [
    {"role": "user", "content": "Dame los puntos principales sobre el cambio climático."}
]

response = ai.str_output(
    messages=messages,
    response_format=response_format
)
```

### Versión Asíncrona

```python
async def structured_output_example():
    messages = [
        {"role": "user", "content": "Dame los puntos principales sobre el cambio climático."}
    ]
    
    response = await ai.str_output(
        messages=messages,
        response_format=response_format
    )
```

## Embeddings

### Versión Síncrona

```python
# Generar embeddings para un texto
text = "Este es un ejemplo de texto para generar embeddings."
response = ai.embeddings(text)

# Calcular similitud coseno entre dos textos
text1 = "Hola mundo"
text2 = "Saludos mundo"

emb1 = ai.embeddings(text1).data[0].embedding
emb2 = ai.embeddings(text2).data[0].embedding

similarity = ai.cosine_similarity(emb1, emb2)
print(f"Similitud: {similarity}")
```

### Versión Asíncrona

```python
async def embeddings_example():
    text = "Este es un ejemplo de texto para generar embeddings."
    response = await ai.embeddings(text)
    
    # Calcular similitud
    text1 = "Hola mundo"
    text2 = "Saludos mundo"
    
    emb1 = (await ai.embeddings(text1)).data[0].embedding
    emb2 = (await ai.embeddings(text2)).data[0].embedding
    
    similarity = ai.cosine_similarity(emb1, emb2)
    print(f"Similitud: {similarity}")
```

## Speech to Text (STT)

### Versión Síncrona

```python
# Transcribir audio
transcription = ai.transcribe(
    file_path="audio.mp3",
    language="es",
    response_format="text"
)
print(transcription)

# Traducir audio a inglés
translation = ai.translate(
    file_path="audio.mp3",
    response_format="text"
)
print(translation)
```

### Versión Asíncrona

```python
async def stt_example():
    # Transcribir audio
    transcription = await ai.transcribe(
        file_path="audio.mp3",
        language="es",
        response_format="text"
    )
    print(transcription)
    
    # Traducir audio a inglés
    translation = await ai.translate(
        file_path="audio.mp3",
        response_format="text"
    )
    print(translation)
```

## Text to Speech (TTS)

### Versión Síncrona

```python
# Generar audio a partir de texto
text = "Hola, esto es una prueba de texto a voz."
ai.speech(
    text=text,
    output_file_path="output.mp3",
    voice="nova",
    speed=1.2
)
```

### Versión Asíncrona

```python
async def tts_example():
    text = "Hola, esto es una prueba de texto a voz."
    await ai.speech(
        text=text,
        output_file_path="output.mp3",
        voice="nova",
        speed=1.2
    )
```

## Manejo de Errores

Todas las funciones incluyen manejo de errores y logging. Los errores se registran usando el módulo de logging configurado.

```python
try:
    response = ai.chat(messages)
    if response is None:
        print("Ocurrió un error en la llamada a la API")
except Exception as e:
    print(f"Error inesperado: {e}")
```

## Parámetros Comunes

### Modelos Disponibles
- Chat: gpt-4, gpt-35-turbo
- Embeddings: text-embedding-3-small, text-embedding-ada-002, text-embedding-3-large
- TTS: tts-1, tts-1-hd
- STT: whisper-1

### Voces Disponibles para TTS
- alloy
- echo
- fable
- onyx
- nova
- shimmer

### Formatos de Respuesta
- Chat: text, json_object
- Audio: mp3, opus, aac, flac, pcm
- Transcripción: json, text, srt, verbose_json, vtt

## Mejores Prácticas

1. **Manejo de Recursos**
   ```python
   # Usar context managers para archivos
   with open("audio.mp3", "rb") as audio_file:
       transcription = ai.transcribe(audio_file)
   ```

2. **Configuración de Temperatura**
   - Valores bajos (0.0-0.3): Respuestas más deterministas
   - Valores medios (0.3-0.7): Balance entre creatividad y coherencia
   - Valores altos (0.7-1.0): Respuestas más creativas

3. **Gestión de Tokens**
   ```python
   # Configurar max_tokens según necesidades
   ai = AzureAI(max_tokens=500)
   ```

4. **Uso Asíncrono Eficiente**
   ```python
   async def process_multiple():
       tasks = [
           ai.chat(messages1),
           ai.chat(messages2),
           ai.chat(messages3)
       ]
       results = await asyncio.gather(*tasks)
   ```

## Ejemplos Completos

### Análisis de Sentimiento con Salida Estructurada

```python
from pydantic import BaseModel

class SentimentAnalysis(BaseModel):
    sentiment: str
    confidence: float
    key_points: list[str]

sentiment_format = {
    "type": "object",
    "properties": {
        "sentiment": {"type": "string"},
        "confidence": {"type": "number"},
        "key_points": {"type": "array", "items": {"type": "string"}}
    }
}

messages = [
    {"role": "system", "content": "Analiza el sentimiento del siguiente texto."},
    {"role": "user", "content": "El servicio fue excelente y el personal muy amable."}
]

response = ai.str_output(messages, sentiment_format)
print(response)
```

### Pipeline de Procesamiento de Audio

```python
async def audio_pipeline():
    # 1. Transcribir audio
    transcription = await ai.transcribe("input.mp3", language="es")
    
    # 2. Analizar contenido
    messages = [
        {"role": "user", "content": f"Resume este texto: {transcription}"}
    ]
    summary = await ai.chat(messages)
    
    # 3. Convertir resumen a audio
    await ai.speech(
        text=summary.choices[0].message.content,
        output_file_path="summary.mp3"
    )
```

## Soporte y Contribuciones

Para reportar problemas o contribuir al desarrollo, por favor:
1. Abre un issue en el repositorio
2. Describe el problema o mejora propuesta
3. Sigue las guías de contribución del proyecto

## Licencia

Este proyecto está licenciado bajo MIT License.