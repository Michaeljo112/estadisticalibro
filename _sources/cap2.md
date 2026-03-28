---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.19.1
kernelspec:
  name: python3
  display_name: Python 3
---

# Mirar los datos

Hagámonos una pregunta: ¿cuántas personas hay por hogar en el Ecuador? Para responderla, usemos los datos del censo de 2022, como antes.

Los datos que el INEC se pueden descargar de su página web, pero son archivos *.csv* que son bastante pesados para procesar en tu computadora. Por eso, preparé un archivo *parquet* con datos suficientes para que puedes usarlo sin problema. Este tipo de archivo sirve para almacenar grandes conjuntos de datos de forma eficiente, se usa en Big Data.

Leamos tales datos.

```{code-cell}
# Leemos los datos de población del censo de 2022 a nivel de hogar y sexo
import pandas as pd
import pyarrow

url = "https://github.com/Michaeljo112/estadisticalibro/releases/download/popec22/popec22.parquet"

df = pd.read_parquet(url, engine='pyarrow')

df.head()
```

Ahora, vamos a obtener un conteo de la cantidad de personas por hogar. En los datos del INEC se enumeró a cada persona del hogar, así que para obtener la cantidad de personas por hogar basta con obtener el número máximo de la columna *P00* por hogar de forma agrupada. 

```{code-cell}
# Diccionario de columnas
"""
I01 Provincia
I02 Identificador de Cantón
I03 Identificador de Parroquia
I04 Zona
I05 Sector
I10 Número de vivienda
INH Número de hogar
P00 Número de persona
P01 Parentesco o relación con el representante del hogar
P02 Sexo al nacer
P03 Años cumplidos
"""

excluir = ['P00','P01','P02','P03']

agrupacion = [c for c in df.columns if c not in excluir]

# Al obtener el número máximo del número de persona obtendremos la cantidad de personas del hogar
personasporhogar = (
    df.groupby(agrupacion)
      .agg(numpersonas=('P00','max'))
      .reset_index()
)

personasporhogar
```

En su [metodología](https://www.censoecuador.gob.ec/wp-content/uploads/2024/02/1.Ficha_Met_Promedio_de_personas_por_hogar.pdf), el INEC excluye a los hogares que están clasificados con el número 0 cuando cuenta a las personas. Probablemente se trate de viviendas que no están ocupadas por hogares, ya que es habitual clasificar este tipo de viviendas como 0, pero no pude encontrar esta aclaración ni en los diccionarios ni en los metadatos públicos. —Si el INEC lee esto, le agradecería que me lo hiciera saber—. En las líneas de código de abajo usamos el mismo filtro que el INEC y contamos cuántos hogares tienen 1, 2, 3, etc. personas. (Recordemos que en las líneas de código presedentes ya habíamos obtenido la cantidad de miembros por hogar, así que ahora contaremos cuántos hogares tienen una cantidad determinada de miembros).

```{code-cell}
# Excluye hogar que están clasificados con el número 0. Así que se respetó el filtro
pararesumen = personasporhogar[personasporhogar['INH']>0]

# Ver un conteo de la cantdiad de personas en el hogar
resumen = pararesumen['numpersonas'].value_counts().sort_index().reset_index(name='numhogares')

resumen
```

Como puede observar, en el año 2022, 314.250 hogares eran de 1 persona; 431.560 hogares eran de 2 personas; 536.947 hogares eran de 3 personas, etc. Muy pocos hogares tenían más de 11 miembros. Pero resumamos la tabla obtenida graficándola. Dibujemos en el eje horizontal número de personas en el hogar y en el eje vertical la frecuencia o cantidad de hogares con ese número de personas. 

```{code-cell}
import matplotlib.pyplot as plt
import seaborn as sns
import matplotlib.ticker as ticker

plt.figure(figsize=(8,5))

sns.barplot(
    x=resumen['numpersonas'],
    y=resumen['numhogares']
)

plt.xlabel("Número de personas en el hogar")
plt.ylabel("Conteo (miles)")
plt.title("Distribución del tamaño del hogar")

# Formatear eje Y en miles
plt.gca().yaxis.set_major_formatter(
    ticker.FuncFormatter(lambda x, p: f'{int(x/1000)}K')
)

plt.show()
```

Este gráfico es una distribución estadística: la forma en la que se reparten los datos. En este caso, la mayoría de los hogares tienen entre 2 y 5 personas. Note que las barras del gráfico, vistas como un todo, parecen una campana deformada, como si la hubieran martillado.

Hay otra forma de presentar estos datos: como porcentajes. Si dividimos el número de hogares que hay en cada grupo según la cantidad de miembros por el número total de hogares (2.780.237), obtenemos la porción que respresentan. Llamamos a esta representación porcentual la **frecuencia relativa** comunmente. 

```{code-cell}
hogarestotales = sum(resumen['numhogares'])
print(f'Hay {hogarestotales} hogares en total.')
resumen['porcentaje'] = resumen['numhogares']/hogarestotales

# configurar por defecto la visualización de decimales (5 dígitos)
pd.options.display.float_format = '{:.5f}'.format

resumen
```

El 11,30% de hogares es de 1 miembro; el 15,52%, de 2; 19,31%, de 3; 22,80%, de 4; etcétera. Podemos graficar estos porcentajes:

```{code-cell}
plt.figure(figsize=(8,5))

sns.barplot(
    x=resumen['numpersonas'],
    y=resumen['porcentaje'] 
)

plt.xlabel("Número de personas en el hogar")
plt.ylabel("Frecuencia relativa")
plt.title("Distribución relativa del tamaño del hogar")

plt.show()
```

Como nota, el gráfico conserva su forma; esto es porque solo es una forma diferente de personificar la misma información. Lo que mostramos en el gráfico de arriba es la frecuencia relativa, es decir, la porción de hogares que hay en cada grupo según la cantidad de miembros por el número total de hogares.

```{note} Nota
La información es el significado que les damos a los datos. En nuestro análisis, cada fila de la tabla empelada es un dato y los volvimos información al analizar la distribución.
```

## La frecuencia como probabilidad

Anteriormente dividimos el número de hogares según su tamaño por el número total de hogares para obtener la frecuencia relativa. Es decir, cuántos hogares de un miembro había para el total, cuántos de 2 para el total, cuántos de 3 para el total, et. al. Dividimos la cantidad de veces que ocurrió un evento (ser un hogar de una cantidad de miembros) por el total de eventos (el número de hogares). En este apartado veremos que esta frecuencia relativa es una estimación de la probabilidad de que un hogar tenga un tamaño determinado.

Usar el término "frecuencia" resume el hecho de cuántas veces ocurre un evento respecto al total de eventos. El nombre que usamos para referinos al total de eventos es **espacio muestral**. Más adelante quedará claro por qué "muestral", de momento es importante notar que la frecuencia relativa de un evento es el porcentaje que representa respecto al espacio muestral.

Consideremos otro ejemplo: si lanzamos un dado, el espacio muestral son los puntos de sus caras {1, 2, 3, 4, 5, 6}. La frecuencia relativa de que veamos un punto en una de sus caras es una de seis (1/6); de que salga 2, una de sesis (1/6), etc.

Al hablar de probabilidad aludimos a la frecuencia relativa de un evento. Por ejemplo, en nuestro caso, la frecuencia o probabilidad de que un hogar en el Ecuador sea de 1 miembro es 11,30%. Otra forma de ver ese 11,30% es pensar así: 113 de cada 1000 hogares tienen 1 miembro, porque 113/1000 = 11,30% = 314.250 (hogares de 1 miembro)/2.780.237 (hogares totales). La probabilidad de que un hogar en el Ecuador esté consitituído de un miembro es 11,30%, porque expresa la posibilidad de observar eso basándonos en la frecuencia relativa, que a su vez se basa en la frecuencia (o cantidad de veces que ocurre algo); es decir, en qué tan habitual es el evento.

Es indispensable que usted entienda que la probabilidad es una frecuencia relativa. Sino, relea los capítulso hasta aquí antes de seguir. 

Como seguramente ya entendió hasta este momento, la probabilidad está asociada con la distribución de los datos. Prácticamente entender la distribución de los datos es entender la probabilidad de la ocurrencia de los eventos que estamos analizando.

```{admonition} Resumen
:class: important

Hemos aprendido qué es una distribución de datos: la forma en la que estos datos están repartidos. También podríamos pensar en estas distribuciones como las ubicaciones que ocupan los datos de forma conceptual, que puede intuirse de forma gráfica.
Además, qué es la probabilidad: la frecuencia relativa de un evento.
```

En los próximos capítulos profundizaremos en estos conceptos. Por ahora, solo quiero que se quede con la idea de que la probabilidad es una frecuencia relativa y que las distribuciones son la forma en la que se reparten los datos.

En el siguiente capítulo conoceremos algunas distribuciones comunes y útiles, que nos sirven analizar fenómenos aleatorios. Luego de ese, empezaremos a utilizar el cálculo de probabilidades.