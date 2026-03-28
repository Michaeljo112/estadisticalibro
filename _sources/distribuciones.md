---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Mirar los datos

En el capítulo anterior analizamos la pobreza parroquial de Ecuador. Elegimos un mapa un indicador de pobreza que construímos. Presentamos los datos de forma gráfica, a esto le decimos "graficar". Hay varias formas de graficar. En este caso, usamos un mapa para graficar la pobreza parroquial de Ecuador. Un mapa que variaba la intensidad de color según el valor del indicador. Más rojo, más pobreza. Este tipo de mapas que usamos se llama "mapa de calor". Pero hay más de una forma de dibujar los datos. Usemos otra.


```{code-cell} python
:tags: [thebe]

import pandas as pd

url = "https://raw.githubusercontent.com/Michaeljo112/Estimando-la-pobreza-parroquial/main/datos22.xlsx"

df = pd.read_excel(url, sheet_name='data', index_col=None)

df.head()
```