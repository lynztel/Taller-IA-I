---
tags:
  - taller-ia
  - modulo-2
  - probabilidad
modulo: 2
aliases:
  - Azar al responder
  - Siguiente palabra
  - Temperatura
---

> [!info] Qué resuelve esta nota
> Un modelo de lenguaje no «busca» la respuesta: **calcula, para cada fragmento posible, la probabilidad de que siga al texto actual, y elige uno**. Como en la elección interviene el azar, la misma instrucción puede dar respuestas distintas. Entender esto ayuda a decidir cuándo variar es útil y cuándo estorba.

## El bucle de generación

1. El modelo recibe el texto actual (la instrucción más lo que ya generó).
2. Calcula una **distribución de probabilidad** sobre los fragmentos que podrían seguir.
3. **Elige uno**, según esas probabilidades.
4. Lo agrega al texto y vuelve al paso 1.

Según Raschka, el entrenamiento enseña al modelo a asignar alta probabilidad al fragmento que realmente sigue; la generación usa esas mismas probabilidades condicionales en otro ciclo: se elige un fragmento, se agrega y se vuelve a alimentar. La continuación es desconocida, así que **cada paso futuro no se puede calcular por adelantado** (ver [[03 Cómo se construye un modelo|Cómo se construye un modelo]]).

## Cuando casi todo cae en una opción… y cuando no

> [!example] Ejemplo (probabilidades ilustrativas, no medidas de un modelo real)
> **Probabilidad concentrada.** Texto: «La capital de Francia es…». Un resultado ilustrativo: *París* 97 %, otras opciones 3 % entre todas. Casi siempre saldrá lo mismo.
>
> **Probabilidad repartida.** Texto: «Había una vez un…».
>
> | Fragmento | Probabilidad |
> | :--- | :-: |
> | rey | 40 % |
> | niño | 27 % |
> | dragón | 18 % |
> | otros | 15 % |
>
> Cada vez que se genera, se elige una opción al azar **según su probabilidad**. Primera vez: «Había una vez un **rey**…». Segunda vez: «Había una vez un **dragón**…». El mismo comienzo puede dar historias muy distintas, porque cada elección abre caminos diferentes.

## Qué dice la documentación sobre el azar

La documentación de la interfaz de programación (API) de Claude describe el parámetro de temperatura (`temperature`) como la **cantidad de aleatoriedad inyectada en la respuesta**, entre 0.0 y 1.0, con valor por defecto de 1.0. Sugiere acercarlo a 0.0 para tareas analíticas o de opción múltiple y a 1.0 para tareas creativas y generativas. Dos advertencias importantes:

- Incluso con `temperature` en 0.0, **los resultados no son del todo deterministas**.
- Los modelos publicados después de Claude Opus 4.6 ya **no permiten cambiar** ese parámetro: solo aceptan 1.0 (la documentación lo marca como obsoleto). Es un ejemplo de cómo los controles disponibles cambian con las generaciones.

> [!warning] Ni con buenos ajustes
> Ni una buena instrucción ni un parámetro vuelven *determinista* a un modelo. Lo que se puede hacer es **reducir las opciones razonables** con instrucciones más completas.

## Cuándo ayuda y cuándo estorba

| Tarea | La variación… | Qué conviene |
| :--- | :--- | :--- |
| Lluvia de ideas, nombres, borradores creativos | **Ayuda**: más opciones por explorar | Pedir varias versiones y elegir |
| Resumir un documento, extraer datos, citar | **Estorba**: se quiere precisión y repetibilidad | Instrucción más precisa, criterios de aceptación y revisión de resultados |

Esta clasificación es coherente con la sugerencia de la documentación de usar menos aleatoriedad en tareas analíticas.

> [!example] Pruébalo
> Pide la misma instrucción tres veces en conversaciones nuevas y compara las respuestas. Luego escribe una versión más completa (con restricciones y criterios, ver [[17 Anatomía de una instrucción|Anatomía de una instrucción]]) y repite. Observa si las tres respuestas se parecen más entre sí. Es un experimento para entender el efecto, no una garantía.

## Fuentes

- Raschka, [predicción del siguiente token](https://sebastianraschka.com/faq/docs/next-token-prediction.html).
- Claude API, [crear un mensaje](https://platform.claude.com/docs/en/api/messages/create): parámetro `temperature`.

## Siguiente

Qué entra al modelo además de tu mensaje: [[08 Qué recibe el modelo|Qué recibe el modelo]].

← [[00 Módulo II - Índice]]
