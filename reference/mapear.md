# Grafica variables en Argentina

Dadas mediciones de una variable en puntos ubicados en Argentina,
interpola al resto del territorio usando kriging y grafica con
contornos. Las funciones secundarias `coord_argentina()` y
`theme_inta_mapa()` permiten generar un mapa en la región de Argentina
(definida por `xlim` y `ylim`) con el estilo específico usando por INTA.

## Uso

``` r
mapear(
  data,
  valor,
  lon,
  lat,
  breaks = waiver(),
  escala = scales::viridis_pal(),
  cordillera = FALSE,
  variable = NULL,
  titulo = NULL,
  subtitulo = NULL,
  fuente = NULL
)

coord_argentina(xlim = c(-77, -50), ylim = c(-57, -20), ...)

theme_inta_mapa(...)
```

## Argumentos

- data:

  data.frame o similar con las variables a utilizar.

- valor:

  vector con los valores medidos.

- lon, lat:

  vectores de ubicación en longitud y latitud.

- breaks:

  vector numérico que define para que valores se graficará los
  contornos. Si es`NULL` hace 10 contornos calculados a partir el rango
  de los datos.

- escala:

  paleta de colores a usar. Tiene que ser una función que reciba un
  número y devuelva esa cantidad de colores. Por ejemplo
  [escala_temp_min](https://docs.ropensci.org/agroclimatico/reference/escalas.md).

- cordillera:

  valor lógico indicando si hay que tapar los datos donde está la
  cordillera (donde el kriging es particularmente problemático). Si es
  `TRUE` pinta con gris donde la altura de la topografía es mayor a
  1500 m. También puede ser un número, indicando el valor mínimo desde
  donde empezar a graficar la cordillera.

- titulo, subtitulo, fuente, variable:

  texto para usar como título, subtítulo, epígrafe y nombre de la
  leyenda.

- xlim, ylim:

  límites en longitud y latitud.

- ...:

  otros argumentos que se pasan a
  [`ggplot2::coord_sf()`](https://ggplot2.tidyverse.org/reference/ggsf.html)
  o
  [`ggplot2::theme_linedraw()`](https://ggplot2.tidyverse.org/reference/ggtheme.html).

## Valor

Un objeto ggplot2.

## Ejemplos

``` r
if (FALSE) { # \dontrun{

library(dplyr)

data(datos_nh_mensual)

abril <- datos_nh_mensual %>%
  filter(mes == unique(mes)[4]) #datos del cuarto mes en la base, abril.

abril %>%
  mapear(precipitacion_mensual, lon, lat, cordillera = TRUE,
              escala = escala_pp_mensual,
              titulo = "Precipitación en abril de 2019",
              fuente = "Fuente: INTA",
              variable = "pp")
} # }
```
