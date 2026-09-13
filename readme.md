# Visualización efectiva de datos — Actividad 1

**Tema:** Fundamentos y clasificación de datos para el diseño de visualizaciones efectivas
**Dataset:** Resultados de la temporada 2025 de Fórmula 1 (24 Grandes Premios, 20 pilotos)
**Herramienta utilizada:** Python (pandas, matplotlib, seaborn, plotly) en Jupyter Notebook

---

## 1. Investigación

### ¿Qué es la visualización efectiva de datos y por qué es importante?

La visualización de datos es el proceso de representar información mediante elementos gráficos que facilitan su interpretación, permiten descubrir patrones, contrastar hipótesis y comunicar resultados con claridad. Su importancia radica en que transforma datos en argumentos: un gráfico no es neutral, sino que construye una narrativa que orienta la toma de decisiones, ya sea con fines exploratorios (analistas, iterativo, centrado en el dato) o explicativos (audiencias directivas, diseño depurado con un mensaje específico).

### ¿Qué diferencias existen entre las variables cualitativas y las cuantitativas?

Las variables cualitativas describen categorías: las **nominales** carecen de orden intrínseco (equipo, giro comercial), mientras que las **ordinales** sí lo poseen (nivel de satisfacción). Las variables cuantitativas miden magnitudes numéricas: las **discretas** provienen de conteos con valores enteros (número de quejas, puntos obtenidos), y las **continuas** se miden en una escala continua (monto de ventas, tiempo de vuelta). Identificar correctamente esta naturaleza es el primer paso para elegir el gráfico correcto, pues cada tipo responde a una pregunta analítica distinta.

### ¿Qué principios perceptivos y de codificación visual deben considerarse?

En el diseño gráfico deben aplicarse principios perceptivos como el **procesamiento preatentivo** (color, tamaño y posición se detectan antes que el texto) y las **leyes de Gestalt** —proximidad, similitud, continuidad y cierre—, que agrupan visualmente los elementos relacionados y reducen la carga cognitiva. En codificación visual, la **posición** y la **longitud** son los canales más precisos para representar magnitudes, seguidos del **color** (para destacar o segmentar) y la **forma** (para diferenciar grupos).

### ¿Qué errores comunes deben evitarse?

Los errores más comunes incluyen los **ejes truncados** (exageran diferencias mínimas), los **gráficos en 3D** (distorsionan proporciones), el ***chartjunk*** o exceso de elementos decorativos sin función informativa, las **paletas de color engañosas** que inducen juicios emocionales no justificados, y el uso de **dobles ejes** que sugieren correlaciones inexistentes. Una visualización profesional debe ser honesta, autointerpretativa y estar guiada por el objetivo analítico y no por criterios meramente estéticos.

*(Fuentes consultadas: Tema 1 — Fundamentos de la visualización efectiva de datos; Tema 2 — Clasificación de datos y estrategias de visualización efectiva; Kirk, A. (2024). Data Visualisation: A Handbook for Data-Driven Design (3ª ed.). Sage Publications; Knaflic, C. (2023). Storytelling con datos. Anaya Multimedia; Guo et al. (2023) sobre leyes de Gestalt aplicadas a la visualización.)*

**Palabras: 288**

---

## 2. Selección del conjunto de datos

**Dataset:** Resultados de carrera de la temporada 2025 de Fórmula 1, construido a nivel *piloto × Gran Premio* (474 registros) a partir de la clasificación oficial de las 24 carreras de la temporada.

**Fuente de los resultados reales de posición final:** F1-Fansite — *2025 F1 Standings* ([f1-fansite.com/f1-results/f1-standings-2025-championship](https://www.f1-fansite.com/f1-results/f1-standings-2025-championship/)), consultada el 13/09/2026. Los datos corresponden a la clasificación oficial de carrera principal (no incluyen los puntos de las 6 carreras *sprint* de la temporada, lo que explica que los totales calculados —por ejemplo, 394 pts de Norris— sean ligeramente menores a los totales oficiales de campeonato, 423 pts).

**Nota metodológica:** la variable continua `Tiempo_Vuelta_Rapida_seg` se estima a partir de referencias públicas de tiempos de vuelta característicos por circuito, ajustados según la posición final obtenida (proxy del ritmo relativo del auto/piloto ese fin de semana) más una variación aleatoria menor. Se declara explícitamente como variable **simulada** con fines didácticos, tal como permiten las instrucciones de la actividad ("podrá utilizarse un *dataset* público o simulado").

### Tabla descriptiva de variables

| Variable | Tipo | Descripción | Ejemplo de valores |
|---|---|---|---|
| `Gran_Premio` | Cualitativa **nominal** | Sede del Gran Premio dentro del calendario 2025 | Australia, Mónaco, Italia |
| `Equipo` | Cualitativa **nominal** | Escudería para la que compite el piloto | McLaren, Ferrari, Red Bull |
| `Categoria_Resultado` | Cualitativa **ordinal** | Nivel de desempeño en la carrera, con orden implícito | Podio &gt; Puntos &gt; Sin puntos &gt; No finalizó |
| `Puntos_Carrera` | Cuantitativa **discreta** | Puntos obtenidos en esa carrera según el sistema oficial de la F1 | 0, 1, 2, 4, 6, 8, 10, 12, 15, 18, 25 |
| `Tiempo_Vuelta_Rapida_seg` | Cuantitativa **continua** | Tiempo estimado de vuelta rápida, en segundos (simulada, ver metodología) | 71.592, 93.568, 105.8 |
| `Delta_Ritmo_seg` | Cuantitativa **continua** (derivada) | Diferencia del tiempo de vuelta respecto al tiempo base del circuito; usada para comparar equipos entre circuitos distintos | 0.06, 0.98, 1.72 |

### Muestra del dataset

| Gran_Premio | Ronda | Piloto | Equipo | Categoria_Resultado | Posicion_Final | Puntos_Carrera | Tiempo_Vuelta_Rapida_seg |
|:---|---:|:---|:---|:---|---:|---:|---:|
| Australia | 1 | Lando Norris | McLaren | Podio | 1 | 25 | 76.060 |
| China | 2 | Lando Norris | McLaren | Podio | 2 | 18 | 93.568 |
| Japón | 3 | Lando Norris | McLaren | Podio | 2 | 18 | 90.663 |

*(archivo completo: `f1_2025_resultados.csv`, 474 filas × 9 columnas)*

---

## 3. Diseño de visualizaciones

### Visualización 1 — Gráfica de barras: puntos totales por equipo

![Puntos totales por equipo](viz1_barras_puntos_equipo.png)

### Visualización 2 — Boxplot: distribución del ritmo relativo por equipo

![Boxplot de ritmo por equipo](viz2_boxplot_tiempos.png)

### Visualización 3 — Gráfica de líneas: evolución de puntos acumulados (Top 3 del campeonato)

![Evolución de puntos acumulados](viz3_lineas_puntos_acumulados.png)

*(El código completo que genera estas tres visualizaciones, con salidas ya ejecutadas, se encuentra en `Actividad1_F1_2025.ipynb`; incluye además una versión interactiva en Plotly de la Visualización 3.)*

---

## 4. Justificación y narrativa

### Justificación — Visualización 1 (Barras)

Esta visualización representa una variable cualitativa nominal (Equipo) frente a una variable cuantitativa discreta agregada (suma de puntos por carrera). Su propósito es comparar categorías: identificar qué escudería concentró más puntos en la temporada 2025. Se aplicó el canal de posición y longitud —los más precisos perceptualmente según Kirk (2024)— mediante barras horizontales, ordenadas de mayor a menor para aprovechar el principio de continuidad y facilitar la lectura jerárquica. El color se usó de forma preatentiva y minimalista: un solo tono de énfasis (naranja) resalta al equipo líder, mientras el resto permanece en gris neutro, evitando la sobrecarga cromática. El título es afirmativo y comunica directamente el hallazgo principal. Se descartó la gráfica de pastel porque con diez categorías dificultaría comparar magnitudes similares (Williams, Racing Bulls, Aston Martin), y una gráfica de líneas sería inadecuada al no existir una secuencia temporal entre equipos.

**Palabras: 143**

### Justificación — Visualización 2 (Boxplot)

Se combina una variable cualitativa nominal (Equipo) con una variable cuantitativa continua derivada (diferencia de tiempo de vuelta respecto al circuito). El propósito es explorar la distribución y variabilidad del ritmo de cada escudería en la temporada, e identificar consistencia u outliers. El boxplot resume mediana, cuartiles y valores atípicos sin adornos innecesarios, aplicando el canal de posición vertical, el más preciso para magnitudes. Los equipos se ordenaron por mediana (continuidad) para leer de inmediato la jerarquía competitiva. Fue clave normalizar el tiempo contra el promedio de cada circuito: comparar segundos absolutos entre pistas tan distintas como Austria (~64 s) y Bélgica (~105 s) habría distorsionado la lectura, un error de honestidad visual señalado en el Tema 1. Se prefirió el boxplot sobre un histograma porque permite comparar diez grupos a la vez en un solo eje, en lugar de diez histogramas separados y poco comparables.

**Palabras: 146**

### Justificación — Visualización 3 (Líneas)

Esta visualización cruza una variable cuantitativa discreta que actúa como eje temporal (ronda del campeonato, 1 a 24) con una variable cuantitativa continua acumulada (puntos acumulados), diferenciando por una variable cualitativa nominal (piloto) mediante color. Su propósito es analizar la tendencia y narrar la evolución de la disputa por el título entre los tres primeros lugares del campeonato. Se aplicó el principio de continuidad de Gestalt: la vista sigue naturalmente la trayectoria de cada línea, revelando de inmediato los cruces de posición. El color es consistente y limitado a tres tonos (similitud), y el título afirmativo resume el hallazgo central: Norris resistió la remontada de Verstappen. Se eligió la gráfica de líneas sobre una de barras porque representar 24 rondas por 3 pilotos en barras (72 elementos) resultaría ilegible; la línea comunica de forma inmediata la evolución continua y el momento exacto de los adelantamientos en la clasificación.

**Palabras: 148**

---

## Archivos entregados

| Archivo | Contenido |
|---|---|
| `Reporte_Actividad1.md` | Este reporte |
| `Actividad1_F1_2025.ipynb` | Notebook de Jupyter con el código completo y las salidas ya ejecutadas |
| `f1_2025_resultados.csv` | Dataset completo (474 filas × 9 columnas) |
| `viz1_barras_puntos_equipo.png` | Visualización 1 |
| `viz2_boxplot_tiempos.png` | Visualización 2 |
| `viz3_lineas_puntos_acumulados.png` | Visualización 3 |
