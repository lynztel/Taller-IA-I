---
tags:
  - taller-ia
  - modulo-2
  - modelos
modulo: 2
aliases:
  - Modelo vs aplicación vs agente
  - Modelos actuales
---

> [!info] Qué resuelve esta nota
> En la conversación diaria, «la IA» nombra tres cosas distintas: el **modelo**, la **aplicación** donde lo usas y el **agente** que actúa con herramientas. Separarlas evita errores como pensar que cambiar de aplicación es cambiar de modelo, o que un chat y un agente son lo mismo. La definición de agente sigue la de Anthropic.

## Las tres piezas

| Pieza | Qué es | Ejemplos |
| :--- | :--- | :--- |
| **Modelo** | Sistema entrenado que recibe texto o, según el modelo, imágenes, y genera una respuesta. | Claude Sonnet 5.5, GPT-6 Astra, Gemini 3.8 Flash |
| **Aplicación** | Programa donde usas un modelo. Añade interfaz, historial, archivos y herramientas. | ChatGPT, Claude, Gemini |
| **Agente** | Un sistema donde el modelo dirige dinámicamente su propio proceso y el uso de herramientas para cumplir una meta (definición de Anthropic). | Ejemplo: uno que lee tus archivos y prepara un informe |

> [!example] Analogía
> El modelo es el **motor**; la aplicación es el **vehículo completo** (tablero, asientos, controles); el agente es un vehículo que, además, **elige la ruta** una vez que le das el destino. Sirve para recordar que el motor solo no es el producto.

### Por qué importa la diferencia

- **Al comparar:** los resultados de una prueba (ver [[13 Pruebas de referencia|Pruebas de referencia]]) pertenecen a un *modelo*, no a una aplicación. Una aplicación puede ofrecer distintos modelos (conviene revisar cuál estás usando).
- **Al revisar privacidad y costos:** el historial, los archivos adjuntos y las herramientas los aporta la *aplicación*; en la interfaz de programación (API) de OpenAI el precio se calcula por tokens (ver [[04 Tokens e incrustaciones|Tokens e incrustaciones]]).
- **Al delegar trabajo:** un chat y un agente exigen cuidados distintos (ver [[12 Chat y agente|Chat y agente]]).

## Modelos actuales (a 8 de octubre de 2026)

Cada empresa ofrece modelos más capaces y otros más rápidos o económicos.

| Empresa | Modelo | Para qué lo describe la empresa |
| :--- | :--- | :--- |
| Anthropic | Claude Fable 5.1 | Razonamiento exigente y trabajo agéntico de larga duración |
| | Claude Opus 5.5 | Programación agéntica de larga duración y trabajo del conocimiento |
| | Claude Sonnet 5.5 | La mejor combinación de velocidad e inteligencia |
| | Claude Haiku 5.5 | Tareas de alto volumen y baja latencia: clasificación, extracción, enrutamiento y tareas de subagentes (publicado el 7 de octubre de 2026) |
| OpenAI | GPT-6 Astra | El más capaz, para el trabajo más exigente |
| | GPT-6.1 Sol | Rendimiento cercano a Astra para trabajo complejo, a menor costo |
| | GPT-6 Luna | El más eficiente, para tareas enfocadas de alto volumen |
| Google | Gemini 3.8 Flash | Su modelo Flash más inteligente, para ingeniería de software de larga duración y agentes autónomos |
| | Gemini 3.1 Pro (vista previa) | Inteligencia avanzada, resolución de problemas complejos y capacidades de agente |
| | Gemini 3.5 Flash-Lite | El modelo más rápido y rentable de la serie 3.5 |

> [!warning] Esta tabla caduca
> Claude Haiku 5.5 se publicó el 7 de octubre de 2026. Las empresas renuevan sus familias cada pocos meses. Antes de citar un nombre o una ventana de contexto, abre la página oficial: [Claude](https://platform.claude.com/docs/en/models/overview) · [OpenAI](https://developers.openai.com/api/docs/models) · [Google](https://ai.google.dev/gemini-api/docs/models).

### Cómo leer los nombres

- **Familia y tamaño.** Dentro de cada familia hay un modelo para el trabajo más exigente y otros más pequeños, rápidos y baratos (la propia documentación de Claude describe a Haiku como el más rápido y a Fable como el de razonamiento exigente). Más en [[11 Tipos de modelo|Tipos de modelo]].
- **Versión.** El número cambia con las generaciones (por ejemplo, 5.5 frente a 4.5). Que un número sea mayor no dice por sí solo cuál sirve para *tu* tarea.
- **Estado.** Google marca algunos modelos como *vista previa* (*preview*) y otros como estables. Si vas a depender de un modelo, revisa cuál es su estado en la página oficial.

### Cómo elegir

La documentación de Claude recomienda definir criterios de éxito según tu caso de uso y probar con tus propias tareas (ver [[13 Pruebas de referencia|Pruebas de referencia]] y [[17 Anatomía de una instrucción|Anatomía de una instrucción]]). Una forma práctica: toma una tarea real, escribe tres criterios que puedas comprobar y pruébala en dos modelos de distinto tamaño. Compara resultado, tiempo y costo.

## Qué cambia cuando hay agente

Un agente no es un modelo distinto: es un **modelo usado de otra forma**. Recibe una meta, decide los pasos, usa herramientas (leer archivos, buscar, ejecutar código) y revisa el resultado de cada paso antes de seguir. Anthropic distingue los *flujos de trabajo* (pasos definidos por código) de los *agentes* (el modelo decide). El ciclo y sus riesgos se explican en [[12 Chat y agente|Chat y agente]]; las formas de combinar varios modelos, en [[14 Orquestación de agentes|Orquestación de agentes]].

## Fuentes

- Anthropic, [*Building effective agents*](https://www.anthropic.com/research/building-effective-agents): definición de agente y de flujo de trabajo.
- Documentación de modelos: [Anthropic](https://platform.claude.com/docs/en/models/overview), [Claude Haiku 5.5](https://platform.claude.com/docs/en/models/haiku-5-5/overview), [OpenAI](https://developers.openai.com/api/docs/models), [Google](https://ai.google.dev/gemini-api/docs/models).
- Claude, [definir criterios de éxito](https://platform.claude.com/docs/en/test-and-evaluate/define-success).

## Siguiente

Ahora, cómo se fabrica un modelo: [[03 Cómo se construye un modelo|Cómo se construye un modelo]].

← [[00 Módulo II - Índice]]
