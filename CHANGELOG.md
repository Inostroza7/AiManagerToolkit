# Changelog

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.6] - 2024-10-01

### HotFix

## [0.1.4] - 2024-10-01

### Fix
- Fix en 'messages'

### Añadido
- Soporte para modelos de embeddings de Azure OpenAI.
- Nuevo método `embeddings()` para generar representaciones vectoriales de texto.
- Funcionalidad de Speech-to-Text (STT) con el método `transcribe()`.
- Funcionalidad de Text-to-Speech (TTS) con el método `speech()`.
- Método `translate()` para traducir audio a texto en inglés.
- Función `cosine_similarity()` para calcular la similitud entre vectores.

### Cambiado
- Refactorización completa para utilizar exclusivamente Azure OpenAI API.
- Actualización de la inicialización del cliente para usar `AzureOpenAI` en lugar de `OpenAI`.
- Modificación del método `chat()` para adaptarse a la API de Azure OpenAI.
- El parámetro `model` en el constructor ahora se refiere al deployment de Azure OpenAI.

### Eliminado
- Soporte para OpenAI API estándar.
- Clase `OpenAiToolkit` removida en favor de `AzureAiToolkit`.

## [0.1.1] - 2024-09-23

### Añadido
- Implementación inicial de `AzureAiToolkit` con soporte básico para Azure OpenAI.
- Métodos `chat()` y `stream()` para interacciones de chat.
- Método `str_output()` para generar salidas estructuradas.

### Cambiado
- Actualización de la documentación para reflejar el enfoque en Azure OpenAI.

## [0.1.0] - 2024-09-01

### Añadido
- Versión inicial de `OpenAiToolkit` con soporte para OpenAI API.
- Funcionalidades básicas de chat y completación de texto.
- Sistema de logging configurable.
