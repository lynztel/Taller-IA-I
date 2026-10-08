---
tags:
  - taller-ia
  - modulo-2
  - benchmarks
modulo: 2
aliases:
  - Benchmarks
  - Lectura crítica de benchmarks
  - Métricas de las empresas
  - Evaluación de modelos
---

> [!info] Qué resuelve esta nota
> Las empresas presentan sus modelos con tablas de puntuaciones. Una **prueba de referencia** (*benchmark*) es una prueba estándar con la que se compara a los modelos. Una cifra solo significa algo si sabes **qué mide la prueba, cómo se aplicó y qué vio el modelo antes**. Esta nota explica tres pruebas muy citadas, cuatro razones por las que una cifra puede engañar y cinco preguntas para leerlas sin caer en el marketing.

## Tres pruebas muy citadas

### GPQA

Una prueba de **448 preguntas de opción múltiple** de biología, física y química, **escritas por personas expertas** de cada campo. Al publicarse (noviembre de 2023), expertos con doctorado o cursándolo acertaron 65 % (74 % si se excluyen errores evidentes que ellos mismos identificaron después). Personas no expertas muy capaces, con más de 30 minutos de acceso libre a internet, acertaron 34 %. El mejor sistema basado en GPT-4 alcanzó 39 %.

### SWE-bench

**2,294 problemas de ingeniería de software** tomados de reportes reales (*issues*) en GitHub, de **12 repositorios populares de Python**. El modelo recibe el código y la descripción del problema y debe **editar el código** para resolverlo. La métrica es el porcentaje de problemas resueltos. Al publicarse, el mejor modelo (Claude 2) resolvía el 1.96 %.

> [!example] Para ver cuánto cambian las cifras
> Ese 1.96 % es la cifra **del momento de la publicación del artículo**, no la actual. Es un buen recordatorio de que las puntuaciones envejecen rápido: la prueba que parecía casi imposible deja de distinguir a los modelos en pocos años.

**SWE-bench Verified** es un subconjunto de **500 casos revisados por personas**. Se explica abajo.

### Chatbot Arena

Una plataforma abierta donde **personas comparan las respuestas de dos modelos y votan por la mejor**. La clasificación sale de esos votos con métodos estadísticos. Tenía más de 240 mil votos al publicarse el artículo (marzo de 2024). Los autores reportan que las preguntas de los usuarios son diversas y discriminantes y que los votos coinciden bien con los de evaluadores expertos.

| Prueba | Qué mide | Quién decide si está bien | Límite a considerar |
| :--- | :--- | :--- | :--- |
| GPQA | Conocimiento y razonamiento en ciencias (opción múltiple) | Respuesta correcta fijada por expertos | Una sola respuesta correcta; no mide redacción ni tareas largas |
| SWE-bench | Resolver problemas reales de programación | Pruebas automáticas del repositorio | Solo Python y GitHub; las pruebas pueden tener errores |
| Chatbot Arena | Preferencia de personas entre dos respuestas | Votos de usuarios | Mide preferencia, no necesariamente corrección |

## Cuatro razones por las que una cifra puede engañar

### 1. La prueba ya quedó fácil

El artículo de «El último examen de la humanidad» (*Humanity's Last Exam*, HLE) señala que los modelos ya superan 90 % de precisión en pruebas populares como MMLU. Cuando casi todos sacan lo mismo, la prueba deja de distinguir. Por eso se creó **MMLU-Pro**: amplió las opciones de **4 a 10** y añadió preguntas de razonamiento; la precisión de los modelos **bajó entre 16 y 33 %** respecto a MMLU. HLE propone otra respuesta al mismo problema: 2,500 preguntas escritas por expertos de todo el mundo, con respuestas verificables que no se encuentran con una búsqueda rápida.

### 2. La prueba tiene errores

OpenAI revisó **1,699 muestras** de SWE-bench con **93 desarrolladores de Python** y descartó **68.3 %**: 38.3 % por enunciados incompletos y 61.1 % por pruebas unitarias que podían rechazar soluciones válidas (los porcentajes se traslapan). De ahí salieron los **500 casos de SWE-bench Verified**. Con el mejor marco de código abierto en ese momento (Agentless), OpenAI reporta que GPT-4o resuelve **33.2 %** de SWE-bench Verified, aproximadamente el doble del 16 % que ese tipo de marcos lograba en la prueba original. Según OpenAI, la prueba original **subestimaba la capacidad de los modelos** por esos problemas: es decir, parte de lo que parecía un límite del modelo era un defecto de la prueba.

### 3. El modelo pudo ver las preguntas

**Contaminación**: Chen et al. (2025) la definen como la inclusión involuntaria de datos de la prueba en el entrenamiento, lo que lleva a evaluaciones infladas y engañosas. Otro artículo de revisión (Xu et al.) la describe como incorporar información de la prueba al entrenarse, lo que vuelve poco confiable la evaluación.

> [!example] Analogía
> Es como estudiar con la **copia del examen**: sacas una gran calificación, pero no demuestras que sabes la materia.

Una respuesta de diseño: **LiveBench** usa preguntas de fuentes recientes (competencias de matemáticas, artículos de arXiv, noticias) y las **agrega y actualiza cada mes**, con calificación automática contra valores de referencia objetivos.

### 4. La forma de preguntar cambia el resultado

El artículo de MMLU-Pro midió 24 estilos de instrucción: la variación de la puntuación fue de **4 a 5 % en MMLU** y de **2 % en MMLU-Pro**. Es decir, cambiar un poco la instrucción (*prompt*) mueve la puntuación. Si dos empresas reportan la misma prueba con instrucciones distintas, **no son comparables**.

Y un quinto cuidado, de Kalai et al. (2025): si una prueba **no da crédito por responder «no sé»**, los modelos aprenden a adivinar y las tablas de clasificación premian eso (ver [[10 Alucinaciones|Alucinaciones]]).

## Cinco preguntas antes de creer un resultado

Se derivan de los casos anteriores.

| # | Pregunta | Qué buscas | Apoyo en los casos |
| :-: | :--- | :--- | :--- |
| 1 | **¿Quién lo midió?** | Si lo midió la empresa que vende el modelo o un tercero | SWE-bench distingue en su sitio los resultados que su equipo ejecutó o verificó |
| 2 | **¿En qué condiciones?** | Cómo se aplicó: instrucción, número de ejemplos, herramientas | La instrucción (*prompt*) mueve la puntuación (4 a 5 % en MMLU) |
| 3 | **¿Qué otras pruebas hay?** | Qué otras pruebas existen para esa tarea y si también se reportaron | Una sola prueba puede estar saturada o tener errores |
| 4 | **¿Todavía distingue?** | Si casi todos los modelos sacan lo mismo, la prueba ya no ayuda | MMLU se estancó; por eso se creó MMLU-Pro |
| 5 | **¿Mide lo que necesito?** | Que la prueba se parezca a *tu* tarea | La guía de Claude recomienda definir criterios de éxito para tu caso de uso |

> [!example] Analogía
> Un auto no se juzga solo por su **velocidad máxima**: importan el consumo, la seguridad y el uso que le darás. Igual con un modelo: la mejor puntuación en una prueba no es la mejor elección para tu tarea.

> [!example] Ejemplo (cifra inventada)
> «Nuestro nuevo modelo obtiene 92 % en la prueba X.» Preguntas: ¿quién midió el 92 %?, ¿con qué instrucción y cuántos ejemplos?, ¿cuánto sacan los demás modelos en esa prueba?, ¿la prueba se publicó antes del entrenamiento (riesgo de contaminación)?, ¿se parece a lo que yo necesito hacer?

### Cómo aplicarlo a tu caso

La guía de Claude pide criterios de éxito **específicos y medibles**, por ejemplo: en lugar de «salidas seguras», «menos de 0.1 % de salidas marcadas por un filtro de toxicidad en 10,000 pruebas». Para tu tarea, construye una mini-prueba propia: 5 a 10 ejemplos reales, un criterio de revisión por cada uno y la misma instrucción para todos los modelos (ver [[17 Anatomía de una instrucción|Anatomía de una instrucción]]).

> [!note] Comparadores
> Sitios como Artificial Analysis y LLM Stats reúnen métricas, velocidades y costos; son **independientes** y no sustituyen a las fuentes oficiales ni a las pruebas de tu caso. Están en [[Laboratorio de tokens y modelos]].

## Fuentes

- Rein et al., [GPQA (arXiv 2311.12022)](https://arxiv.org/abs/2311.12022) · Jimenez et al., [SWE-bench (arXiv 2310.06770)](https://arxiv.org/abs/2310.06770) · OpenAI, [SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/) · Chiang et al., [Chatbot Arena (arXiv 2403.04132)](https://arxiv.org/abs/2403.04132).
- [Humanity's Last Exam (arXiv 2501.14249)](https://arxiv.org/abs/2501.14249) · [MMLU-Pro (arXiv 2406.01574)](https://arxiv.org/abs/2406.01574).
- Contaminación: Xu et al., [arXiv 2406.04244](https://arxiv.org/abs/2406.04244) · Chen et al., [arXiv 2502.17521](https://arxiv.org/abs/2502.17521) · [LiveBench (arXiv 2406.19314)](https://arxiv.org/abs/2406.19314).
- Kalai et al., [*Why Language Models Hallucinate*](https://arxiv.org/abs/2509.04664).
- Claude, [definir criterios de éxito](https://platform.claude.com/docs/en/test-and-evaluate/define-success).

## Siguiente

Con criterio para leer métricas, se puede planear cómo combinar varios modelos: [[14 Orquestación de agentes|Orquestación de agentes]].

← [[00 Módulo II - Índice]]
