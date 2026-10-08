---
tags:
  - taller-ia
  - modulo-2
  - practica
  - prompting
modulo: 2
aliases:
  - Ejercicio de reescritura
  - Práctica del módulo II
---
> [!info] Objetivo
> Comprobar con tu propia tarea y la herramienta de IA que uses que **una instrucción mejor escrita cambia el resultado**, y descubrir **qué parte** de la instrucción es la que lo cambia. Duración sugerida: unos 15 minutos. No es un experimento controlado: sus conclusiones valen para tu caso, no como regla general.
## Los cinco pasos

1. **Elige una tarea real** de tu carrera o de tu trabajo (no un ejemplo inventado: así podrás juzgar si el resultado sirve).
2. **Escríbela como la pedirías normalmente**, en una línea. Guárdala tal cual: es tu punto de partida.
3. **Reescríbela con la plantilla** de [[18 Plantilla y recursos para escribir instrucciones|Plantilla y recursos para escribir instrucciones]]. Si quieres, prueba también el otro orden de [[17 Anatomía de una instrucción|Anatomía de una instrucción]] y compara.
4. **Pégala en el modelo y revisa el resultado con tus criterios de aceptación.**
5. **Ajusta la parte que falló y vuelve a intentar.**

Lo importante no es llegar a una instrucción perfecta, sino **comparar el primer intento con el último** y anotar qué cambio hizo la diferencia.

## Hoja de trabajo

Copia esto en una nota nueva (puedes hacerlo con Obsidian) y complétala mientras trabajas.

```markdown
# Práctica: reescribir una instrucción

## Tarea elegida
[Una frase]

## Intento 1: como la pediría normalmente
[Pega la instrucción de una línea]

### Resultado
[Pega o resume la respuesta]

### ¿Qué le faltó?
[Contesta con las cuatro preguntas: ¿tarea clara? ¿información? ¿límites? ¿cómo sé que está bien?]

## Intento 2: con la plantilla
### Rol
### Contexto
### Tarea
### Restricciones
### Criterios de aceptación
(escribe cada sección)

### Resultado
[Pega o resume la respuesta]

### Revisión con mis criterios
| Criterio | ¿Cumple? (sí/no) | Evidencia |
| :--- | :-: | :--- |
|  |  |  |

## Intento 3 (si hizo falta)
### ¿Qué cambié?
[Una sola cosa por intento]

### Resultado

## Conclusión
- ¿Qué parte de la instrucción cambió más el resultado?
- ¿Qué criterio se incumplió con más frecuencia?
- ¿Qué haría igual en mi próxima instrucción?
```

## Ejemplo resuelto

Una tarea de oficina o de estudio, para que veas la forma del ejercicio. Los resultados descritos son **ilustrativos**: no se presentan como salida real de un modelo.

**Tarea elegida:** resumir un artículo para un informe.

**Intento 1:**

```text
Resume este artículo.
```

*Qué falta (con las cuatro preguntas):* para quién es, cuánto debe medir, qué enfoque seguir, cómo sabré si está bien. Un resultado típico de una instrucción así es un resumen genérico, de extensión arbitraria, que quizá no destaque lo que necesitas. Es lo que predice la lógica de [[08 Qué recibe el modelo|Qué recibe el modelo]]: con poca información, el modelo rellena.

**Intento 2 (con la plantilla):**

```markdown
## Rol
Eres asistente de investigación.

## Contexto
Adjunto un artículo sobre trabajo híbrido. Mi informe trata de ese tema
y lo leerá la dirección de la organización.

## Tarea
Resume el artículo para un compañero que no lo ha leído.

## Restricciones
- Un párrafo de 120 palabras.
- No agregues datos que no estén en el texto.
- Español de México.

## Criterios de aceptación
- Incluye el argumento principal, el método y una limitación.
- Si algo no aparece, escribe «no aparece en el texto».
```

**Revisión con los criterios:**

| Criterio | ¿Cumple? | Evidencia |
| :--- | :-: | :--- |
| Un párrafo de 120 palabras | Comprobar contando | Contar con el procesador de textos |
| Incluye argumento, método y limitación | Comprobar | Buscar cada uno en el resumen |
| Nada que no esté en el texto | Comprobar | Verificar cada dato contra el PDF |
| «No aparece en el texto» donde falte algo | Comprobar | Revisar si el artículo menciona limitaciones |

**Intento 3 (ajuste de una sola cosa):** supón que el resumen no menciona limitaciones y no indica que el artículo no las discute. Ajusta el criterio: «Si el artículo no menciona limitaciones, escribe "el artículo no menciona limitaciones" en lugar de deducirlas». Un solo cambio, una sola causa a comprobar.

## Cómo revisar el resultado

- **Verifica contra la fuente.** Si el modelo cita cifras, páginas o autores, compruébalos tú: ver [[10 Alucinaciones|Alucinaciones]]. Una respuesta fluida no es una respuesta verificada.
- **Cuenta lo que se pueda contar** (palabras, elementos, secciones). Para eso sirve un criterio comprobable.
- **Cambia una cosa por intento.** Si cambias cinco, no sabrás cuál funcionó.
- **Repite el mismo intento un par de veces.** La respuesta puede variar entre ejecuciones ([[07 Predicción y azar|Predicción y azar]]); una sola corrida no te dice si la mejora es estable.

> [!tip] Si el resultado empeora
> A veces la versión larga sale peor. Revisa si hay **instrucciones contradictorias** (por ejemplo «sé breve» y «incluye todos los detalles») o un exceso de restricciones; recuerda que, según la documentación de Claude Code para sus archivos de instrucciones, cuando dos instrucciones se contradicen el modelo puede elegir una arbitrariamente.

## Para compartir

Si hay tiempo, algunas personas voluntarias muestran su *antes* y *después*. Mientras escuchas, fíjate en qué elemento del *después* aporta más en cada caso: la tarea, la información, las restricciones o los criterios.

## Autoevaluación

1. ¿Cuál de los cuatro elementos faltaba en tu primer intento?
2. ¿Qué criterio de aceptación escribiste que *no* podrías comprobar con un sí o un no? Reescríbelo.
3. ¿Qué información le diste en el contexto que el modelo no podía saber por sí mismo?
4. Si cambiaras de modelo, ¿qué parte de tu instrucción revisarías primero según su guía?

## Fuentes

- Claude, [buenas prácticas para escribir instrucciones (*prompting*)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) y [definir criterios de éxito](https://platform.claude.com/docs/en/test-and-evaluate/define-success): base de los criterios comprobables y de revisar la instrucción con otra persona.
- Claude Code, [memoria y CLAUDE.md](https://code.claude.com/docs/en/memory): instrucciones contradictorias.

## Cierre del módulo

Con esta práctica termina el Módulo II. El resumen está en [[00 Módulo II - Índice]]; el siguiente módulo toma estas bases para trabajar con herramientas, generación aumentada por recuperación (RAG), habilidades (*skills*) y Protocolo de Contexto de Modelo (MCP).

← [[00 Módulo II - Índice]]
