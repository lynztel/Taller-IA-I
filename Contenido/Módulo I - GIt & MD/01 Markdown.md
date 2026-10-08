---
tags:
  - taller-ia
  - modulo-1
  - markdown
modulo: 1
aliases:
  - Sintaxis Markdown
---

> [!info] Qué es Markdown
> **Markdown** es un lenguaje de marcado ligero, creado en 2004 por John Gruber y Aaron Swartz, que da formato a texto plano con una sintaxis sencilla y convertible de forma directa a HTML u otros formatos estructurados.

## ¿Para qué sirve?

Permite redactar documentos con jerarquía y estilo visual sin editores visuales pesados (WYSIWYG). Se utiliza principalmente en:

- Documentación técnica y repositorios de código (archivos `README.md` en GitHub o GitLab).
- Aplicaciones de notas y gestión del conocimiento (Obsidian, Notion, Logseq).
- Blogs técnicos y generadores de sitios estáticos (Jekyll, Hugo, Astro).
- Mensajería y plataformas colaborativas (Slack, Discord, foros como Stack Overflow).

> [!important]+ Importancia en el uso de Inteligencia Artificial
> Markdown es el estándar de facto para estructurar datos e interactuar con modelos de lenguaje (LLMs) por cinco razones técnicas:
>
> - **Eficiencia de tokens y costo:** al carecer del cierre verboso de etiquetas propio de HTML o XML (`</div>`, `</p>`), minimiza la sobrecarga sintáctica. Menos caracteres de formato implican menor consumo de tokens, menor latencia y menor costo en la ventana de contexto.
> - **Alineación con los datos de preentrenamiento:** los modelos se entrenaron masivamente con código fuente, documentación técnica y repositorios (como GitHub). Por eso entienden y generan la jerarquía de Markdown (`#`, `-`, `|`, bloques de código) de forma nativa y con una tasa de error sintáctico casi nula.
> - **Estructuración de prompts y *system instructions*:** permite delimitar roles, instrucciones, restricciones y ejemplos *few-shot* con encabezados y listas. Esa segmentación semántica reduce ambigüedades y ayuda al modelo a priorizar directivas frente a los datos del usuario.
> - **Calidad de segmentación en RAG (*Retrieval-Augmented Generation*):** al convertir PDFs o páginas web a Markdown antes de incrustarlos en bases vectoriales se conserva la jerarquía (títulos, tablas, listas) sin la basura de scripts o estilos, y los documentos pueden dividirse en fragmentos (*chunks*) semánticamente coherentes.
> - **Renderizado y *streaming* en tiempo real:** los frontends pueden analizar el flujo de tokens conforme llega y transformarlo en interfaces ricas (bloques de código con resaltado, tablas o fórmulas) sin procesar archivos binarios pesados.

## ¿Por qué es útil?

- **Legibilidad en crudo:** un archivo Markdown se lee de inmediato en cualquier editor de texto plano, sin que las etiquetas estorben (a diferencia de HTML o LaTeX).
- **Velocidad de escritura:** estilos, enlaces y estructuras sin separar las manos del teclado ni usar menús flotantes.
- **Control de versiones amigable:** al ser texto sin formato binario, Git registra los cambios línea por línea de forma exacta y sin metadatos opacos. Ver [[02 Comandos básicos]].
- **Portabilidad y longevidad:** no depende de software propietario ni se vuelve obsoleto por incompatibilidad de versiones. Con motores de conversión como Pandoc, un `.md` se exporta a PDF, HTML, EPUB o DOCX.

## Sintaxis básica

### Encabezados

Se definen anteponiendo de uno a seis caracteres `#` según el nivel jerárquico:

```markdown
# Encabezado nivel 1 (equivalente a <h1>)
## Encabezado nivel 2 (equivalente a <h2>)
### Encabezado nivel 3 (equivalente a <h3>)
```

### Énfasis y estilo de texto

```markdown
*Texto en cursiva* o _cursiva_
**Texto en negrita** o __negrita__
***Negrita y cursiva combinadas***
~~Texto tachado~~
```

### Listas

```markdown
<!-- Lista desordenada -->
* Elemento 1
* Elemento 2
  * Subelemento anidado

<!-- Lista numerada -->
1. Primer paso
2. Segundo paso
3. Tercer paso

<!-- Lista de tareas -->
- [x] Tarea completada
- [ ] Tarea pendiente
```

### Enlaces e imágenes

```markdown
[Texto del enlace](https://ejemplo.com)
![Texto alternativo de la imagen](https://ejemplo.com/imagen.png)
```

### Bloques de código

Para código dentro de una línea se usan comillas invertidas simples. Para bloques completos se usan tres comillas invertidas, indicando opcionalmente el lenguaje para el resaltado de sintaxis:

````markdown
Usa la función `console.log()` para imprimir.

```python
def saludar(nombre):
    return f"Hola, {nombre}"
```
````

### Citas y líneas divisorias

```markdown
> Esto es una cita textual o bloque de referencia.

---
```

### Tablas

Se estructuran con barras verticales (`|`) y guiones (`-`):

```markdown
| Herramienta | Tipo      | Licencia    |
| :---------- | :-------: | ----------: |
| Obsidian    | Notas     | Propietaria |
| Pandoc      | Conversor | GPL         |
```

> [!tip] Alineación de columnas
> Los dos puntos `:` en la fila divisoria definen la alineación: `:---` izquierda, `:---:` centro, `---:` derecha.

## Siguiente

Con Markdown dominado, el siguiente paso es versionar tus notas: [[02 Comandos básicos]]. Para enlaces de apoyo (guía de sintaxis, Mermaid, TikZ y plantillas) consulta [[Git, GitHub y Markdown]].

← [[00 Módulo I - Índice]]
