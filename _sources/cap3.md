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

# El arte de la inferencia

En el capítulo anterior usamos datos censales, es decir, de toda la población de Ecuador. Este censo costó [83,3](https://www.primicias.ec/noticias/sociedad/censo-ecuador/inec-poblacion-roberto-castillo-criticas/) millones de dólares.

Antes había discutido cómo el coste de un censo es elevado como para levantarlo continuamente. (Aunque quizá gastamos más dinero en tonterías como sociedad, bien haríamos en priorizar la recopilación de estos datos).

Los políticos no están dispuestos a censar a la población cada año, porque tienen la opción de usar el dinero que gastarían en un censo en otras cosas: como contratar propaganda para hablar bien de su gestión, aunque sea pésima.

Pero aunque no tuvieramos malos políticos ―como de hecho ocurre―, puede ser que el país enfrente una dura crisis económica, por lo que gastar dinero en un censo no sería prioridad. En esa situación sería más importante gastar ese dinero para evitar muertes infantiles, por ejemplo.

Por uno u otro motivo, el costo de un censo es elevado como para levantarlo continuamente. Entonces, ¿qué podemos hacer? Digamos que usted piensa en esto por primera vez. ¿Qué se le ocurre?

Digamos que piensa: "bueno, encuestar a todos es costoso, pero ¿y si no encuesto a todos, sino a una parte?". Entonces decide encuestar a una parte de la población: su barrio. Mejor aun a su parroquia entera.	

En el capítulo anterior analizamos qué porcentaje de hogares estaba integrado por 1, 2, 3, y así sucesvamente, hasta 34 miembros. Supongamos que el censo no se hizo, y le encomiendan determinar qué porcentaje de hogares son de una cantidad determinada de miembros.

Usamos los mismos datos que en el ejercicio anterior. El bloque de código siguiente carga los datos del censo y calcula el número de personas por hogar, por lo que puede omitirlo si no considera necesario volver a ver cómo leer los datos. En adelante, podras desplegar el código dando click en "Show code cell content".

```{code-cell} ipython3
:tags: [hide-cell]

import pandas as pd
import pyarrow

url = "C:/Users/Michael/Downloads/popec22.parquet"

df = pd.read_parquet(url, engine='pyarrow')

excluir = ['P00','P01','P02','P03']

agrupacion = [c for c in df.columns if c not in excluir]

# Al obtener el número máximo del número de persona obtendremos la cantidad de personas del hogar
personasporhogar = (
    df.groupby(agrupacion)
      .agg(numpersonas=('P00','max'))
      .reset_index()
)

# Excluir no hogares (revisar explicación cap anterior)
personasporhogar = personasporhogar[personasporhogar['INH']>0]
```

Digamos que usted vive en una parroquia del país llamada Sofía, ubicada en el cantón Sucumbíos y la provincia Sucumbíos. Usted piensa que encuestar a la todos sus vecinos de la parroquia es buena idea. 

Tomar una parte de las observaciones (en este caso los hogares) de la población se le llama **muestrar**: seleccionar un subconjunto de todas observaciones de la población. Al grupo de observaciones seleccionadas se le llama **muestra**. 

Tomada su muestra de hogares, los encuesta. Obtiene sus datos; los tabula; hace el mismo análisis que ya hicimos en el capítulo anterior: cuenta el número de hogares por tamaño; luego los expresa como porción del total de hogares y los grafica. Las siguientes líneas de código hacen esto, mostrando los resultados como una distribución. Obsérvela.
  
```{code-cell} ipython3
:tags: [hide-input]

import altair as alt

# Elección de todos los datos de su parroquia
# Provincia: Sucumbíos, Cantón: Sucumbíos, Parroquia: La Sofía
# código: 210552
parroquia = personasporhogar[
    (personasporhogar['I01'] == 21) & 
    (personasporhogar['I02'] == 5) & 
    (personasporhogar['I03'] == 52)
]

# Obtenemos la probabilidad por tamaño de hogar
freq_parroquia = (
    parroquia['numpersonas']
    .value_counts(normalize=True)
    .sort_index()
    .reset_index()
)

# Graficar resultado
chart = alt.Chart(freq_parroquia).mark_bar(
    size=25
).encode(
    x=alt.X(
        'numpersonas:O',
        sort=None,
        title='Número de personas en el hogar',
        axis=alt.Axis(labelAngle=0)
    ),
    y=alt.Y(
        'proportion:Q',
        title='Porcentaje de hogares',
        axis=alt.Axis(format='.0%')
    ),
    tooltip=[
        alt.Tooltip('numpersonas:O', title='Número de miembros'), 	
        alt.Tooltip('proportion:Q', title='Probabilidad del evento', format='.2%')
    ]
).properties(
    title="Distribución del tamaño del hogar",
    width=700,
    height=400
)

chart
```

## Sesgo de selección

Como nota, esta distribución es diferente a la distribución de la población. De hecho, podemos comparar la distribución de su parroquia y la de la población en un mismo gráfico, el de abajo.

```{code-cell} ipython3
:tags: [hide-input]

# Probabilidades de la población
freq_df = (
    personasporhogar['numpersonas']
    .value_counts(normalize=True)
    .sort_index()
    .reset_index()
)

# Unir distribuciones
freq = freq_df.rename(columns={'proportion': 'poblacion'}).merge(
    freq_parroquia.rename(columns={'proportion': 'muestra'}), 
    on='numpersonas', how='left'
)

# Cambiamos la estructura de la tabla
freq_resize = freq.melt(
    id_vars='numpersonas',
    var_name='grupo',
    value_name='porcentaje'
)

chart = alt.Chart(freq_resize).mark_bar(
    size=10 # más ancho (porque hay xOffset)
).encode(
    x=alt.X(
        'numpersonas:O',
        title='Número de personas en el hogar',
        axis=alt.Axis(labelAngle=0)
    ),
    y=alt.Y(
        'porcentaje:Q',
        title='Porcentaje de hogares',
        axis=alt.Axis(format='.1%')
    ),
    color=alt.Color(
        'grupo:N',
        sort=['poblacion','muestra'],
        title='',
        legend=alt.Legend(orient='top'),   # mueve la leyenda arriba
        scale=alt.Scale(
            domain=['poblacion','muestra'],
            range=['#013440', '#593954']
        )
    ),
    xOffset=alt.XOffset(
        'grupo:N',
        sort=['poblacion','muestra']   # importante también aquí
    ),
    tooltip=[
        alt.Tooltip('numpersonas:O', title='Personas'),
        alt.Tooltip('grupo:N', title='Grupo'),
        alt.Tooltip('porcentaje:Q', title='Porcentaje',format='.2%')
    ]
).properties(
    title="Distribución del tamaño del hogar",
    width=700,
    height=400
)

chart
```

Pensemos un poco. ¿No es posible que su parrroquia tenga un número de miembros bastante diferente al de las demás? Ya sea porque hay costumbres familiares particulares; una propensión a tener una cantidad específica de hiijos; quizá tiene una economía y cultura que influye en que los tamaños de hogar sean diferentes a los de otras parroquias. Favorecer su parroquia en lugar de otras es sesgado. ¿Por qué no elegir otra parroquia?

Incluso si toma otra parroquia podría pasar que también tiene una distribución diferente al de la población, y su meta es caracterizar el país.

### Estimador y parámetro

Cada porcentaje que calculamos con los datos de nuestraes un *estimador*. Se denomina estimador a una medida de la muestra, que tiene intención de ser igual a la misma medida aplicada a la población. 

Nuestro estimado en este caso es el porcentaje de hogares por tamaño. Pero podemos construir muchos estimadores, por ejemplo: el porcentaje de personas del hogar que son mujeres; el porcentaje de personas del hogar que son hombres; el porcentaje de personas del hogar que son niños, etc.

También podemos hacer los mismos cálculos con todos los datos de la población. A las medidas de la población se les conoce como **parámetros**. Un **parámetro** es una medida de la población.

Nuestro propósito es que nuestro parámetro sea igual al estimador. En este caso, que el porcentaje calculado con nuestra muestra sea igual al porcentaje que obtendríamos si el cálculo se hiciera con la población. En otras palabras, que nuestro estimador sea una buena estimación de nuestro parámetro. Como en la vida real, por varios motivos y factores, es muy, muy, muy poco probable que logremos que el estimador sea igual al parámetro, queremos que sea lo más cercano posible; es decir, que la diferencia sea lo más pequeña posible (tienda a 0, si hablamos con lenguaje del cálculo).

Hablamos de **sesgo de selección** cuando la elección de las observaciones nos conduce a un error en la estimación de algún parámetro de la población: que el valor del estimador sea diferente al del parámetro. Por ejemplo, en nuestro caso los porcentajes de hogares de 2 miembros de la muestra y la población son 21,05% 11,30%, respectivamente. Una diferencia de casi 10 puntos porcentuales. No es el mejor estimador, porque no elegimos la mejor muestra.

## Selección aleatoria

La cantidad de hogares en su parroquia Sofía son 19.

```{code-cell} ipython3
print(f'El número de hogares en la parroquia Sofía es {parroquia.shape[0]}')
```

¿Qué tal si en lugar de selecionar hogares de una parroquia elegimos una parte de los hogares de todo el país? Un puñado de cada cantón y provincia. Y hacemos la selección de forma aleatoria. En el siguiente gráfico seleccionamos aleatoriamente 10 hogares al inicio, luego 30, 50, 100, 1.000, etcétera. Puede usar el deslizador del gráfico para cambiar el tamaño de la muestra aleatoria. Además, puede dar "play" para ver cómo se comporta el estimador a medida que aumenta el tamaño de la muestra.

```{code-cell} ipython3
:tags: [hide-input]

import plotly.express as px

sizepop = len(personasporhogar)

# Distribución población
freq_poblacion = (
    personasporhogar['numpersonas']
    .value_counts(normalize=True)
    .sort_index()
    .reset_index()
)

freq_poblacion.columns = ['numpersonas','porcentaje']
freq_poblacion['grupo'] = 'poblacion'
freq_poblacion['n'] = sizepop

# Tamaños muestrales pedagógicos
tamanos = [10, 30, 50, 100, 1000, 10000, 100000, 1000000]

# Filtrar si alguno supera la población
tamanos = [n for n in tamanos if n <= sizepop]

# Generar muestras
lista = []

for n in tamanos:

    muestra = personasporhogar.sample(
        n=n,
        random_state=123
    )

    freq_muestra = (
        muestra['numpersonas']
        .value_counts(normalize=True)
        .sort_index()
        .reset_index()
    )

    freq_muestra.columns = ['numpersonas','porcentaje']
    freq_muestra['grupo'] = 'muestra'
    freq_muestra['n'] = n

    lista.append(freq_muestra)

df_muestras = pd.concat(lista)

df_total = pd.concat([
    df_muestras,
    freq_poblacion
])

fig = px.bar(

    df_total,

    x="numpersonas",
    y="porcentaje",

    color="grupo",

    barmode="group",

    animation_frame="n",

    color_discrete_map={
        "poblacion":"#013440",
        "muestra":"#593954"
    },

    labels={
        "numpersonas":"Número de personas en el hogar",
        "porcentaje":"Porcentaje",
        "grupo":"",
        "n":"Tamaño muestra"
    },

    title="Distribución del tamaño del hogar: convergencia muestral"

)

fig.update_layout(

    width=700,
    height=500,

    yaxis_tickformat=".1%",

    legend=dict(
        orientation="h",
        y=1.1
    )

)

fig.show()
```

¿Qué sucede con el estimador a medida que aumenta el tamaño de la muestra? ¿Se parece más a la distribución de la población? ¿Disminuye la diferencia entre el estimador y el parámetro?

Como puede ver, la estimación mejora conforme aumentamos el tamaño de la muestra. Cuando la muestra tiene 10 hogares, el estimador es muy diferente al parámetro. Cuando tiene 100, mejora. Cuando tiene 1000, mejora aún más. Así sucesivamente hasta 1.000.000 de hogares; en este caso, el estimador es muy cercano al parámetro. Conforme aumentan las observaciones de la muestra, nuestro estimador se acerca más al parámetro.

Pasan dos cosas aquí. Primero, la distribución de la muestra se parece más a la distribución de la población cuando es aleatoria. Mejora más cuando la selección es aleatoria y el tamaño de la muestra es mayor. Segundo, la diferencia entre el estimador y el parámetro disminuye. En otras palabras, el estimador se acerca más al parámetro.

Analicemos una cosa: ¿qué pasaría si elegimos una muestra sesgada? No obtendríamos una buena estimación de la población. Puede ser incluso que esta muestra tenga más observaciones que el de una selección aleatoria y sería peor opción para calcular nuestro estimador. Por eso es importante que la selección sea aleatoria.

Un asunto que puede preguntarse es ¿qué tan grande debe ser el tamaño de una buena muestra para obtener un buen estimador? Responderemos esta pregunta en los siguientes capítulos. Sea paciente. Concepto a concepto.

# Una idea vaga de la Ley de grandes números

Empíricamente hemos observado que aumentar la cantidad de observaciones en la muestra aleatorua mejora la estimación. La ley de los grandes número resume esta idea: aumentar el tamaño de la muestra hace que los valores de estimadores sean más cercanos a los valores de los parámetros.

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