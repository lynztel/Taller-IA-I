---
tags:
  - taller-ia
  - modulo-2
  - transformer
  - atencion
modulo: 2
aliases:
  - Transformer
  - Atención
  - Attention Is All You Need
---

> [!info] Qué resuelve esta nota
> La **atención** es el mecanismo con el que el modelo decide, para interpretar cada palabra, **a cuáles otras palabras del texto prestarles más peso**. El **Transformer** es el diseño de modelo que se apoya solo en ese mecanismo (Google, 2017). Es la base de la mayoría de los modelos de lenguaje actuales.

## El problema que resuelve

Para interpretar «estaba» en *«El gato no cruzó la calle porque estaba cansado»*, hay que saber quién estaba cansado. La respuesta («el gato») está varias palabras atrás. Un modelo necesita una forma de **relacionar cada palabra con las demás**.

Antes del Transformer, según sus autores, los modelos dominantes eran redes recurrentes o convolucionales. En los recurrentes, el cálculo se reparte siguiendo las posiciones del texto, una tras otra; esa naturaleza secuencial **impide paralelizar dentro de un mismo ejemplo de entrenamiento**, lo que pesa más con textos largos. El Transformer, que prescinde por completo de recurrencia y convoluciones, permite mucho más paralelismo y requirió bastante menos tiempo de entrenamiento en las pruebas de traducción del artículo.

## Cómo funciona la atención, en tres pasos

Vaswani et al. definen una función de atención como una correspondencia entre una **consulta** (*query*) y un conjunto de pares **clave-valor** (*key-value*): la salida es una **suma ponderada de los valores**, donde el peso de cada valor lo calcula una función de compatibilidad entre la consulta y su clave.

> [!example] Analogía (consulta, clave y valor)
> Cada palabra tiene tres «papeles»: lo que **busca** (consulta), la **etiqueta** que ofrece para que la encuentren (clave) y la **información** que aporta si la eligen (valor). En el artículo, las tres piezas se definen matemáticamente.

Aplicada a «estaba»:

1. **Comparar.** La consulta de «estaba» se compara con la clave de cada palabra anterior. Cuanto mejor coinciden, más alta la puntuación.
2. **Convertir en porcentajes.** Las puntuaciones se convierten en porcentajes que suman 100 %.
3. **Mezclar.** Se mezcla la información (los valores) de las palabras según esos porcentajes. «Estaba» queda entonces enriquecida con lo que el texto dice de «gato».

> [!example] Ejemplo (puntuaciones inventadas)
> Supón que las puntuaciones de «estaba» frente a las palabras anteriores son las de la tabla. Al convertirlas en porcentajes con la función exponencial normalizada (*softmax*, la que usa el artículo en su ecuación 1), resulta:
>
> | Palabra | El | gato | no | cruzó | la | calle | porque |
> | :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
> | Puntuación (inventada) | 0.2 | 3.0 | 0.1 | 1.0 | 0.1 | 1.8 | 0.5 |
> | Atención | 4 % | **59 %** | 3 % | 8 % | 3 % | 18 % | 5 % |
>
> Los porcentajes están redondeados y suman 100. «Gato» recibe el mayor, y «calle», el segundo, porque también es un sustantivo candidato. **Los números son un ejemplo para explicar la idea, no medidas de un modelo real.**

> [!abstract]- Para quien quiera la formulación (ecuación 1 del artículo)
> Si las consultas, claves y valores se agrupan en matrices $Q$, $K$ y $V$, la atención se calcula como:
>
> $$\text{Attention}(Q,K,V)=\text{softmax}\!\left(\frac{QK^{T}}{\sqrt{d_k}}\right)V$$
>
> donde $d_k$ es la dimensión de las claves. $QK^{T}$ compara cada consulta con todas las claves; dividir entre $\sqrt{d_k}$ y aplicar *softmax* produce los porcentajes; multiplicar por $V$ mezcla los valores.

## Piezas adicionales del Transformer

- **Autoatención** (*self-attention*). Cuando consultas, claves y valores vienen del mismo lugar —el texto mismo—, cada posición puede relacionarse con todas las demás.
- **Atención de varias cabezas** (*multi-head attention*). En vez de una sola atención, el modelo hace varias en paralelo y combina sus resultados. Según el artículo, esto permite atender conjuntamente a información de distintos «subespacios de representación» en distintas posiciones; con una sola cabeza, el promedio lo impide. El modelo base usa 8 cabezas de 64 dimensiones cada una (8 × 64 = 512, el tamaño de las incrustaciones).
- **Máscara.** En la parte que genera texto, se impide que cada posición atienda a las posteriores; por eso, en el ejemplo, las palabras que vienen después de «estaba» quedan en gris: «todavía no existen».
- **Codificación posicional.** Como no hay recurrencia, se suma a las incrustaciones información sobre la posición de cada fragmento (ver [[04 Tokens e incrustaciones|Tokens e incrustaciones]]).

## Dos cuidados al interpretar

> [!warning] Pesos no son porcentajes de atención
> Los **pesos del modelo** (incluidas las matrices que producen consultas, claves y valores) se aprenden al entrenar y son los mismos para cualquier texto. Los **porcentajes de atención** se calculan de nuevo en cada texto. Son cosas distintas (ver [[05 Pesos y parámetros|Pesos y parámetros]]).

> [!warning] Paralelo al leer, secuencial al escribir
> La paralelización del Transformer aplica al **procesar el texto de entrada** y al entrenar, cuando todo el texto ya se conoce. Al **generar** una respuesta, el modelo produce un fragmento a la vez porque el siguiente aún no existe (ver [[07 Predicción y azar|Predicción y azar]]).

## ¿Entiende el modelo la frase?

La atención muestra *qué información se combina*, no que el modelo «comprenda» como una persona. Lo documentado es el mecanismo de cálculo y sus resultados medibles.

## Fuentes

- Vaswani et al., 2017, [*Attention Is All You Need*](https://arxiv.org/abs/1706.03762): resumen e introducción; secciones 3.1 a 3.5; ecuación 1.

## Siguiente

Con la atención calculada, el modelo produce una lista de posibles continuaciones con su probabilidad. Ver [[07 Predicción y azar|Predicción y azar]].

← [[00 Módulo II - Índice]]
