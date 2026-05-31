---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.19.1
kernelspec:
  display_name: estadistica
  language: python
  name: python3
---

# Probabilidad

Recordemos el caso de análisis de los hogares del capítulo anterior, estos pueden conformarse por 1 hasta 34 miembros.

Como ejercicio intelectual, supongamos que usted hubiese podido observara la conformación de todos los hogares. Imagínese un observador omniprescente que puede viajar al pasado y presenciar la evolución de la formación de los hogares. Usted, sin embargo, no tiene el poder de saber el resultado, solo puede presenciar y tomar apuntes. También suponga que el viaje le borra la memoria y usted no sabe cuántos hogares de un tamaño determinado existirán en el 2022 de Ecuador. Entonces, antes que se constituyan los hogares, usted hará un experimento.

## Experimento

En el contexto de la probabilidad, un **experimento** es un proceso, situación o acción cuyo resultado no conocemos con certeza antes de realizarlo. 

Usted debería esperar, como ese observador, a que se conformen los hogares y luego censar a los pobladores para conocer la distribución del tamaño de los hogares.

Como dijimos en el capítulo anterior, la probabilidad es la frecuencia relativa. Profundicemos esa idea.

Los experimentos serían, en diversos contextos, el proceso que genera los resulatdos. En nuestro ejercicio, nosotros no emparejamos a las perosnas. Esperamos y observamos. El proceso es la demografía. También podemos pensar en el experimento como la situación: la conformación de hogares. En otras situaciones, el proceso será lanzar una moneda --la acción--.

El experimento es el proceso generador de resultados. Por lo tanto, si queremos contar los puntos de las caras de dos dados, hacemos un experimentos al lanzamos al aire. Si empezamos a mirar con atención el precio de un activo en el mercado de valores, también estamos haciendo un experimento. Existen varias situaciones de interés en las que hacemos experimentos, ya sean mentales, como en nuestro ejemplo del observador omniprescente sin memoria que viaja al pasado para observar la constitución del tamaño de los hogares, o físicos: como al medir la temperatura. Eso sí, **cuando no podemos saber con certeza el resultado**.

Note que al lanzar una moneda podemos obtener dos caras. Si lanzamos al aire dos dados, 2 caras con puntos entre 1 y 6 cada una. Si miramos el precio de un activo, un rango de precios, expresados en números reales. Los resultados, todos, contados, se conocen como espacio muestral.

## Espacio muestral

Todos los resultados de un experimento son el espacio muestral. Note que "todos los resultados" pueden representarse en un conjunto de todas las opciones producidas por el experimento. En la Teoría de la Probabilidad (TP), una rama de las matemáticas que estudia la probabilidad, se utilizan los conjuntos como elementos clave. Estos nos permiten ponerle un número a los procesos estocásticos.

## Procesos estocásticos

Un sistema **estocástico** es aquel comportamiento **no determinista**. En ellos no podemos asegurar, predecir o adivinar con certeza un resultado.

Cuando no podemos asegurar con certeza, pensamos en posibilidades. Como señaló {cite}`grimmett_probability_2020`: 
>Muchas afirmaciones cotidianas tienen la forma: “la posibilidad —o probabilidad— de que ocurra A es p”, donde A es algún evento, como “que mañana brille el sol” o “que Cambridge gane la regata Boat Race”, y p es un número o adjetivo que describe una cantidad, como “un octavo”, “baja”, etc.

No está demás precisar que Teoría es, en ciencia, explicación exhaustiva y comprobable de algún aspecto del universo. Así que la TP es una descripción rigurosa de lso fenómenos aleatorios.

## Evento

Un evento es un subconjunto del espacio muestral. Es decir, es un puñado de todos resultados posibles que ocurren en el experimento. Por ejemplo, al lanzar dos dados la suma puede ser de 2 a 12. Dibujemos el espacio muestral lanzar dos dados en una tabla: en las filas listemos los puntos de un dado, y en las columnas del otro.

| + | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| **1** | 2 | 3 | 4 | 5 | 6 | 7 |
| **2** | 3 | 4 | 5 | 6 | 7 | 8 |
| **3** | 4 | 5 | 6 | 7 | 8 | 9 |
| **4** | 5 | 6 | 7 | 8 | 9 | 10 |
| **5** | 6 | 7 | 8 | 9 | 10 | 11 |
| **6** | 7 | 8 | 9 | 10 | 11 | 12 |

Un evento A, digamos, puede ser: que la suma de las caras sea par: {2, 4, 6, 8, 10, 12} (6 posibles resultados), o que la suma sea impar {1, 3, 5, 7, 9, 11} (también 6 posibles resultados). Hay varios eventos que son subconjuntos del espacio muestral.

Al lanzar los dados tendremos solo un resultado, digamos: 3 en un dado, y 5 en el otro. La suma sería 3 + 5 = 8. El resultado del experimento es 8, entonces. El evento "suma par" ocurrió. Existían 6 resulatos posibles, así que cualquier resultado que esté en A implica que A ocurra (se dé, tenga lugar, suceda).

## Conjuntos y definiciones formales

Empecemos a expresar estos conceptos de forma económica, es decir, sin tener que repetir largas oraciones:

> **Espacio muestral**: conjunto, S, de todos los resultados posibles generados con el experimento. <br>
> **Evento**: $A \subseteq S$. Note que escribimos $\subseteq$ ya que A puede ser B.

Construímos definiciones justamente, entre otros propósitos, para no repetir un párrado completo cada vez que tengamos que trabajar sobre uns situación en la que tengamos que estimar la posibilidad de un ocurrencia de un evento. Es fácil emplear símbolos para comunicarnos con otros, además, sin los problemas del idioma, la mala comunicación de ambos, o otras minucias.

Partiendo de estas definiciones, queremos cuantificar la posibilidad de ocurrencia de un evento. Ponerle un número, que de cuenta de la magintud de esa posibilidad.  En el [capítulo 2](cap2.md#la-frecuencia-como-probabilidad) dijimos que la probabilidad era la frecuencia relativa, y dividimos la cantidad de hogares de un tamaño para la cantidad total de hogares del país. Los eventos podían haberse definido como: "el hogar sea de 1 miembro", "el hogar sea de 2 miembros", etc. Siendo más breves: "el hogar sea de *i* miembros"; de esta manera, i puede ser algún valor del conjunto {1, 2, 3, ..., 34}.

También podíamos escribir, deseando ser ocupar menos espacio:

$A_i := \text{el hogar sea de } i \text{ miembros}, \forall i \in \{1, 2, 3, ..., 34\}$
o

$A_i := \text{el hogar sea de } i \text{ miembros}, \forall i = 1, 2, 3, ..., 34$.

Escribir $A_i$ nos permite definir un evento para cada cantidad de miembros, e identificar el evento.

Quiero que se de cuenta de que el uso de símbolos matemáticos nos permite ser precisos y breves.

Continuemos.

Al medir la probabilidad, estamos calculando la frecuencia relativa. Siendo específicos, dado un evento $E$ contamos todos los resultados potenciales que conforman el conjunto del evento (hogar de $i$ miembros en nuestro análisis de los hoagres) y lo dividimos para la cantidad de eventos posibles del espacio muestral (total de hogares de Ecuador). 

Ese conteo se puede expresar matemáticamente (con símbolos, precisión y brevedad) con $n$. Así, con un conjunto $C$, $n(C)$ es la cantdiad de elementos del conjunto $C$.

Sean $E$ el evento de interés y $S$ el espacio muestral de nuestro experimento, $\frac{n(E)}{n(S)}$ es la probabilidad del evento $E$. Usaremos $P$ para referirnos a probabilidad, y $P(E)$ para aludir a la probabilidad de $E$. Así:

$$
P(E) = \frac{n(E)}{n(S)}
$$

(Me reservo el derecho de ser redundante o poco ahorrativo de palabras en aras de que usted, estudiante, entienda sin duda razonable cada definición y objeto matemático).

También es importante notar que $n(\cdot)$ y $P(\cdot)$ son funciones (si usted no recuerda que es una función, revíselo brevemente con su agente favorito de IA).

En el siguiente capítulo exploraremos las propiedades que debe tener una función de probabilidad. Esto nos permitirá ser claros cuando hablemos de estimar probabilidades, incluyendo las limitaciones de nuestras estimaciones. Por ahora, solo vamos a pensar en aritmética (divisiones) y conceptos.

Hagamos un par de estimaciones. Usemos nuestros datos censales para calcular la probabilidad del evento $M := \text{ser mujer}$.

Estimemos la probabilidad con Python.

```{code-cell} ipython3
:tags: [hide-input]
import pandas as pd
import pyarrow

url = "https://github.com/Michaeljo112/estadisticalibro/releases/download/popec22/popec22.parquet"

df = pd.read_parquet(url, engine='pyarrow')
```

```{code-cell}
# 1: Hombre
# 2: Mujer

df.groupby("P02").size().reset_index(name="n")
```
Como puede ver, existen 8.686.463 mujeres; entonces, $n(M) = 8.686.463$. Además, definamos $H := \text{ser hombre}$ y $S := \text{ser ecuatoriana/o}$. Por lo tanto, $n(S) = 16.938.986 = n(M) + n(H) = 8.686.463 + 8.252.523$. De modo que 

$$
P(M) = \frac{n(M)}{n(S)} = \frac{8.252.523}{16.938.986} \approx 0.487191 \approx 49.72\%
$$ 

# Dependencia

Ahora consideremos la distribución por edad de hombres y mujeres.

```{code-cell}
df["sexo"] = df["P02"].map({
    1: "Hombre",
    2: "Mujer"
})

tabla = pd.crosstab(df["P03"], df["sexo"], margins=True)
tabla
```

En la tabla de arriba podemos ver cuántas mujeres y hombres de determinada edad hay. Como puedes ver, tenemos personas que alcanzan hasta los 120 años; cosa que es muy extraña, pero así constan los registros. Para poder resumir estos datos, usemos rangos de edad de 10 años.

```{code-cell} ipython3
bins   = range(0, 121, 10)
labels = [f'{i}-{i+9}' for i in range(0, 120, 10)]

df['rango_edad'] = pd.cut(df['P03'], bins=bins, labels=labels, right=False)

tabla_rangos = pd.crosstab(df['rango_edad'], df['sexo'], margins=True)
tabla_rangos
```

Si sumamos las filas, tenemos cuántas personas tienen edades según el rango de edad. Si sumamos las columnas, cuántas personas por sexo hay. Ahora, pensemos en los eventos que podemos conformar con los rangos de edad. Definamos eventos $Y_j := \text{que la persona tenga una edad en el rango de edad } j$, y asignemos cada rango de edad de menor a mayor a los números 1, 2, 3, etc.

```{code-cell} ipython3
cod_rango = {label: j+1 for j, label in enumerate(labels)}
df['cod_rango'] = df['rango_edad'].map(cod_rango)
df[['P03', 'rango_edad', 'cod_rango']].drop_duplicates().sort_values('cod_rango').head(12)
```

Además, podemos definir los eventos "ser mujer y tener 15 años" (ser mujer y tener una edad en el rango 2) o "ser hombre y tener 20 años" (ser hombre y tener una edad en el rango 3). Pensemos en ellos de forma gráfica.

```{code-cell} ipython3
:tags: [hide-input]

import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import numpy as np

fig, ax = plt.subplots(figsize=(9, 8))
ax.axis('off')

col_w = 3.0
row_h = 0.45
gap_col = 1.0
x_h = 1.5
x_m = x_h + col_w + gap_col
y0 = 0.5
total_h = 12 * row_h

palette = plt.cm.tab20(np.linspace(0, 1, 12))

for j in range(12):
    y = y0 + j * row_h
    color = palette[j]
    ax.add_patch(mpatches.Rectangle((x_h, y), 2 * col_w + gap_col, row_h,
                                     color=color, alpha=0.45, zorder=1))
    ax.text(x_h - 0.15, y + row_h / 2, f'$Y_{{{j+1}}}$', ha='right', va='center', fontsize=9)

ax.add_patch(mpatches.Rectangle((x_h, y0), col_w, total_h, fill=False, ec='#013440', lw=2.5, zorder=3))
ax.add_patch(mpatches.Rectangle((x_m, y0), col_w, total_h, fill=False, ec='#593954', lw=2.5, zorder=3))

ax.text(x_h + col_w / 2, y0 + total_h + 0.25, 'Hombres ($H$)', ha='center', fontsize=13, fontweight='bold', color='#013440')
ax.text(x_m + col_w / 2, y0 + total_h + 0.25, 'Mujeres ($M$)', ha='center', fontsize=13, fontweight='bold', color='#593954')

ax.set_xlim(0, x_m + col_w + 1)
ax.set_ylim(0, y0 + total_h + 1)
ax.set_title('Cada rango $Y_j$ atraviesa $H$ y $M$', fontsize=13, pad=10)
plt.tight_layout()
plt.show()
```

El evento "ser mujer y tener 15 años", llamémosle $Z$, es la intersección de los eventos $M$ (ser mujer) y $Y_2$ (tener 15 años o estar en el rango de edad 2). Es decir: $Z = M \cap Y_2$. Por pura conveniencia, podemos usar $Z_i := \text{ser mujer y tener una edad en el rango de edad } i$. Así, $Z_2 := \text{ser mujer y tener una edad en el rango de edad 2}$.

Entonces, la probabilidad de "ser mujer y tener 15 años" o "ser mujer y tener una edad en el rango de edad 2" es:

$$
P(Z_2) = n(Z_2)/n(S) = n(M \cap Y_2)/n(S)
$$

Notemos que otra forma de escribir $P(Z_2) = P(\text{ser mujer } \textbf{y} \text{ tener una edad en el rango 2}) = P(M \textbf{ y } Y_2) = P(M, Y_2)$. Es habitual usar coma como "y". Usaremos esta forma reducida: $P(M, Y_2)$, en adelante, para hablar de eventos conjuntos: que están intersectados, literalmente o "que ocurren juntos", como han memorizado algunos estudiantes. Mi recomendación --de las pocas que me atrevo a hacer, pues considero dar consejos una mala costumbre-- es que no memorice y entendienda.

## Disjunciones

Se le ha denominado dependencia al hecho de que un evento y otro sean conjuntos. Cuando no se intersectan se los considera eventos independientes. Yo preferiría decirles eventos conjuntos o disjuntos, pero bueno.

Si yo quisiera estimar la probabilidad de que ser mujer y hombre tendría que estimar:

$$
P(H, M) = P(H \cap M) = P(\emptyset)
$$

Si yo quisiera estimar la probabilidad de que ser mujer y hombre tendría que estimar:

## $ \emptyset $

$\emptyset$ no tiene ningún elemento 
($n( \emptyset ) $ = 0). Le parecerá intuitivo que la probabilidad de algo que no tiene elementos sea 0. Esa intuición puede ser una restricción que inponemos. Efectivamente, los matemáticos inponen restricciones a sus cuerpos teóricos. Restrinjamos, entonces, que $P(\emptyset) = 0$.

## $ S $

Por otra parte, pensemos en $P(S)$ (recuerda que S es todo el espacio muestral). Como $S$ son todos los resulatdos posibles, digamos que fueran $N$ resulatdos, $P(S) = n(S)/n(S) = N/N = 1$. La intuición sugeriría que considerar todos los elementos implica que siempre suceden todos los resultados posibles. Sí, es una intuición útil. La refinaremos en los próximos capítulos.

## Ocurrencias temporales

Hemos analizado casos estáticos. Un punto del tiempo, datos de 2022. Pero qué ocurre cuando consideramos casos dinámicos: sucesos en que ocurren en el tiempo.

Consideremos el lanzamiento de una moneda. Si lanzo una moneda una vez, el espacio muestral es cara (C) y sello (S): $S = \{C, S\}$. Si vuelvo a lanzar la cara tendré otro espacio muestral $\{C, S\}$ en el siguiente intento. Cada intento podría anclarse a un punto del tiempo $t$. 

Hagamos un esquema de dos lanzamientos, como un árbol de bifurcación. En cada punto del tiempo el experimento vuelve a abrir dos caminos posibles:

```{image} imagenes/arbol_lanzamientos_moneda.svg
:alt: Árbol de bifurcación de dos lanzamientos de una moneda
:width: 85%
:align: center
```

El espacio muestral de dos lanzamientos es, entonces:

$$
S_2 = \{(C, C), (C, S), (S, C), (S, S)\}
$$

Cada rama completa del árbol representa una ocurrencia temporal: primero observamos el resultado en $t_1$ y luego el resultado en $t_2$.



# Filtros, condicionalidad

Por otra parte, podríamos calcular las probabilidades de que alguien en Ecuador sea mujer y tenga 15 años, o que sea hombre y tenga 17 años. O cualquier combinación. Ahora, sin embargo, pensemos en la composición de mujeres por edad. Dividiremos la cantidad de mujeres de cada edad para el total de mujeres.

```{code-cell}
n_mujeres = tabla_rangos.loc[tabla_rangos.index != "All", "Mujer"]

pd.DataFrame({
    "n": n_mujeres,
    "porcentaje": n_mujeres / tabla_rangos.loc["All", "Mujer"] * 100
})
```

Si el evento es $A_k := \text{ser una mujer de edad dentro del rango } k$, en la tabla anterior calculamos $n(A_k)/n(M)$. Ahora, consideremos esa división y reescribamosla:

$$
\frac{n(A_k)}{n(M)} = \frac{n(A_k)}{n(M)} \cdot 1 =
\frac{n(A_k)}{n(M)} \cdot \frac{\frac{1}{n(E)}}{\frac{1}{n(E)}} =
\frac{\frac{n(A_k)}{n(E)}}{\frac{n(M)}{n(E)}} =
\frac{P(A_k)}{P(M)}
$$

Recordemos que 

# Una idea vaga de la Ley de grandes números

Empíricamente hemos observado que aumentar la cantidad de observaciones en la muestra aleatoria mejora la estimación. La ley de los grandes número resume esta idea: aumentar el tamaño de la muestra hace que los valores de estimadores sean más cercanos a los valores de los parámetros.

Más adelante vovleremos a esta ley y la delimitaremos matemáticamente para que sea precisa, tenga un sentido riguroso. De momento es suficiente con una noción vaga de ella.

Cuando diga que "seré más formal" me referiré a que "seré más riguroso y usaré el lenguaje de las matemáticas para expresar una definición". En el siguiente capítulo vamos a intruducirnos en la probabilidad de manera formal, sentando las bases para entender las propiedades y supuestos de una distribución de probabilidad.

Repase bien todo lo aprendido hasta aquí, sino no podrá avanzar.

```{admonition} Resumen
:class: important

1. **Inferencia estadística**: No siempre nos será posible obtener datos de la población, por lo que usaremos una muestra para inferir medidas de la población. El acto de estimar alguna medida de la población es hacer una inferecnia estadística.

2. **Muestreo**: Tomar una parte de las observaciones de la población es hacer un muestreo: seleccionar un subconjunto de todas observaciones de la población. Al grupo de observaciones seleccionadas se le llama **muestra**.

3. **Estimador**: Se denomina **estimador** a una medida de la muestra, que tiene intención de ser igual a la misma medida aplicada a la población. También podemos hacer las mismas mediciones con todos los datos de la población. Un **parámetro** es una medida de la población.

3. **Sesgo de selección**: Elección de muestras que conducen a un error en la estimación de algún parámetro de la población: que el valor del estimador sea diferente al del parámetro.

4. **Selección aleatoria**: Elección de observaciones de la población de forma aleatoria. Permite que los estimadores calculados con las obersvaciones de la muestra sean lo más cercanos posible a los parámetros de la población.

```
