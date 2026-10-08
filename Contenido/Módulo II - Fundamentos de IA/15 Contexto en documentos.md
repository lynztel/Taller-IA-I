---
tags:
  - taller-ia
  - modulo-2
  - contexto
  - documentos
modulo: 2
aliases:
  - Contexto en documentos organizados
  - AGENTS.md
  - CLAUDE.md
  - Archivos de instrucciones
---

> [!info] Qué resuelve esta nota
> Cada conversación nueva empieza «en blanco»: el modelo no recuerda lo que le dijiste ayer (ver [[03 Cómo se construye un modelo|Cómo se construye un modelo]] y [[09 Ventana de contexto|Ventana de contexto]]). Una solución práctica es **escribir una sola vez en un archivo** lo que el agente necesita saber y dejar que lo lea al empezar. Esta nota explica cómo funciona eso en las herramientas reales (`CLAUDE.md`, `AGENTS.md`), qué conviene escribir y cómo organizar una carpeta de trabajo propia.

## La idea: que el archivo haga de memoria

Un archivo de instrucciones es **texto que la herramienta carga en el contexto al empezar la sesión**. No cambia al modelo; solo coloca ese texto dentro de la ventana de contexto, junto con todo lo demás ([[08 Qué recibe el modelo|Qué recibe el modelo]]).

Claude Code lo documenta así: *cada sesión empieza con una ventana de contexto nueva* y hay dos mecanismos que llevan conocimiento de una sesión a otra: los archivos **CLAUDE.md** (instrucciones que tú escribes) y la **memoria automática** (notas que escribe el propio Claude a partir de tus correcciones y preferencias).

> [!example] Ejemplo
> Sin archivo, cada sesión empiezas con: «Escribe en español de México, usa un tono formal, cita siempre la fuente y no uses jerga…». Con archivo, esas líneas se escriben **una vez** y la herramienta las carga sola.

## Dos archivos que verás en programación

### AGENTS.md: «un README para agentes»

El sitio del formato lo define como «un README para agentes» (*a README for agents*): un lugar dedicado y predecible para dar contexto e instrucciones a los agentes de programación. Según el propio sitio:

- Es **Markdown común**: **no hay campos obligatorios** y los títulos son libres.
- Sirve para el detalle que **estorbaría en un README para personas**: cómo compilar, cómo ejecutar pruebas, convenciones de estilo.
- Se declara usado por **más de 60 mil proyectos de código abierto**.
- En repositorios grandes puede haber uno por subproyecto: los agentes leen **el archivo más cercano** en el árbol de carpetas, y **gana el más cercano al archivo que se edita**; lo que le pidas directamente en el chat tiene prioridad sobre todo.

### CLAUDE.md: lo equivalente en Claude Code

Según la documentación de Claude Code:

| Archivo | Ubicación | Para qué | ¿Quién lo ve? |
| :--- | :--- | :--- | :--- |
| Instrucciones de usuario | `~/.claude/CLAUDE.md` | Preferencias personales para **todos** tus proyectos | Solo tú |
| Instrucciones de proyecto | `./CLAUDE.md` o `./.claude/CLAUDE.md` | Instrucciones del proyecto compartidas con el equipo | El equipo, vía control de versiones |
| Instrucciones locales | `./CLAUDE.local.md` | Preferencias personales de ese proyecto (se agrega a `.gitignore`) | Solo tú, en ese proyecto |

Más detalles documentados:

- Se cargan **al inicio de cada sesión**. Los de las carpetas superiores a donde trabajas se cargan al lanzar; los de subcarpetas se cargan **cuando Claude lee o edita un archivo de esa subcarpeta**.
- Todos los archivos encontrados se **concatenan** en el contexto; no se sobrescriben entre sí.
- Pueden **importar otros archivos** con la sintaxis `@ruta/del/archivo` (hasta cuatro niveles de profundidad). Importar sirve para organizar, pero **no reduce el costo en contexto**, porque lo importado también se carga al inicio.
- El comando `/init` genera un CLAUDE.md inicial analizando el proyecto.
- Claude Code **puede leer `AGENTS.md`** como instrucciones del proyecto. Por defecto lo hace cuando no hay ningún `CLAUDE.md` en el directorio de trabajo ni por encima; si existen ambos, usa solo los CLAUDE.md, salvo que el CLAUDE.md importe al AGENTS.md o se cambie la configuración.

> [!warning] Es contexto, no una regla obligatoria
> La documentación de Claude Code es explícita: **Claude trata estos archivos como contexto, no como configuración que se hace cumplir.** Para bloquear una acción pase lo que pase, la propia documentación remite a mecanismos distintos (los ganchos, o *hooks*, de tipo PreToolUse). Dicho llanamente: escribir «nunca borres archivos» en el archivo **hace menos probable** que lo haga, pero **no lo garantiza**.

## Qué escribir y qué no

La regla de fondo viene de la ingeniería de contexto de Anthropic: buscar **el conjunto más pequeño posible de tokens de alta señal** que maximice la probabilidad del resultado que quieres. Se concreta así:

### 1. Instrucciones concretas y verificables

La documentación de Claude Code da estos contrastes:

| Vago | Concreto (verificable) |
| :--- | :--- |
| «Formatea bien el código» | «Usa sangría de 2 espacios» |
| «Prueba tus cambios» | «Ejecuta `npm test` antes de confirmar» |
| «Mantén los archivos ordenados» | «Los manejadores de la interfaz de programación (API) viven en `src/api/handlers/`» |

> [!example] Ejemplo, fuera de programación
> | Vago | Concreto |
> | :--- | :--- |
> | «Escribe formal» | «Usa tercera persona y evita contracciones o muletillas» |
> | «Cita bien» | «Después de cada dato, indica la fuente: autor, año y enlace» |
> | «Sé breve» | «Máximo 150 palabras por respuesta, salvo que pida más» |

La lógica es la de [[17 Anatomía de una instrucción|Anatomía de una instrucción]]: un criterio que puedes comprobar vale más que un adjetivo.

### 2. Cortos, organizados y sin contradicciones

Recomendaciones de la documentación de Claude Code:

- **Tamaño:** apuntar a **menos de 200 líneas** por archivo CLAUDE.md; los archivos más largos consumen más contexto y **reducen el seguimiento** de las instrucciones.
- **Estructura:** agrupar instrucciones bajo títulos y viñetas; Claude las sigue mejor que párrafos densos.
- **Consistencia:** si dos instrucciones se contradicen, **Claude puede elegir una arbitrariamente**. Conviene revisar los archivos de vez en cuando y quitar lo obsoleto o contradictorio.

### 3. Ni demasiado rígido ni demasiado vago

Anthropic describe dos fallas al escribir instrucciones de sistema: por un lado, meter **lógica compleja y frágil** escrita a mano; por el otro, dar **guía vaga y de alto nivel** que no ofrece señales concretas. Lo recomendable está en un punto medio. También recomienda **curar ejemplos diversos y canónicos** en lugar de llenar la instrucción con una lista de casos límite, algo que dicen explícitamente no recomendar.

> [!tip] Consejo
> Antes de añadir una línea al archivo, pregúntate: *¿esto cambiaría la respuesta?* Si el agente haría lo mismo sin esa línea, sobra. Un archivo de 20 líneas que se lee completo vale más que uno de 200 donde lo importante se pierde.

## Una carpeta de trabajo propia

Todo lo anterior vale también para quien no programa: la idea es **tener el contexto en archivos de texto**, que cualquier agente pueda leer. Esta es una estructura de ejemplo, no un estándar:

```text
Mi-proyecto/
├─ instrucciones.md   ← cómo quiero que trabaje el agente
├─ contexto.md        ← qué es el proyecto, para quién, estado actual
├─ fuentes/
│  └─ articulo.pdf    ← material que debe consultar
└─ notas/             ← apuntes, decisiones, pendientes
```

Una versión mínima de `instrucciones.md`:

```markdown
# Instrucciones

## Rol
Eres asistente de redacción profesional.

## Estilo
- Español de México, tercera persona.
- Máximo 150 palabras por respuesta, salvo que pida más.

## Fuentes
- Después de cada dato, indica la fuente: autor, año y enlace.
- Si no encuentras una fuente, dilo; no inventes referencias.

## Antes de entregar
- Revisa que cada cifra tenga fuente.
```

Y `contexto.md`:

```markdown
# Contexto
- Proyecto: informe de 8 páginas sobre trabajo híbrido.
- Entrega: 20 de noviembre. Lector: la dirección de la organización.
- Estado: ya tengo la introducción; falta el apartado de recomendaciones.
```

Ahí se separan dos tipos de contenido que cambian a ritmos distintos: **lo que casi no cambia** (instrucciones) y **lo que cambia con el avance** (contexto y notas). Mantener el segundo al día es parte del trabajo.

> [!tip] Consejo: datos sensibles
> Todo lo que está en el archivo termina dentro de la ventana de contexto y puede enviarse al servicio que uses. No guardes en estos archivos contraseñas, datos personales de terceros ni información que no compartirías con ese servicio.

## Notas que escribe el propio agente

Hay un segundo uso del documento: no solo tú le escribes al agente, también **el agente escribe para sí mismo**. Anthropic llama a esto *toma de notas estructurada*: el agente **escribe notas con regularidad en un almacenamiento fuera de la ventana de contexto** y las vuelve a leer cuando las necesita; como ejemplos menciona a Claude Code creando una lista de pendientes, o un agente propio que mantiene un archivo `NOTES.md`.

También es la base de la recuperación «justo a tiempo»: en lugar de cargar todo de antemano, el agente mantiene **referencias ligeras** (rutas de archivos, enlaces) y carga los datos solo cuando los necesita. Anthropic señala que la **jerarquía de carpetas, los nombres y las fechas** dan señales útiles: los tamaños sugieren complejidad, los nombres insinúan el propósito y las fechas pueden indicar relevancia. Por eso importa **nombrar bien los archivos**.

Estas notas se organizan mejor con un método: eso es lo que sigue en [[16 Segundo cerebro y PARA|Segundo cerebro y PARA]].

## Fuentes

- AGENTS.md, [sitio del formato](https://agents.md/): definición, adopción, sin campos obligatorios, archivo más cercano.
- Claude Code, [*How Claude remembers your project*](https://code.claude.com/docs/en/memory): CLAUDE.md, ubicaciones, carga, tamaño, consistencia, importaciones, lectura de AGENTS.md, «contexto, no configuración que se hace cumplir».
- Anthropic, [*Effective context engineering for AI agents*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents): conjunto mínimo de tokens de alta señal, altura adecuada de las instrucciones, ejemplos canónicos, toma de notas, jerarquías de carpetas.

## Siguiente

Cómo organizar esas notas para encontrarlas y reutilizarlas: [[16 Segundo cerebro y PARA|Segundo cerebro y PARA]].

← [[00 Módulo II - Índice]]
