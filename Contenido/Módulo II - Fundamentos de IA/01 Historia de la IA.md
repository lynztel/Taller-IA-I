---
tags:
  - taller-ia
  - modulo-2
  - historia
modulo: 2
aliases:
  - La IA no nació con ChatGPT
  - Hitos de la IA
---

> [!info] Qué resuelve esta nota
> La presentación recorre siete hitos y varios casos en pocas diapositivas. Aquí se explica qué ocurrió en cada uno, qué lo hizo importante y con qué cuidados conviene leer las cifras. La idea de fondo: **lo nuevo no es la IA, sino que los modelos de lenguaje la volvieron accesible para cualquier persona.**

## Línea de tiempo

| Año | Hito | Qué ocurrió |
| :-: | :--- | :--- |
| 1950 | Alan Turing | Publica «Computing Machinery and Intelligence» en la revista *Mind* (vol. LIX, núm. 236) y abre con la pregunta de si las máquinas pueden pensar. |
| 1955-1956 | Dartmouth | McCarthy, Minsky, Rochester y Shannon firman el 31 de agosto de 1955 una propuesta para estudiar la inteligencia artificial durante el verano de 1956. |
| 1997 | Deep Blue | Según IBM, venció al campeón mundial de ajedrez Garry Kasparov por 3.5 a 2.5. |
| 2012 | AlexNet | Krizhevsky, Sutskever y Hinton entrenan una red neuronal convolucional profunda con ImageNet y reportan errores considerablemente menores que el estado del arte. |
| 2016 | AlphaGo | Vence 5 a 0 al campeón europeo de Go (2015, publicado en *Nature*) y 4 a 1 a Lee Sedol (marzo de 2016). |
| 2020 | AlphaFold | Es el método mejor clasificado en CASP14, una competencia de predicción de estructuras de proteínas. |
| 2022 | ChatGPT | El 30 de noviembre, OpenAI lo presenta como vista previa de investigación gratuita. |

Fuentes: [Turing, *Mind* (1950)](https://academic.oup.com/mind/article/LIX/236/433/986238) · [Propuesta de Dartmouth (1955)](http://jmc.stanford.edu/articles/dartmouth/dartmouth.pdf) · [IBM, Deep Blue](https://www.ibm.com/history/deep-blue) · [AlexNet (2012)](https://proceedings.neurips.cc/paper_files/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) · [AlphaGo, *Nature* (2016)](https://research.google/pubs/mastering-the-game-of-go-with-deep-neural-networks-and-tree-search/) · [DeepMind, AlphaGo](https://deepmind.google/research/breakthroughs/alphago/) · [AlphaFold](https://alphafold.com/) · [OpenAI, ChatGPT](https://openai.com/index/chatgpt/).

## Dos hitos para entender qué cambió

### AlphaGo (2016)

**Qué es.** Un programa de Google DeepMind que juega Go, un juego de tablero. El artículo de *Nature* dice que vencer a un profesional con un programa se creía a una década de distancia.

**Cómo funciona.** Combina dos redes neuronales: una *red de política* que propone jugadas y una *red de valor* que evalúa posiciones. Antes de elegir, prueba muchas jugadas posibles con una búsqueda de tipo Monte Carlo. Se entrenó primero con partidas de expertos (aprendizaje supervisado) y luego jugando contra sí mismo (aprendizaje por refuerzo).

**Qué logró.** Según el artículo, ganó 99.8 % de las partidas contra otros programas de Go. Según DeepMind: en octubre de 2015 venció 5 a 0 a Fan Hui, tres veces campeón europeo; en marzo de 2016 ganó 4 a 1 a Lee Sedol en Seúl, un encuentro visto por más de 200 millones de personas. En la partida 2, su jugada 37 tenía, según DeepMind, una probabilidad de 1 en 10,000 de ser usada por una persona. El reporte de la Asociación Británica de Go confirma el marcador final.

Fuentes: [Silver et al., *Nature* (2016)](https://research.google/pubs/mastering-the-game-of-go-with-deep-neural-networks-and-tree-search/) · [DeepMind, AlphaGo](https://deepmind.google/research/breakthroughs/alphago/) · [British Go Association](https://britgo.org/node/5458).

### AlphaFold (2020) y el Nobel de Química 2024

**El problema.** Una proteína es una cadena de aminoácidos que se pliega en una forma tridimensional; esa forma determina qué hace. Predecir la forma a partir de la secuencia era un problema abierto desde hacía más de 50 años, según el Comité Nobel.

**Qué logró.** En CASP14 (2020) fue el método mejor clasificado por un amplio margen. Su base de datos reúne más de 200 millones de predicciones. El Comité Nobel indica que, hasta octubre de 2024, AlphaFold2 lo habían usado más de 2 millones de personas de 190 países.

**El premio.** El Nobel de Química 2024 fue para Demis Hassabis y John Jumper por la predicción de estructuras de proteínas y para David Baker por el diseño computacional de proteínas.

Fuentes: [AlphaFold](https://alphafold.com/) · [Comité Nobel, Química 2024](https://www.nobelprize.org/prizes/chemistry/2024/popular-information/).

## El Nobel de Física 2024

El premio fue para John Hopfield y Geoffrey Hinton «por descubrimientos e invenciones fundamentales que permiten el aprendizaje automático con redes neuronales artificiales». Según el comité, Hopfield creó una red que guarda y reconstruye patrones, y Hinton la usó como base de la **máquina de Boltzmann** (1985), que con herramientas de física estadística aprende a reconocer elementos característicos de un conjunto de datos. El comité sitúa esos descubrimientos de los años 80 como la base de la «revolución» del aprendizaje automático que empezó hacia 2010.

Fuente: [Comité Nobel, Física 2024](https://www.nobelprize.org/prizes/physics/2024/press-release/).

## Seis resultados que no son chats ni imágenes

| Ámbito | Qué se reportó | Cuidado al leerlo |
| :--- | :--- | :--- |
| **Materiales** | GNoME (DeepMind) predijo 2.2 millones de cristales; 380,000 son los candidatos más estables. Antes se conocían unos 48,000 materiales estables y GNoME llevó el total a 421,000. | Son *predicciones*: investigadores externos sintetizaron 736 de las estructuras. |
| **Matemáticas** | Problema 728 de Erdős: una IA de OpenAI (GPT-5.2 Pro) propuso la demostración y otra, Aristotle (Harmonic), la formalizó en Lean, un lenguaje en el que la computadora comprueba cada paso. | Terence Tao señala que los problemas de Erdős difieren en dificultad por varios órdenes de magnitud y que uno lleve 50 años abierto no implica que haya resistido todo esfuerzo humano; estima que solo 1 a 2 % de los problemas abiertos son lo bastante sencillos para este tipo de ayuda. |
| **Clima** | El Centro Europeo de Pronósticos Meteorológicos a Plazo Medio (ECMWF) puso en operación el 1 de julio de 2025 su pronóstico de ensamble con IA (51 pronósticos con variaciones). Mejora hasta 20 % en varias medidas y consume cerca de 1,000 veces menos energía. | Usa menor resolución (31 km frente a 9 km) y usa física para las condiciones iniciales. |
| **Energía** | Un sistema de redes neuronales entrenado con datos de sensores recomendó cómo operar el enfriamiento de centros de datos de Google (2016): hasta 40 % menos energía de enfriamiento y 15 % menos en el exceso total de energía del centro de datos (indicador PUE). | Validado en un centro de datos real; cifra reportada por la propia empresa. |
| **Fusión** | Degrave et al. (*Nature*, 2022): un controlador entrenado con aprendizaje por refuerzo en un simulador se transfirió, sin ajuste, al tokamak TCV del Swiss Plasma Center (EPFL) y controló formas de plasma variadas. | Es un reactor experimental, no una planta de energía. |
| **Medicina** | Ensayo aleatorizado MASAI (Suecia, 80,033 mujeres): con tamizaje apoyado por IA la carga de lectura de los radiólogos bajó 44.3 %. | La detección fue 6.1 frente a 5.1 por 1,000 (razón 1.2, p = 0.052): **no alcanzó significancia al 5 %**, así que no se puede afirmar superioridad, solo que la detección no bajó. |

> [!tip] Verificar es parte de la ciencia
> En el caso de Erdős, la prueba quedó en Lean: no depende de que alguien «confíe» en la IA, porque la computadora comprueba cada paso. Es un buen ejemplo de **resultado verificable**, la misma idea que se usa más adelante con los criterios de aceptación en [[17 Anatomía de una instrucción|Anatomía de una instrucción]].

Fuentes: [GNoME, DeepMind](https://deepmind.google/discover/blog/millions-of-new-materials-discovered-with-deep-learning/) y [Merchant et al., *Nature* (2023)](https://www.nature.com/articles/s41586-023-06735-9) · [Erdős 728, arXiv 2601.07421](https://arxiv.org/abs/2601.07421) · [Wiki de Tao sobre IA y problemas de Erdős](https://github.com/teorth/erdosproblems/wiki/AI-contributions-to-Erd%C5%91s-problems) · [OpenAI, GPT-5.2](https://openai.com/index/introducing-gpt-5-2/) · [ECMWF](https://www.ecmwf.int/en/about/media-centre/news/2025/ecmwfs-ensemble-ai-forecasts-become-operational) · [DeepMind, enfriamiento de centros de datos](https://deepmind.google/discover/blog/deepmind-ai-reduces-google-data-centre-cooling-bill-by-40/) · [Degrave et al., *Nature* (2022)](https://www.nature.com/articles/s41586-021-04301-9) · [MASAI, *Lancet Oncology* (2023)](https://lup.lub.lu.se/record/be033994-ed89-4a99-904a-f6e97b3d2b21).

## Dos hitos de 2026

**Matemáticas.** En su ensayo «Las matemáticas en la era de la IA» (*Mathematics in the age of AI*, arXiv 2608.16753, 17 de agosto de 2026), basado en su conferencia en el Congreso Internacional de Matemáticos 2026, Terence Tao parte de herramientas de IA capaces de hacer tareas matemáticas de nivel de investigación. Escribe que pasaremos «de una era de escasez de demostraciones a una era de abundancia». Añade que lo que está bajo prueba es el marco implícito de valores y prácticas de la comunidad, no el fundamento de la verdad matemática. Fuente: [Tao (2026)](https://arxiv.org/abs/2608.16753).

**Web.** Según el informe de Cloudflare del 1 de julio de 2026, este año el tráfico de agentes cruzó por primera vez un umbral histórico: más de 50 % del tráfico de Internet ya no es humano.

> [!warning] Cómo leer esa cifra
> El informe no da un porcentaje más preciso ni un mes, no define «agente» ni «bot» y no indica con qué métrica obtuvo la cifra; sus datos vienen de Cloudflare Radar. Por eso no es comparable con otras mediciones: Radar mostraba el 7 de octubre de 2026 (últimos 7 días, a nivel mundial) 60.6 % de solicitudes HTTP humanas y 39.4 % de bots, que es **otra métrica**. Este es un buen ejemplo de la lectura crítica que se practica en [[13 Pruebas de referencia|Pruebas de referencia]].

Fuentes: [Cloudflare, informe de bots](https://blog.cloudflare.com/agentic-internet-bot-report/) · [Cloudflare Radar](https://radar.cloudflare.com/bots).

## Caso: Jim Simons y el aprendizaje automático en los mercados

Jim Simons, matemático, presidió el departamento de Matemáticas de la Universidad de Stony Brook y, según la Fundación Simons, fundó en 1978 lo que sería Renaissance Technologies, pionera de la operación bursátil cuantitativa (*trading* cuantitativo). En una entrevista en video explica su enfoque:

- La teoría del mercado eficiente sostiene que los precios pasados no dicen nada del futuro porque el precio siempre es correcto; Simons dice que «eso simplemente no es cierto».
- Existen **anomalías sutiles** incluso en el historial de precios; ninguna basta para enriquecerse por sí sola, pero juntando muchas se puede predecir bastante bien.
- El método: se adivina qué podría ser predictivo, se prueba en computadora con datos históricos de largo plazo, se añade al sistema si funciona y se descarta si no. Simons lo describe como «aprendizaje automático».
- El equipo: unos 100 doctores en física, astronomía, matemáticas y estadística, sin experiencia en finanzas pero con buena ciencia previa.

> [!note] Precisión histórica
> Los modelos de lenguaje actuales no existían entonces. Lo que Simons describe son **modelos estadísticos que aprenden de datos históricos**: aprendizaje automático, pero no un chat.

### El fondo Medallion frente a Buffett y al S&P 500 (1988-2018)

| | Medallion (neto de comisiones) | Berkshire Hathaway | S&P 500 |
| :--- | :-: | :-: | :-: |
| Promedio anual | 39.1 % | 18.8 % | 11.6 % |
| Mejor año | 98.5 % (2000) | 84.6 % (1989) | 37.6 % (1995) |
| Peor año | −4.0 % (1989) | −31.8 % (2008) | −37.0 % (2008) |
| Años con pérdida (de 31) | 1 | 6 | 6 |

Los promedios son **promedios simples** de los rendimientos anuales. Con rendimientos compuestos las cifras son 37.7 %, 16.1 % y 10.2 %, respectivamente.

> [!warning] Salvedades que acompañan a estas cifras
> - Renaissance no publica los datos de Medallion y no están auditados: vienen del libro de Zuckerman, que cita informes anuales e informes a inversionistas, y el análisis de Bradford Cornell (UCLA) los reproduce con diferencias menores (por ejemplo, 1989: −3.2 % en su cálculo).
> - Las tres series no son del todo comparables (comisiones e impuestos distintos). Medallion está cerrado a inversionistas externos y pasó de manejar 20 millones de dólares (1988) a 10 mil millones (2018): a mayor tamaño, menos margen.
> - Los rendimientos pasados no garantizan los futuros. Esto es información, no una recomendación de inversión.

Fuentes: entrevista a [Jim Simons (video)](https://youtu.be/c2QZXCizcSk) · [Fundación Simons (2024)](https://www.simonsfoundation.org/2024/05/10/simons-foundation-co-founder-mathematician-and-investor-jim-simons-dies-at-86) · Zuckerman, *The Man Who Solved the Market* (2019), Apéndice 1 · Cornell, *Journal of Portfolio Management* (marzo de 2020, DOI 10.3905/jpm.2020.1.128) · Berkshire Hathaway, carta anual de 2018.

## Caso: de un fondo cuantitativo a DeepSeek

- **High-Flyer** es un fondo chino que se describe en su sitio como un fondo «impulsado por IA» (*AI Driven Hedge Fund*).
- El **14 de abril de 2023**, según el medio chino Yicai, High-Flyer anunció que concentraría recursos en una organización de investigación independiente para explorar la inteligencia artificial general (**AGI**: una IA capaz de muchas tareas, no solo de una). Un representante la describió como «investigación de modelos grandes completamente independiente, sin relación con las finanzas» y su director escribió que «la AGI no sirve para operar en bolsa; tiene usos y valor mucho mayores».
- En una entrevista publicada en 36Kr en mayo de 2023, el fundador **Liang Wenfeng** explica que la compra de tarjetas gráficas obedeció sobre todo a la curiosidad por la IA y que su incursión en los modelos de lenguaje no está directamente relacionada con las finanzas cuantitativas. En 2024, DeepSeek estaba financiada por completo por High-Flyer.

Fuentes: [High-Flyer](https://www.high-flyer.cn/en/) · [Yicai (14 de abril de 2023)](https://www.yicai.com/news/101732215.html) · [Liang Wenfeng, 36Kr 2023 (Recode China AI)](https://www.recodechinaai.com/p/the-deep-roots-of-deepseek-how-it) · [Liang Wenfeng, 2024 (ChinaTalk)](https://www.chinatalk.media/p/deepseek-ceo-interview-with-chinas).

## Qué conviene llevarse

1. **IA ≠ chat.** La mayoría de los resultados de esta nota son modelos hechos para una tarea concreta (jugar Go, predecir proteínas, pronosticar clima). Los modelos de lenguaje son una parte, la más visible, del campo. Más sobre esa distinción en [[11 Tipos de modelo|Tipos de modelo]].
2. **Un resultado se lee con su método de verificación.** Una prueba formal en Lean, un ensayo aleatorizado o un artículo en *Nature* pesan distinto que un anuncio de una empresa.
3. **Las cifras siempre vienen con salvedades.** Casi todos los casos anteriores traen una: significancia estadística, tamaño del fondo, definición de «bot». Aprender a buscarlas es el núcleo de [[13 Pruebas de referencia|Pruebas de referencia]].

> [!question] Para pensar
> ¿En tu carrera o trabajo hay una tarea parecida a las de la tabla (predecir, clasificar, optimizar) que ya se haga con IA especializada y no con un chat? ¿Qué evidencia pedirías para confiar en ella?

## Siguiente

Con el recorrido histórico hecho, define los términos con los que se habla de IA hoy en [[02 Modelo, aplicación y agente|Modelo, aplicación y agente]].

← [[00 Módulo II - Índice]]
