---
tags:
  - taller-ia
  - modulo-2
  - tokens
  - embeddings
modulo: 2
aliases:
  - Tokens y embeddings
  - Tokens
  - Fragmentos de texto
  - Embeddings
---

> [!info] Qué resuelve esta nota
> El modelo no lee letras ni palabras completas. Primero **parte el texto en fragmentos llamados tokens** y luego convierte cada fragmento en **una lista de números**, llamada incrustación (*embedding*). Entender esos dos pasos explica por qué el precio y los límites se miden en tokens, por qué un mismo texto cuesta distinto en distintos modelos y por qué conviene escribir los documentos de forma compacta (ver [[01 Markdown]]).

## Qué es un token

Según OpenAI, los tokens son las unidades que sus modelos usan para procesar texto. Un token puede ser un carácter, parte de una palabra, una palabra completa o un signo de puntuación. Dos reglas prácticas de OpenAI, **válidas para inglés**:

- 1 token equivale en promedio a unos 4 caracteres.
- 1 token equivale en promedio a tres cuartos de palabra; 100 tokens son unas 75 palabras.

OpenAI aclara que en otros idiomas la relación entre caracteres, palabras y tokens es distinta, y que el mismo texto puede dar recuentos distintos según el modelo, su codificación y el idioma. Para saber cuántos tokens usa un texto en español hay que **usar un contador**: el [Tokenizer de OpenAI](https://platform.openai.com/tokenizer) (herramienta web) o la biblioteca [tiktoken](https://github.com/openai/tiktoken) (programática).

> [!example] Analogía
> Es como armar con piezas de Lego: el modelo no ve el texto entero, ve piezas. Hay piezas grandes (palabras frecuentes) y piezas pequeñas (sílabas, signos) para armar lo demás.

## Ejemplos reales (calculados con tiktoken)

Los fragmentos siguientes se obtuvieron con la biblioteca `tiktoken` (versión 0.14.0) y la codificación `o200k_base`, que usan los modelos recientes de OpenAI. La marca `·` indica que el fragmento comienza con un espacio, porque **el espacio forma parte del fragmento**.

| Texto | Caracteres | Tokens | Fragmentos |
| :--- | :-: | :-: | :--- |
| Los modelos leen fragmentos de texto | 36 | 7 | `Los` `·modelos` `·leen` `·fragment` `os` `·de` `·texto` |
| The models read fragments of text | 33 | 6 | `The` `·models` `·read` `·fragments` `·of` `·text` |
| Explícame cómo funciona la IA | 29 | 7 | `Expl` `íc` `ame` `·cómo` `·funciona` `·la` `·IA` |
| Explain how AI works | 20 | 4 | `Explain` `·how` `·AI` `·works` |
| El gato no cruzó la calle porque estaba cansado | 47 | 11 | `El` `·gato` `·no` `·cruz` `ó` `·la` `·calle` `·porque` `·estaba` `·cans` `ado` |
| inconstitucionalmente | 21 | 4 | `in` `constit` `ucional` `mente` |
| 1234567 | 7 | 3 | `123` `456` `7` |
| 2026-10-08 | 10 | 6 | `202` `6` `-` `10` `-` `08` |

Lo que se observa en estos ejemplos (una muestra pequeña, no una regla):

- **Las palabras frecuentes suelen ser un solo fragmento; las largas o poco frecuentes se parten** en piezas (`inconstitucionalmente` en 4). Las partes acentuadas pueden quedar separadas (`Expl` `íc` `ame`).
- **Las mayúsculas y los espacios cuentan.** `red`, `Red` y `·red` son tres fragmentos distintos, con identificadores `1291`, `7805` y `3592`, respectivamente.
- **Los números se parten en bloques**, no en cifras individuales ni en el número completo.
- **En estas frases, el español usó igual o más fragmentos que el inglés.** Con tan pocos casos no se puede generalizar; por eso la regla de OpenAI se limita al inglés.

### Otro tokenizador, otro recuento

La misma frase da recuentos distintos según la codificación:

| Texto | `cl100k_base` | `o200k_base` |
| :--- | :-: | :-: |
| Los modelos leen fragmentos de texto | 8 | 7 |
| El gato no cruzó la calle porque estaba cansado | 12 | 11 |

También entre modelos de una misma empresa: la documentación de Claude Haiku 5.5 indica que usa el mismo tokenizador, más nuevo, que Claude 4.7 y posteriores, con el que **el mismo texto cuenta aproximadamente 30 % más tokens que en Claude Haiku 4.5**. Moraleja: las cifras de tokens sirven para comparar *dentro* de un mismo modelo, no para trasladarlas a otro.

### Markdown frente a HTML, en tokens

En la nota [[01 Markdown]] se explica que Markdown consume menos tokens que HTML por tener menos etiquetas. Medido con `o200k_base` sobre la misma lista de dos elementos:

| Formato | Texto | Caracteres | Tokens |
| :--- | :--- | :-: | :-: |
| Markdown | `# Título` + lista con `- uno` y `- dos` | 21 | 9 |
| HTML | `<h1>Título</h1><ul><li>uno</li><li>dos</li></ul>` | 48 | 24 |

> [!note] Alcance del ejemplo
> Es un solo ejemplo pequeño, calculado con una codificación. Muestra el efecto de las etiquetas de cierre, no una proporción general entre formatos.

### Cómo reproducirlo

```python
import tiktoken

enc = tiktoken.get_encoding("o200k_base")
texto = "Los modelos leen fragmentos de texto"
ids = enc.encode(texto)                                   # identificadores
trozos = [enc.decode_single_token_bytes(i) for i in ids]  # fragmentos (en bytes)
print(len(texto), "caracteres,", len(ids), "tokens")
print(trozos)
```

> [!tip] Una nota técnica
> A veces un fragmento corta un carácter acentuado a la mitad (en UTF-8 un carácter puede ocupar varios bytes). En esos casos `decode_single_token_bytes` devuelve bytes que no forman texto válido por sí solos; hay que unir fragmentos contiguos.

## Para qué sirve contar tokens

OpenAI documenta dos efectos prácticos:

1. **El precio.** En la API de OpenAI el precio por token depende del modelo. La interfaz de programación (API) es la vía por la que los programas usan los modelos. Consulta las páginas de precios en [[Laboratorio de tokens y modelos]].
2. **El límite.** La **ventana de contexto** se mide en tokens: limita cuánto puede procesar el modelo en una petición. Se explica en [[09 Ventana de contexto|Ventana de contexto]].

## Incrustaciones (*embeddings*): de fragmentos a números

Un identificador como `39564` no dice nada por sí solo del significado de `·modelos`. Por eso, cada fragmento se convierte en una **lista de números** llamada **incrustación** (*embedding*). En el Transformer original, la primera capa usa *incrustaciones aprendidas* (Vaswani et al., sección 3.4) que convierten cada fragmento en una lista de **512 números** en el modelo base y **1,024** en el modelo grande.

> [!example] Analogía
> Una incrustación es como las **coordenadas de un punto en un mapa**. Un mapa de ciudades tiene dos coordenadas (latitud y longitud); una incrustación real tiene cientos. Fragmentos con usos parecidos quedan cerca; los que no tienen relación, lejos.

Mikolov et al. (2013) propusieron arquitecturas para calcular representaciones vectoriales continuas de palabras y midieron su calidad con una **prueba de similitud entre palabras**, con un conjunto de prueba de similitudes sintácticas y semánticas. Eso respalda la idea de que con números se puede *calcular* qué tan parecidas son dos palabras.

### Ejemplo con números inventados

> [!example] Ejemplo (números inventados, en dos dimensiones)
> | Palabra | Coordenada 1 | Coordenada 2 |
> | :--- | :-: | :-: |
> | rey | 0.90 | 0.80 |
> | reina | 0.85 | 0.90 |
> | manzana | −0.70 | 0.10 |
>
> La distancia entre «rey» y «reina» es de unos 0.11; entre «rey» y «manzana», de unos 1.75. En un mapa con esas coordenadas, «rey» y «reina» quedan juntos y «manzana», lejos. Los modelos reales usan cientos de coordenadas aprendidas durante el entrenamiento, no números elegidos a mano.

### El orden también se codifica

Las incrustaciones por sí solas no dicen en qué posición está cada fragmento. Como el Transformer no tiene recurrencia ni convoluciones, Vaswani et al. (sección 3.5) **añaden «codificaciones posicionales»** a las incrustaciones para que el modelo pueda usar el orden de la secuencia. Sin ese paso, «el gato persiguió al ratón» y «el ratón persiguió al gato» tendrían los mismos fragmentos.

## Fuentes

- OpenAI, [qué son los tokens y cómo contarlos](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them) · [tiktoken](https://github.com/openai/tiktoken).
- Anthropic, [Claude Haiku 5.5](https://platform.claude.com/docs/en/models/haiku-5-5/overview): nota sobre el tokenizador.
- Vaswani et al., 2017, [*Attention Is All You Need*](https://arxiv.org/abs/1706.03762): secciones 3.4 (incrustaciones) y 3.5 (codificación posicional); Tabla 3 (512 y 1,024).
- Mikolov et al., 2013, [*Efficient Estimation of Word Representations in Vector Space*](https://arxiv.org/abs/1301.3781).
- Las tablas de fragmentos y el recuento Markdown/HTML se calcularon con `tiktoken` 0.14.0.

## Siguiente

Los números de cada incrustación no se escriben a mano: son parte de lo que el modelo aprende. Qué son esos números y cuántos hay se explica en [[05 Pesos y parámetros|Pesos y parámetros]].

← [[00 Módulo II - Índice]]
