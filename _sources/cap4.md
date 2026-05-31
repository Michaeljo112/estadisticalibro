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

Como ejercicio intelectual, supongamos que usted hubiese podido observara la conformación de todos los hogares. Imagínese un observador omnipresente que puede viajar al pasado y presenciar la evolución de la formación de los hogares. Usted, sin embargo, no tiene el poder de saber el resultado, solo puede presenciar y tomar apuntes. También suponga que el viaje le borra la memoria y usted no sabe cuántos hogares de un tamaño determinado existirán en el 2022 de Ecuador. Entonces, antes que se constituyan los hogares, usted hará un experimento.

## Experimento

En el contexto de la probabilidad, un **experimento** es un proceso, situación o acción cuyo resultado no conocemos con certeza antes de realizarlo. 

Usted debería esperar, como ese observador, a que se conformen los hogares y luego censar a los pobladores para conocer la distribución del tamaño de los hogares.

Como dijimos en el capítulo anterior, la probabilidad es la frecuencia relativa. Profundicemos esa idea.

Los experimentos serían, en diversos contextos, el proceso que genera los resultados. En nuestro ejercicio, nosotros no emparejamos a las personas. Esperamos y observamos. El proceso es la demografía. También podemos pensar en el experimento como la situación: la conformación de hogares. En otras situaciones, el proceso será lanzar una moneda --la acción--.

El experimento es el proceso generador de resultados. Por lo tanto, si queremos contar los puntos de las caras de dos dados, hacemos un experimento al lanzarlos al aire. Si empezamos a mirar con atención el precio de un activo en el mercado de valores, también estamos haciendo un experimento. Existen varias situaciones de interés en las que hacemos experimentos, ya sean mentales, como en nuestro ejemplo del observador omnipresente sin memoria que viaja al pasado para observar la constitución del tamaño de los hogares, o físicos: como al medir la temperatura. Eso sí, **cuando no podemos saber con certeza el resultado**.

Note que al lanzar una moneda podemos obtener dos caras. Si lanzamos al aire dos dados, 2 caras con puntos entre 1 y 6 cada una. Si miramos el precio de un activo, un rango de precios, expresados en números reales. Los resultados, todos, contados, se conocen como espacio muestral.

## Espacio muestral

Todos los resultados de un experimento son el espacio muestral. Note que "todos los resultados" pueden representarse en un conjunto de todas las opciones producidas por el experimento. En la Teoría de la Probabilidad (TP), una rama de las matemáticas que estudia la probabilidad, se utilizan los conjuntos como elementos clave. Estos nos permiten ponerle un número a los procesos estocásticos.

## Procesos estocásticos

Un sistema **estocástico** es aquel comportamiento **no determinista**. En ellos no podemos asegurar, predecir o adivinar con certeza un resultado.

Cuando no podemos asegurar con certeza, pensamos en posibilidades. Como señaló {cite}`grimmett_probability_2020`: 
>Muchas afirmaciones cotidianas tienen la forma: “la posibilidad —o probabilidad— de que ocurra A es p”, donde A es algún evento, como “que mañana brille el sol” o “que Cambridge gane la regata Boat Race”, y p es un número o adjetivo que describe una cantidad, como “un octavo”, “baja”, etc.

No está demás precisar que Teoría es, en ciencia, explicación exhaustiva y comprobable de algún aspecto del universo. Así que la TP es una descripción rigurosa de los fenómenos aleatorios.

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

Un evento A, digamos, puede ser: que la suma de las caras sea par: {2, 4, 6, 8, 10, 12}, o que la suma sea impar {3, 5, 7, 9, 11}. Hay varios eventos que son subconjuntos del espacio muestral.

Al lanzar los dados tendremos solo un resultado, digamos: 3 en un dado, y 5 en el otro. La suma sería 3 + 5 = 8. El resultado del experimento es 8, entonces. El evento "suma par" ocurrió. Cualquier resultado que esté en A implica que A ocurra (se dé, tenga lugar, suceda).

## Conjuntos y definiciones formales

Empecemos a expresar estos conceptos de forma económica, es decir, sin tener que repetir largas oraciones:

> **Espacio muestral**: conjunto, S, de todos los resultados posibles generados con el experimento. <br>
> **Evento**: $A \subseteq S$. Note que escribimos $\subseteq$ ya que A puede ser B.

Construimos definiciones justamente, entre otros propósitos, para no repetir un párrafo completo cada vez que tengamos que trabajar sobre una situación en la que tengamos que estimar la posibilidad de una ocurrencia de un evento. Es fácil emplear símbolos para comunicarnos con otros, además, sin los problemas del idioma, la mala comunicación de ambos, o otras minucias.

Partiendo de estas definiciones, queremos cuantificar la posibilidad de ocurrencia de un evento. Ponerle un número, que dé cuenta de la magnitud de esa posibilidad.  En el [capítulo 2](cap2.md#la-frecuencia-como-probabilidad) dijimos que la probabilidad era la frecuencia relativa, y dividimos la cantidad de hogares de un tamaño para la cantidad total de hogares del país. Los eventos podían haberse definido como: "el hogar sea de 1 miembro", "el hogar sea de 2 miembros", etc. Siendo más breves: "el hogar sea de *i* miembros"; de esta manera, i puede ser algún valor del conjunto {1, 2, 3, ..., 34}.

También podíamos escribir, deseando ser ocupar menos espacio:

$A_i := \text{el hogar sea de } i \text{ miembros}, \forall i \in \{1, 2, 3, ..., 34\}$
o

$A_i := \text{el hogar sea de } i \text{ miembros}, \forall i = 1, 2, 3, ..., 34$.

Escribir $A_i$ nos permite definir un evento para cada cantidad de miembros, e identificar el evento.

Quiero que se dé cuenta de que el uso de símbolos matemáticos nos permite ser precisos y breves.

Continuemos.

Al medir la probabilidad, estamos calculando la frecuencia relativa. Siendo específicos, dado un evento $E$ contamos todos los resultados potenciales que conforman el conjunto del evento (hogar de $i$ miembros en nuestro análisis de los hogares) y lo dividimos para la cantidad de eventos posibles del espacio muestral (total de hogares de Ecuador). 

Ese conteo se puede expresar matemáticamente (con símbolos, precisión y brevedad) con $n$. Así, con un conjunto $C$, $n(C)$ es la cantidad de elementos del conjunto $C$.

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
P(M) = \frac{n(M)}{n(S)} = \frac{8.686.463}{16.938.986} \approx 0.512809 \approx 51.28\%
$$ 

# Eventos conjuntos y condicionalidad

Ahora consideremos la distribución por edad de hombres y mujeres.

```{code-cell}
df["sexo"] = df["P02"].map({
    1: "Hombre",
    2: "Mujer"
})

tabla = pd.crosstab(df["P03"], df["sexo"], margins=True)
tabla
```

En la tabla de arriba podemos ver cuántas mujeres y hombres de determinada edad hay. Como puedes ver, tenemos personas que alcanzan hasta los 120 años; cosa que es muy extraña, pero así constan los registros. Para poder resumir estos datos, usemos rangos de edad de 10 años, y asignemos cada rango de edad de menor a mayor a los números 1, 2, 3, etc.

```{code-cell} ipython3
bins   = list(range(0, 111, 10)) + [121]
labels = [f'{i}-{i+9}' for i in range(0, 110, 10)] + ['110-120']

df['rango_edad'] = pd.cut(df['P03'], bins=bins, labels=labels, right=False)
cod_rango = {label: j+1 for j, label in enumerate(labels)}
df['cod_rango'] = df['rango_edad'].map(cod_rango)

tabla_rangos = pd.crosstab(df['rango_edad'], df['sexo'], margins=True)
tabla_rangos = tabla_rangos.assign(
    cod_rango=tabla_rangos.index.map(cod_rango)
)

tabla_rangos
```

La tabla anterior resume cuántas mujeres y hombres hay en cada rango de edad, y asigna a cada rango un código numérico. Ahora, pensemos en los eventos que podemos conformar con los rangos de edad. Definamos eventos $Y_j := \text{que la persona tenga una edad en el rango de edad } j$. Además, podemos definir los eventos "ser mujer y tener 15 años" (ser mujer y tener una edad en el rango 2) o "ser hombre y tener 20 años" (ser hombre y tener una edad en el rango 3). Pensemos en ellos de forma gráfica.

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

Notemos que otra forma de escribir $P(Z_2) = P(\text{ser mujer } \textbf{y} \text{ tener una edad en el rango 2}) = P(M \textbf{ y } Y_2) = P(M, Y_2)$. Es habitual usar coma como "y". Usaremos esta forma reducida: $P(M, Y_2)$, en adelante, para hablar de eventos conjuntos: que están intersectados, literalmente o "que ocurren juntos", como han memorizado algunos estudiantes. Mi recomendación --de las pocas que me atrevo a hacer, pues considero dar consejos una mala costumbre-- es que no memorice y entienda.

## Disjunciones

Se le ha denominado dependencia al hecho de que un evento y otro estén relacionados. Cuando no se intersectan se los considera eventos disjuntos o mutuamente excluyentes. Eso no es lo mismo que independencia.

Si yo quisiera estimar la probabilidad de que ser mujer y hombre tendría que estimar:

$$
P(H, M) = P(H \cap M) = P(\emptyset)
$$

Si yo quisiera estimar la probabilidad de que ser mujer y hombre tendría que estimar:

## $ \emptyset $

$\emptyset$ no tiene ningún elemento 
($n( \emptyset ) $ = 0). Le parecerá intuitivo que la probabilidad de algo que no tiene elementos sea 0. Esa intuición puede ser una restricción que imponemos. Efectivamente, los matemáticos imponen restricciones a sus cuerpos teóricos. Restrinjamos, entonces, que $P(\emptyset) = 0$.

## $ S $

Por otra parte, pensemos en $P(S)$ (recuerda que S es todo el espacio muestral). Como $S$ son todos los resultados posibles, digamos que fueran $N$ resultados, $P(S) = n(S)/n(S) = N/N = 1$. La intuición sugeriría que considerar todos los elementos implica que siempre suceden todos los resultados posibles. Sí, es una intuición útil. La refinaremos en los próximos capítulos.

# Filtros, condicionalidad

Por otra parte, pensemos en la composición de mujeres por edad. Dividiremos la cantidad de mujeres de cada edad para el total de mujeres.

```{code-cell}
n_mujeres = tabla_rangos.loc[tabla_rangos.index != "All", "Mujer"]

pd.DataFrame({
    "n_mujeres": n_mujeres,
    "porcentaje": n_mujeres / tabla_rangos.loc["All", "Mujer"] * 100
})
```

Si el evento es $A_k := \text{ser una mujer de edad dentro del rango } k$, en la tabla anterior calculamos $n(A_k)/n(M)$. Ahora, consideremos esa división y reescribámosla:

$$
\frac{n(A_k)}{n(M)} = \frac{n(A_k)}{n(M)} \cdot 1 =
\frac{n(A_k)}{n(M)} \cdot \frac{\frac{1}{n(E)}}{\frac{1}{n(E)}} =
\frac{\frac{n(A_k)}{n(E)}}{\frac{n(M)}{n(E)}} =
\frac{P(A_k)}{P(M)}
$$

$A_2$ puede ser reescrito como $A_2 := \text{ser mujer y tener una edad en el rango 2} := M \cap Y_2$, de modo que, teniendo en cuenta la expresión de arriba:

$$
\frac{P(A_k)}{P(M)} = \frac{P(M \cap Y_2)}{P(M)} = 
\frac{P(M, Y_2)}{P(M)} = \frac{P(Y_2, M)}{P(M)} 
$$

Dada la población de Ecuador, tomamos las ~8.2 millones mujeres, y dentro de ellas identificamos a 15.420.88 de edades entre 10 - 19 (rango 2). Calculamos el peso de las mujeres de edades entre 10 - 19 en el total de mujeres. Otra forma de decirlo es que calculamos el peso o la porción. Estamos filtrando. También podríamos decir que estamos **calculando la probabilidad de Y_2 en M**.
A este ejercicio de filtrar y calcular la probabilidad de un evento en otro se denomina probabilidad condicional. Y es equivalente decir probabilidad de Y_2 dado M, y escribir:

$$
P(Y_2 | M) = \frac{P(Y_2, M)}{P(M)}
$$

Este enfoque de segmentación es muy importante, estudiante, así que será mejor que lo repase hasta que quede claro. Tómese el tiempo que necesite, pero no avance hasta que esté claro.

En general, la probabilidad de un evento A dado un evento B es

$$
P(A | B) = \frac{P(A, B)}{P(B)}
$$


## Ocurrencias temporales

Hasta aquí, hemos analizado casos estáticos. Un punto del tiempo, datos de 2022. Pero qué ocurre cuando consideramos casos dinámicos: sucesos en que ocurren en el tiempo.

Consideremos el lanzamiento de una moneda. Si lanzo una moneda una vez, el espacio muestral es cara (C) y sello (S): $S = \{C, S\}$. Si vuelvo a lanzar la cara tendré otro espacio muestral $\{C, S\}$ en el siguiente intento. Cada intento podría anclarse a un punto del tiempo $t$. 

Hagamos un esquema de cuatro lanzamientos, como un árbol de bifurcación. En cada punto del tiempo el experimento vuelve a abrir dos caminos posibles:

![Árbol de bifurcación de cuatro lanzamientos de una moneda](imagenes/arbol_lanzamientos_moneda.svg)

Para cada lanzamiento existen dos opciones en el siguiente.

Si quisiera analizar cuatro lanzamientos como un todo, el espacio muestral de cuatro lanzamientos entonces es:

$$
S = \{(C, C, C, C), (C, C, C, S), (C, C, S, C), (C, C, S, S), (C, S, C, C), (C, S, C, S), (C, S, S, C), (C, S, S, S), (S, C, C, C), (S, C, C, S), (S, C, S, C), (S, C, S, S), (S, S, C, C), (S, S, C, S), (S, S, S, C), (S, S, S, S)\}
$$

Cada rama completa del árbol representa una ocurrencia temporal: primero observamos el resultado en $t_1$, luego en $t_2$, después en $t_3$ y finalmente en $t_4$.

Cada vector elemento de $S$ indica la secuencia de lanzamientos.

Consideremos lanzar un dado, ahora. Concentrémonos en 3 lanzamientos.

![Árbol compacto de tres lanzamientos de un dado](imagenes/arbol_lanzamientos_dado_3.svg)

Para cada lanzamiento, existen 6 resultados posibles en el siguiente lanzamiento. Consideremos los eventos $G := \text{ser un número primo}$ y $I := \text{ser un número mayor que 1}$. Centrémonos en dos lanzamientos del dado: pensemos en la probabilidad de que el evento G se dé en el primer lanzamiento y en el segundo.

Para el primer lanzamiento existen 3 opciones: $G = \{2, 3, 5\}$, para el segundo 5: $I = \{2, 3, 4, 5, 6\}$. O sea, en el primer lanzamiento puedo obtener cualquier resultado de $G$ y para cada uno de esos resultados podría obtener un resultado de $I$. Puedo combinar cada número resultado de $G$ se puede combinar con cada número posible de $I$.

![Combinaciones de un número primo en el primer lanzamiento y un número mayor que 1 en el segundo](imagenes/diagrama_dado_primo_mayor_1.svg)

Note que una vez que lanzo el dado, el segundo lanzamiento no está en nada condicionado por el primero. Hay 6 resultados para el primer lanzamiento, en este lanzamiento esperamos que ocurra $G$. Denotaremos el resultado real del primer lanzamiento con $r_1$. Si el resultado está en $G$, lo denotaremos $r_1^1$; sino, $r_1^0$. Los subíndices indicarán qué lanzamiento es, y los superíndices si ocurrió o no el evento deseado en el lanzamiento. Además, $r_1^1$ puede ser cualquier valor de $G$, por lo que existen $n(G) = g$ casos favorables.

Los resultados posibles del segundo lanzamiento son 6, y aquí queremos que ocurra $I$. Denotaremos el resultado real del segundo lanzamiento con $r_2$ y si está en $I$ escribiremos $r_2^1$, sino $r_2^0$. Además, $r_2^1$ puede ser cualquier valor de $I$, por lo que existen $n(I) = i$ casos favorables.

Podemos verificar si un evento del primer lanzamiento sucedió con una función, que podemos llamar O (de ocurrencia). $O(r_1) = r_1^1$ si el resultado en el primer lanzamiento estuvo en $G$; y $O(r_1) = r_1^0$, sino. Así mismo con $r_2$: $O(r_2) = r_2^1$ si el resultado en segundo lanzamiento estuvo en $I$; y $O(r_2) = r_2^0$, sino.

Como $r_1$ puede ser cualquier elemento de $G$, y $r_2$ puede ser cualquier elemento de $I$, sabemos que las combinaciones de los lanzamientos serán $g \cdot i = n(G) \cdot n(I)$ (para cada resultado posible de $G$ hay un resultado posible de $I$). Además, consideremos que los resultados posibles del primer lanzamiento son 6. En este sentido, denotemos los resultados posibles del primer lanzamiento con el conjunto $S_1$, que sería el espacio muestral $\{1, 2, 3, 4, 5, 6\}$. Así, la cantidad de resultados posibles del primer lanzamiento serían $n_1 = n(S_1)$. En el segundo lanzamiento existen $S_2 = \{1, 2, 3, 4, 5, 6\}$ resultados posibles y contándolos: $n_2 = n(S_2)$.

Así que para cada posible resultado del primer lanzamiento existe $n_2$ en el segundo. Entonces, en total existen $n_1*n_2=n(S_1)*n(S_2)$ posibilidades en los que $G$ e $I$ ocurran secuencialmente. En este caso, los resultados posibles en el primer y el segundo lanzamiento son iguales ($n_1 = n_2 \iff n(S_1) = n(S_2)$). Pero no siempre es así. Consideremos el ejemplo el siguiente ejemplo:

Una caja contiene piezas producidas en las fábricas 1 y 2. Digamos que analizamos los eventos: "ser pieza estándar de la fábrica 1" (P) y "ser pieza estándar de la fábrica 2" (Q). En la fábrica 1 habrá un espacio muestral ($S_1$): cantidad de piezas producidas en la fábrica 1 ($n(S_1)$), y en la fábrica 2 otro espacio muestral ($S_2$): la cantidad de piezas producidas en la fábrica 2 ($n(S_2)$). No necesariamente las fábricas producen la misma cantidad de piezas, y de hecho casi nunca lo harán en la práctica.

Entonces, para cada resultado de la fábrica 1 existirá un resultado de la fábrica 2: esto se expresa como producto: $n(S_1) \cdot n(S_2) = n_1 \cdot n_2$.

```{note}
Saqué el ejemplo de las fábricas de *TEORÍA DE LAS PROBABILIDADES Y ESTADÍSTICA MATEMÁTICA* de V.E. GMURMAN, que hace años, cuando buscaba una explicación como estudiante universitario de por qué las fórmulas de probabilidad de independencia se escribían como se escribían, en tiempos de no IA, fue el único que me dio claridad. Uno le guarda cariño a estas cosas. En realidad, modifiqué el ejemplo, en aras de la comprensión. En fin. Sigamos.
```

Es decir, habitualmente: $g_1$ (cantidad de resultados en $G$) < $n_1$ (espacio muestral del primer lanzamiento); y $g_2$ (cantidad de resultados en $I$) < $n_2$ (espacio muestral del segundo lanzamiento). Siendo más precisos:

$$
g_1 \leq n_1 
$$

y 

$$
g_2 \leq n_2
$$

En total, en dos lanzamientos los resultados de $G$ e $I$ si ocurren secuencialmente serían $g \cdot i$, en casos totales $n_1 \cdot n_2$. Entonces, la probabilidad de que ocurran $G$ y $I$ se escribiría:


$$
P(G, I) = \frac{g \cdot i}{n_1 \cdot n_2} = \frac{g}{n_1} \cdot \frac{i}{n_2} = \frac{n(G)}{n(S_1)} \cdot \frac{n(I)}{n(S_2)}
= P(G) \cdot P(I) 
$$

## Independencia

Como notó en los análisis anteriores, cuando dos eventos coexisten ocurriendo el uno sin injerencia del otro, en el sentido de que sus procesos generadores (experimentos) no están condicionados mutuamente o unilateralmente, concluimos que

$$
P(G, I) = P(G) \cdot P(I) 
$$

En general, podemos escribir que dados dos eventos $A$ y $B$:

$$
P(A, B) = P(A) \cdot P(B) 
$$

cuando $A$ y $B$ son independientes.

## Discusión

Como nota, hay dos casos en los que podemos pensar la probabilidad independiente:

1. Dos eventos secuenciales en el tiempo, donde la generación de uno no afecta la del siguiente. Los resultados del evento que sucede después no están contenidos en los del primero.
2. Eventos que ocurren en el mismo momento del tiempo, pero donde conocer el resultado de uno no cambia la probabilidad del otro. En este caso no estamos pensando en una secuencia, sino en dos características, clasificaciones o mediciones observadas al mismo tiempo. Por ejemplo, podríamos preguntar si una pieza viene de cierta fábrica y, además, si cumple cierto estándar de calidad. Si conocer la fábrica de origen no cambia la probabilidad de que la pieza sea estándar, entonces esos eventos pueden tratarse como independientes. Esto no debe confundirse con eventos excluyentes o disjuntos. Por ejemplo, "ser hombre de 25 años" y "ser mujer de 25 años" no pueden ocurrir en la misma persona: son mutuamente excluyentes, no independientes. Que dos eventos no puedan ocurrir juntos significa que su intersección es vacía; que sean independientes significa que conocer uno no cambia la probabilidad del otro.

## Condicionalidad e independencia

Habíamos definido también, antes que

$$
P(A | B) = \frac{P(A, B)}{P(B)}
$$

El enfoque abordado nos permitió entender que la probabilidad condicional era una estimación de la ocurrencia de un subconjunto en otro. Si un conjunto pertenece a otro, tiene elementos en común. Su intersección es diferente del conjunto vacío.

Usemos un ejemplo, solo por familiaridad: si yo soy parte de la Universidad Central del Ecuador, y estudio en una de sus Facultades: la de Economía, bueno, resulta que ambas tienen elementos en común. Si pienso en ambas como conjuntos, y los intersecto, yo estoy en la intersección: soy el elemento en común. (Esto le puede resultar evidente, ahora que se lo digo, pero se lo dije por una razón).

Ahora, pensemos: en nuestra definición de probabilidad condicional $P(A|B)$ comparamos la probabilidad de $A$ dentro del conjunto $B$ con la probabilidad de $A$ en todo el espacio muestral. Si conocer que ocurrió $B$ no cambia la probabilidad de $A$, entonces los eventos son independientes.

Dicho de otra manera:

$$
A \text{ y } B \text{ son independientes} \iff P(A, B) = P(A) \cdot P(B)
$$

Es importante, recapitulando, que le quede claro que en los ejemplos examinados la ocurrencia de un evento no produce nada la del otro. En nuestro caso de los lanzamiento del dado, el siguiente lanzamiento es independiente del anterior; en el caso de las fábricas, examinadas por separado, en un contexto sin colusión, en donde no se coordinan para subir o bajar la producción una después de la otra, tampoco hay cambios de un experimento al otro.

Esta es la lógica de la probabilidad de sucesos compuestos y secuenciales. Y es la **definición de probabilidad de sucesos independientes**. Gaste tiempo en comprenderla. Es esencial. Disculpe si no puedo ser más claro, he intentado todo lo que me ha sido posible.

## Dependencia: cuando un evento cambia la probabilidad de otro

Veamos el contraste entre independencia y dependencia con una urna. Consideremos una urna con 5 bolillas blancas y 3 bolillas negras. En total hay 8 bolillas. Extraemos una bolilla al azar y definimos el evento:

$$
A := \text{extraer una bolilla blanca en la primera extracción}
$$

Como hay 5 bolillas blancas de 8 bolillas en total, la probabilidad de $A$ es:

$$
P(A) = \frac{5}{8}
$$

Ahora devolvemos la bolilla extraída a la urna y repetimos la prueba. Es decir, antes de la segunda extracción la urna vuelve a tener la misma composición inicial: 5 blancas y 3 negras. Definamos:

$$
B := \text{extraer una bolilla blanca en la segunda extracción}
$$

Como la bolilla de la primera extracción fue devuelta, el resultado de la primera extracción no cambia la composición de la urna para la segunda. Por lo tanto:

$$
P(B) = \frac{5}{8}
$$

Además, si sabemos que en la primera extracción ocurrió $A$, la probabilidad de $B$ sigue siendo la misma:

$$
P(B \mid A) = \frac{5}{8} = P(B)
$$

En este caso, $A$ y $B$ son eventos independientes. La ocurrencia del primer evento no modifica la probabilidad del segundo.

La dependencia aparece cuando no devolvemos la bolilla. Si en la primera extracción salió una bolilla blanca y no la regresamos a la urna, para la segunda extracción quedan 4 bolillas blancas y 3 negras; en total, 7 bolillas. Entonces:

$$
P(B \mid A) = \frac{4}{7}
$$

Pero:

$$
P(B) = \frac{5}{8}
$$

Como:

$$
P(B \mid A) \neq P(B)
$$

decimos que, sin reposición, los eventos son dependientes. El resultado de la primera extracción modifica las condiciones de la segunda extracción.

En el próximo capítulo trataremos las ideas aquí presentadas con formalidad, espcificando las propiedades de la definición de probabilidad como una función y de teoremas relevantes. No te preocupes, como todo, iremos paso por paso.


```{admonition} Resumen
:class: important

1. **Experimento**: Es el proceso, situación o acción que genera resultados que no conocemos con certeza antes de observarlos.

2. **Espacio muestral**: Es el conjunto $S$ de todos los resultados posibles de un experimento. Un **evento** es un subconjunto del espacio muestral: $A \subseteq S$.

3. **Probabilidad como frecuencia relativa**: Si $A$ es un evento dentro de $S$, podemos estimar su probabilidad como $P(A) = \frac{n(A)}{n(S)}$.

4. **Eventos conjuntos y disjuntos**: La expresión $P(A, B)$ representa la probabilidad de que ocurran $A$ y $B$; es decir, $P(A \cap B)$. Si $A \cap B = \emptyset$, los eventos son disjuntos o mutuamente excluyentes, y $P(A \cap B)=0$.

5. **Probabilidad condicional**: Calcular $P(A \mid B)$ significa calcular la probabilidad de $A$ dentro del conjunto $B$. Se escribe $P(A \mid B) = \frac{P(A, B)}{P(B)}$, siempre que $P(B)>0$.

6. **Independencia**: Dos eventos son independientes si conocer que ocurrió uno no cambia la probabilidad del otro. En ese caso, $P(A, B) = P(A) \cdot P(B)$.

7. **Dependencia**: Dos eventos son dependientes cuando la ocurrencia de uno modifica la probabilidad del otro. En términos condicionales: $P(A \mid B) \neq P(A)$.

```
