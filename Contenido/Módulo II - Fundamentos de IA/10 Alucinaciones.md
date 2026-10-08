---
tags:
  - taller-ia
  - modulo-2
  - alucinaciones
modulo: 2
aliases:
  - Alucinación
  - Hallucination
---

> [!info] Qué resuelve esta nota
> A veces el modelo responde con seguridad algo que no es cierto. A eso se le llama **alucinación**. No es un fallo raro ni una señal de «mala intención»: tiene explicaciones técnicas, y se puede reducir su efecto con hábitos concretos de instrucción y revisión.

## Qué son

Kalai et al. (2025) describen las alucinaciones como **afirmaciones plausibles pero incorrectas, dichas en lugar de admitir incertidumbre**. Lo importante es el contraste: el problema no es solo que el modelo se equivoque, sino que **suena convincente al hacerlo**.

> [!example] Ejemplo
> Le pides a un modelo, sin darle el documento, «¿qué conclusión da el artículo de Pérez (2019) sobre el trabajo híbrido?». Una respuesta con alucinación puede incluir una conclusión detallada, con cifras y una cita con apariencia correcta, de un artículo que el modelo no tiene o que ni siquiera existe.

## Por qué ocurren

Según Kalai et al., los modelos alucinan porque **los procedimientos de entrenamiento y evaluación premian adivinar sobre reconocer incertidumbre**. Explican que persisten porque las pruebas con las que se evalúa a los modelos dan puntos por acertar y no dan crédito por responder «no sé»; así, adivinar conviene, y los modelos terminan siendo buenos para presentar exámenes. Proponen una solución sociotécnica: **modificar el puntaje de las pruebas existentes** que no están alineadas pero que dominan las tablas de clasificación (ver [[13 Pruebas de referencia|Pruebas de referencia]]).

> [!example] Analogía
> Es como un alumno que, en un examen donde un espacio en blanco vale cero y una respuesta incorrecta tampoco resta, siempre prefiere contestar algo aunque no esté seguro.

Hay un segundo factor, que viene de cómo se construye el modelo: según Raschka, el objetivo de predecir el siguiente fragmento **no da directamente etiquetas de corrección factual** ni de utilidad; esas propiedades dependen de los datos y de las etapas posteriores (ver [[03 Cómo se construye un modelo|Cómo se construye un modelo]]).

## Qué puedes hacer

Hábitos concretos para reducir su efecto:

1. **Dale una salida honesta.** Incluye en la instrucción qué hacer si no encuentra el dato: «Si algo no aparece en el texto, escribe "no aparece en el texto"». Es el criterio de aceptación más barato contra la alucinación (ver [[17 Anatomía de una instrucción|Anatomía de una instrucción]]).
2. **Pídele de dónde sale cada dato.** «Indica la página o el párrafo de donde sale cada afirmación.» Para documentos largos, la guía de Claude recomienda pedirle que **cite primero las partes relevantes** y solo después haga la tarea.
3. **Dale la información que necesita.** Si el modelo no tiene el documento, puede rellenar con lo más probable. Entrega el texto (ver [[08 Qué recibe el modelo|Qué recibe el modelo]]).
4. **Que investigue antes de responder.** La guía de Claude, en su sección de programación con agentes, incluye un ejemplo de instrucción que exige leer los archivos relevantes antes de hacer afirmaciones y no especular sobre lo que no ha abierto. El principio se extiende a cualquier agente que pueda consultar fuentes (ver [[12 Chat y agente|Chat y agente]]).
5. **Verifica las fuentes tú.** Revisa que los datos y las citas existan y digan lo que se afirma. Ninguna instrucción elimina el riesgo por completo.

> [!example] Ejemplo de instrucción con salida honesta
> «Resume el artículo adjunto en un párrafo de 120 palabras. Usa solo información que esté en el texto. Si el artículo no menciona el método o la muestra, escribe "no aparece en el texto" en lugar de suponerlo. Al final, indica las páginas en las que apoyas cada afirmación.»

> [!note] Las herramientas ayudan, pero no son una garantía
> Los autores de ReAct reportan que, en tareas de preguntas y verificación de hechos, permitir que el modelo consulte una interfaz de programación (API) de Wikipedia **reduce la alucinación y la propagación de errores** observadas en el razonamiento solo con cadena de pensamiento (*chain-of-thought*). Es un resultado de una tarea y un entorno concretos; no significa que un agente con herramientas no alucine.

## Fuentes

- Kalai et al., 2025, [*Why Language Models Hallucinate*](https://arxiv.org/abs/2509.04664).
- Raschka, [predicción del siguiente token](https://sebastianraschka.com/faq/docs/next-token-prediction.html).
- Claude, [buenas prácticas para escribir instrucciones (*prompting*)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices): contexto largo y «investigar antes de responder».
- Yao et al., 2022, [ReAct](https://arxiv.org/abs/2210.03629).

## Siguiente

Hasta aquí se vio cómo funciona *un* modelo. Ahora, cómo se clasifican: [[11 Tipos de modelo|Tipos de modelo]].

← [[00 Módulo II - Índice]]
