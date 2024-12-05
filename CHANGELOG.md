# Changelog

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [0.1.11] - 2024-12-04

### Updates
- Actualización de dependencias.
  
## [0.1.10] - 2024-10-20

### Fixed
- Corrección de errores menores en la clase `Tool` relacionados con el registro automático en `Toolbox`.
- Solución de problemas de inicialización en `AzureAI` cuando faltan variables de entorno.
- Ajustes en el manejo de excepciones para mejorar la estabilidad general del sistema.

## [0.1.9] - 2024-10-15

### Añadido
- Implementación de métodos asíncronos para Speech-to-Text (STT) y Text-to-Speech (TTS).
- Nueva clase `AsyncOpenAI` para manejar interacciones asíncronas con OpenAI.
- Método `speech()` asíncrono para generación de audio a partir de texto.
- Método `transcribe()` asíncrono para transcripción de audio a texto.

### Cambiado
- Refactorización de la clase `OpenAI` para mejorar la gestión de errores.
- Actualización de la documentación para incluir ejemplos de uso de métodos asíncronos.

### Eliminado
- Eliminación de métodos obsoletos en la clase `OpenAI`.

## [0.1.8] - 2024-10-10

### Añadido
- Soporte para nuevos modelos de voz en el método `speech()`.
- Parámetros adicionales para personalizar la generación de audio.

### Cambiado
- Mejora en el manejo de excepciones en el método `translate()`.
- Optimización del rendimiento en la generación de embeddings.

## [0.1.7] - 2024-10-05

### Añadido
- Integración con la librería `aiofiles` para operaciones de archivo asíncronas.
- Nuevas opciones de formato de respuesta en el método `chat()`.

### Cambiado
- Refactorización del método `speech()` para soportar múltiples formatos de audio.
- Actualización de dependencias en `requirements.txt`.

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
