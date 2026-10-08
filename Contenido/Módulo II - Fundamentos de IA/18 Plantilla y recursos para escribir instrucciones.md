---
tags:
  - taller-ia
  - modulo-2
  - instrucciones
  - prompting
  - plantilla
modulo: 2
aliases:
  - Plantilla de prompt
  - Few-shot
  - Etiquetas XML
  - Rol en el prompt
  - Recursos de prompting
---

> [!info] Qué resuelve esta nota
> [[17 Anatomía de una instrucción|Anatomía de una instrucción]] explicó **qué** debe tener una instrucción. Aquí hay una **plantilla** para escribirla y **tres recursos** que, según las guías oficiales, mejoran el resultado: dar ejemplos, separar con etiquetas y asignar un rol. Todo se acompaña de ejemplos completos que puedes copiar y adaptar.

## La plantilla

Es un documento Markdown: se copia, se cambia lo que está entre corchetes y se pega en el modelo. Su orden (rol, contexto, tarea, restricciones, criterios) es la primera de las dos formas descritas en [[17 Anatomía de una instrucción|Anatomía de una instrucción]]; puedes reordenarlo según la guía de tu modelo.

```markdown
## Rol
[Quién debe ser el modelo: una frase]

## Contexto
[Documentos, datos y situación]

## Tarea
[Qué debe hacer: un verbo y un resultado]

## Restricciones
[Formato, extensión, tono y lo que no debe hacer]

## Criterios de aceptación
[Condiciones que se puedan comprobar]
```

### Tres consejos de la guía de Claude

1. **Pon los documentos largos antes de la pregunta.** La guía dice que colocar la consulta al final puede mejorar la calidad de la respuesta hasta un 30 % en sus pruebas, sobre todo con entradas complejas.
2. **Explica para qué sirve cada restricción.** El motivo ayuda al modelo a generalizar.
3. **Di lo que sí debe hacer**, no solo lo que no.

Y uno más: si la guía de tu modelo recomienda otro orden, cámbialo.

### Plantilla llena (ejemplo)

```markdown
## Rol
Eres revisor de textos profesionales.

## Contexto
Mi informe (adjunto) trata de trabajo híbrido en nuestra organización y lo
leerá la dirección. Es un borrador de 8 páginas.

## Tarea
Revisa el apartado 2 del informe y señala los tres problemas más graves de
argumentación.

## Restricciones
- Español de México.
- Para cada problema: cita la frase exacta del informe y explica por qué es
  un problema (esto me ayuda a corregirlo yo mismo, no a que lo reescribas).
- No reescribas el texto; solo señala.

## Criterios de aceptación
- Exactamente tres problemas, ordenados del más grave al menos grave.
- Cada uno incluye una cita textual del informe.
- Si no encuentras tres problemas reales, dilo en lugar de inventarlos.
```

Cambia el tipo de documento por el tuyo: un dictamen, un reporte contable, un trabajo escolar, una propuesta comercial. La estructura es la misma.

## Otras plantillas oficiales para comparar

No hay una plantilla única. Estas son las de dos proveedores (tomadas de sus guías; ver fuentes):

- **OpenAI, para GPT-4.1** — secciones sugeridas: rol y objetivo (*Role and Objective*), instrucciones (*Instructions*), pasos de razonamiento (*Reasoning Steps*), formato de salida (*Output Format*), ejemplos (*Examples*), contexto (*Context*) e instrucciones finales (*Final instructions*). La guía la presenta como «un buen punto de partida» y añade: *añade o quita secciones según tus necesidades y experimenta*.
- **Google, para Gemini 3** — separa dos bloques. En la *instrucción de sistema* van el rol, las instrucciones, las restricciones y el formato de salida; en el *mensaje del usuario*, el contexto, la tarea y una instrucción final.

Las tres (la anterior, la de OpenAI y la de Google) comparten lo esencial: rol, contexto, tarea, límites. Cambia el orden y dónde se coloca cada parte.

## Recurso 1: dar ejemplos

Mostrar cómo quieres el resultado suele ser más claro que describirlo. A esto se le llama instrucción con pocos ejemplos (*few-shot prompting*).

### Qué dicen las guías

- **Claude:** incluir de **3 a 5 ejemplos** para mejores resultados. Deben ser **relevantes** (reflejar tu caso real), **diversos** (cubrir casos límite y variar lo suficiente para que el modelo no capte patrones no deseados) y **estructurados** (envueltos en etiquetas `<example>`, o `<examples>` si son varios, para distinguirlos de las instrucciones).
- **Gemini:** recomienda **incluir siempre ejemplos**, y advierte que las instrucciones sin ellos suelen ser menos eficaces. También: que la estructura y el formato de los ejemplos sean **iguales** entre sí, para evitar respuestas con formatos no deseados.
- **Anthropic (ingeniería de contexto):** prefiere **curar ejemplos diversos y canónicos** en lugar de llenar la instrucción con una lista de casos límite.

### De dónde viene la idea

En el artículo de GPT-3, Brown et al. (2020) aplicaron el modelo **sin actualizaciones de gradiente ni ajuste fino**: la tarea y las demostraciones se especificaban solo mediante texto. Es el origen de la idea de dar ejemplos dentro de la instrucción (pocos ejemplos, *few-shot*, y aprendizaje en contexto, *in-context learning*). Aprender «en contexto» no cambia los pesos del modelo ([[05 Pesos y parámetros|Pesos y parámetros]]): los ejemplos solo están en la ventana de contexto mientras dure la conversación ([[09 Ventana de contexto|Ventana de contexto]]).

### Ejemplo

Tarea: clasificar el tono de comentarios de asistentes a una capacitación.

```text
Clasifica el tono de cada comentario como: positivo, neutro o negativo.
Responde solo con la etiqueta.

<examples>
<example>
Comentario: «La sesión estuvo muy clara, por fin entendí el proceso.»
Tono: positivo
</example>
<example>
Comentario: «Se revisó el punto de ayer; queda pendiente para el jueves.»
Tono: neutro
</example>
<example>
Comentario: «Fue confuso y no alcanzó el tiempo.»
Tono: negativo
</example>
</examples>

Comentario: «El material ayudó, pero faltó tiempo para practicar.»
Tono:
```

Observa tres decisiones: los ejemplos **cubren las tres categorías**, tienen **el mismo formato** y están **separados con etiquetas** de la instrucción. El último comentario es intencionalmente ambiguo: es un buen candidato para añadir un cuarto ejemplo si el modelo duda.

## Recurso 2: separar con etiquetas

Cuando una instrucción mezcla instrucciones, contexto, ejemplos y datos, puede no quedar claro dónde acaba una parte y empieza otra. La guía de Claude lo resuelve con **etiquetas** (formato de lenguaje de marcado extensible, XML):

- Las etiquetas ayudan a Claude a interpretar sin ambigüedad instrucciones complejas, **especialmente cuando mezclan instrucciones, contexto, ejemplos y entradas variables**.
- Envolver cada tipo de contenido en su propia etiqueta (por ejemplo `<instructions>`, `<context>`, `<input>`) **reduce las malas interpretaciones**.
- Usar nombres de etiqueta **consistentes y descriptivos** en todas tus instrucciones.

Los nombres de etiqueta no son un estándar fijo: eliges nombres que describan el contenido.

### Ejemplo

```text
<instrucciones>
Resume el documento para un compañero que no lo ha leído.
Un párrafo de 120 palabras, en español de México.
Si algo no aparece en el texto, escribe «no aparece en el texto».
</instrucciones>

<contexto>
Mi informe trata de trabajo híbrido; me interesa el método del estudio.
</contexto>

<documento>
[pega aquí el texto del artículo]
</documento>
```

Dos ventajas prácticas: puedes **reutilizar** el mismo bloque `<instrucciones>` cambiando solo `<documento>` y la estructura queda a la vista cuando vuelves a leerla.

> [!tip] Consejo
> Con texto largo, combina los recursos 1 y 2 con la regla de colocación: documento arriba entre etiquetas, instrucciones debajo. La guía de Claude también sugiere, para tareas con documentos largos, **pedirle que primero cite las partes relevantes** antes de ejecutar la tarea (ver [[09 Ventana de contexto|Ventana de contexto]]).

## Recurso 3: asignar un rol

La guía de Claude indica que **definir un rol en la instrucción de sistema enfoca el comportamiento y el tono del modelo**, y que *incluso una sola frase marca la diferencia*. Su ejemplo: «Eres un asistente de programación que se especializa en Python».

Ejemplos de una frase:

| Situación | Rol |
| :--- | :--- |
| Revisar un documento | «Eres revisor de textos profesionales.» |
| Estudiar | «Eres tutor que pide a la persona que intente primero y solo después da pistas.» |
| Redactar | «Eres editor que recorta sin cambiar el significado.» |
| Revisar un contrato | «Eres asistente jurídico que señala cláusulas ambiguas, sin reescribirlas.» |
| Revisar cuentas | «Eres asistente contable que detecta cifras que no cuadran e indica dónde.» |

Dos aclaraciones para no sobreestimarlo:

1. Un rol es una **instrucción**, no una persona: orienta el estilo y el enfoque, pero **no le da conocimiento que no tenga**. Un «experto en física cuántica» sigue sujeto a los límites de [[10 Alucinaciones|Alucinaciones]].
2. Que un rol enfoque el comportamiento y el tono no implica cifras de mejora para roles específicos: mide con tus propios criterios.

## Cómo combinar todo

Una instrucción completa usa las cuatro partes y los tres recursos:

```text
Eres revisor de textos profesionales.                         ← rol

<contexto>                                                    ← etiquetas
Informe de 8 páginas sobre trabajo híbrido;
lo leerá la dirección de la organización.
</contexto>

<documento>
[texto del informe]
</documento>

Tarea: señala los tres problemas más graves de argumentación del apartado 2.

Restricciones: cita la frase exacta; no reescribas; español de México.

Criterios: exactamente tres, de mayor a menor gravedad, cada uno con cita.
Si no hay tres problemas reales, dilo.

<example>                                                     ← ejemplo
Problema: «El ausentismo bajará porque sí.»
Por qué: afirma una causa sin evidencia ni mecanismo.
</example>
```

> [!warning] Estos recursos complementan, no reemplazan
> Las etiquetas, los ejemplos y el rol **no sustituyen** la tarea, el contexto, las restricciones y los criterios. Una instrucción con etiquetas pero sin criterios sigue siendo ambigua.

## Probar y ajustar

Ninguna plantilla garantiza el resultado. Las guías coinciden en que hay que **iterar**: Gemini dice que el diseño de instrucciones (*prompts*) es iterativo; OpenAI, que es una disciplina empírica y que conviene construir evaluaciones y probar con frecuencia. Cómo hacerlo: cambia **una** cosa a la vez, compara con tus criterios de aceptación y conserva la versión que mejor funcione. Eso es lo que practicas en [[19 Práctica - Reescribir una instrucción|Práctica - Reescribir una instrucción]].

## Fuentes

- Claude, [buenas prácticas para escribir instrucciones (*prompting*)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices): 3–5 ejemplos relevantes, diversos y estructurados; etiquetas XML; rol en las instrucciones del sistema; documentos largos y consulta al final.
- Google, [estrategias para escribir instrucciones en Gemini (*prompting*)](https://ai.google.dev/gemini-api/docs/prompting-strategies): ejemplos *few-shot*, formato consistente, plantilla con instrucción de sistema y mensaje del usuario, iteración.
- OpenAI, [guía para escribir instrucciones en GPT-4.1 (*prompting*)](https://developers.openai.com/cookbook/examples/gpt4-1_prompting_guide): estructura sugerida, enfoque empírico.
- Brown et al., 2020, [*Language Models are Few-Shot Learners*](https://arxiv.org/abs/2005.14165): ejemplos en la instrucción sin ajuste fino ni actualizaciones de gradiente.
- Anthropic, [*Effective context engineering for AI agents*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents): ejemplos canónicos en lugar de listas de casos límite.

## Siguiente

Ponlo en práctica: [[19 Práctica - Reescribir una instrucción|Práctica - Reescribir una instrucción]].

← [[00 Módulo II - Índice]]
