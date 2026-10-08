---
tags:
  - taller-ia
  - modulo-2
  - modelos
modulo: 2
aliases:
  - Clasificación de modelos
  - Modelos de razonamiento
  - Modelos multimodales
  - Pesos abiertos
---

> [!info] Qué resuelve esta nota
> No hay una sola clasificación de modelos. Esta nota presenta **tres ejes** que sirven para elegir: *qué hacen mejor* (razonamiento, código, multimodales), *qué alcance tienen* (especializados o generales) y *quién controla los pesos* (privados o de pesos abiertos). Ninguna de las categorías es «mejor» que otra: cada una tiene costos y usos.

## Eje 1. Por lo que hacen mejor

### Modelos de razonamiento

Dedican un tiempo a «pensar» antes de responder. En Claude, esa función se llama **pensamiento extendido** (*extended thinking*): se define un presupuesto de tokens de pensamiento y el modelo razona dentro de ese presupuesto antes de dar la respuesta final. La documentación señala varias consecuencias:

- **Se cobra.** Los tokens de pensamiento se facturan como tokens de salida, cuentan para los límites y **también para la ventana de contexto**.
- **Es más lento.** Presupuestos mayores permiten un razonamiento más completo, con rendimientos decrecientes según la tarea y a costa de mayor latencia.
- **El presupuesto es una meta, no un tope estricto**; el modelo puede detenerse antes.
- **Pensamiento adaptativo.** Donde está disponible, es el modo recomendado: Claude decide si piensa y cuánto en cada petición; con poco esfuerzo puede omitirlo en entradas fáciles.

> [!tip] Consejo
> Para una tarea sencilla (reformular una frase, clasificar un correo) pensar más no aporta y cuesta más. Para una tarea con varias condiciones (comparar contratos, depurar un cálculo) vale la pena probar un modelo de razonamiento y comparar el resultado.

### Modelos de código

Están **pensados para programar**. Sus empresas los describen así: Claude Opus 5.5, «programación agéntica de larga duración y trabajo del conocimiento»; Gemini 3.8 Flash, «ingeniería de software de larga duración, agentes autónomos y flujos empresariales complejos». Claude Fable 5.1 se describe para razonamiento exigente y trabajo agéntico de larga duración.

### Modelos multimodales

Trabajan con **más de un tipo de contenido**, como texto e imágenes. Según la documentación (a 7 de octubre de 2026), los modelos actuales de Claude y los GPT-6 aceptan texto e imágenes; OpenAI y Google ofrecen además modelos de voz e imagen y, en el caso de Google, de video. Los documentos y las imágenes que adjuntas cuentan dentro de la ventana de contexto (ver [[09 Ventana de contexto|Ventana de contexto]]).

### Tamaños

Dentro de cada familia hay modelos **grandes**, para el trabajo más exigente, y **pequeños**, para velocidad y costo. Por ejemplo, Claude Haiku 5.5 se describe para tareas de alto volumen y baja latencia como clasificación, extracción y enrutamiento. Ver la tabla de [[02 Modelo, aplicación y agente|Modelo, aplicación y agente]].

## Eje 2. Por alcance: especializados y generales

| | Especializados | Generales |
| :--- | :--- | :--- |
| Qué son | Hechos para **una sola función** | **Un solo modelo** cubre muchas funciones |
| Ejemplos | AlphaFold (predice la forma 3D de una proteína a partir de su secuencia). YOLO (reconoce los objetos de una imagen de un solo vistazo; su artículo de 2015 reporta 45 imágenes por segundo en su versión base). Otros usos: diseño de motores, conducción autónoma. | Redactar, programar, analizar imágenes y usar herramientas. Ejemplos: los modelos de [[02 Modelo, aplicación y agente|Modelo, aplicación y agente]]. |

> [!note] Cómo decidir
> Que un modelo te sirva se comprueba, no se supone: la guía de Claude recomienda definir criterios de éxito y probarlo con tus propios casos (ver [[13 Pruebas de referencia|Pruebas de referencia]]).

### La AGI

La **inteligencia artificial general** (AGI) es un término que las empresas definen cada una a su manera. La Carta de OpenAI la define como «sistemas altamente autónomos que superan a los humanos en la mayor parte del trabajo económicamente valioso», y Google DeepMind la menciona como horizonte de la IA. Que los modelos generales sean un paso hacia la AGI es la **postura que declaran esas empresas**, no un hecho demostrado.

> [!question] Para pensar
> En tu campo, ¿conviene más un modelo general o uno dedicado? ¿Qué criterios usarías para decidir (costo, precisión, privacidad, facilidad de uso)?

## Eje 3. Por acceso: privados y de pesos abiertos

Los **pesos** son lo que el modelo aprendió al entrenarse (ver [[05 Pesos y parámetros|Pesos y parámetros]]). La diferencia es si la empresa los publica.

| | Privado (propietario o cerrado) | De pesos abiertos |
| :--- | :--- | :--- |
| Pesos | La empresa los conserva; no se publican | La empresa los publica y cualquiera puede descargarlos |
| Cómo se usa | Desde su aplicación o conectándolo a otros programas mediante su interfaz de programación (API) | Se puede ejecutar por cuenta propia, según su licencia |
| Ejemplos | Claude, ChatGPT (GPT-6), Gemini | DeepSeek-R1 (licencia MIT) y gpt-oss de OpenAI (licencia Apache 2.0) |

Detalles:

- **DeepSeek-R1.** Su ficha en Hugging Face indica que el código y los pesos tienen licencia MIT, con uso comercial, modificación y trabajos derivados permitidos.
- **gpt-oss** (OpenAI, 5 de agosto de 2025). Dos modelos de pesos abiertos, de 117 y 21 mil millones de parámetros en total, con licencia Apache 2.0, descargables en Hugging Face. Según OpenAI, el de 21 mil millones puede ejecutarse en dispositivos con 16 GB de memoria y el de 117 mil millones, en una sola unidad de procesamiento gráfico (GPU) de 80 GB. OpenAI presenta estos modelos como sus primeros de pesos abiertos desde GPT-2.

> [!warning] Pesos abiertos no es lo mismo que código abierto
> La «Definición de IA de código abierto 1.0» (*Open Source AI Definition 1.0*) de la Iniciativa de Código Abierto (OSI, 28 de octubre de 2024) pide que un sistema permita usarlo, estudiarlo, modificarlo y compartirlo, y exige tres componentes: información suficientemente detallada sobre los **datos de entrenamiento**, el **código completo** para entrenar y ejecutar el sistema y los **parámetros**. Publicar solo los pesos no cumple todo eso. Además, cada licencia tiene sus propias condiciones: léela antes de usar el modelo.

> [!note] Para ejecutarlos
> Ejecutar modelos por cuenta propia es posible con herramientas como Ollama (ver [[Inteligencia artificial]]), según los requisitos de hardware de cada modelo.

## Fuentes

- Claude, [pensamiento extendido](https://platform.claude.com/docs/en/build-with-claude/extended-thinking) y [ventanas de contexto](https://platform.claude.com/docs/en/build-with-claude/context-windows).
- Documentación de modelos: [Anthropic](https://platform.claude.com/docs/en/models/overview), [OpenAI](https://developers.openai.com/api/docs/models), [Google](https://ai.google.dev/gemini-api/docs/models).
- [AlphaFold](https://alphafold.com/) · Redmon et al., 2015, [YOLO](https://arxiv.org/abs/1506.02640).
- [Carta de OpenAI](https://openai.com/charter/) · [Google DeepMind](https://deepmind.google/about/).
- [DeepSeek-R1, ficha en Hugging Face](https://huggingface.co/deepseek-ai/DeepSeek-R1) · OpenAI, [gpt-oss](https://openai.com/index/introducing-gpt-oss/) · OSI, [Open Source AI Definition 1.0](https://opensource.org/ai/open-source-ai-definition).

## Siguiente

Con los tipos de modelo claros, falta ver qué cambia cuando el modelo trabaja solo: [[12 Chat y agente|Chat y agente]].

← [[00 Módulo II - Índice]]
