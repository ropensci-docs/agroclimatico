# Escalas de colores usadas por el INTA

Escalas de colores típicas usadas por INTA para distintas variables.

## Uso

``` r
escala_temp_min

escala_temp_max

escala_pp_mensual

escala_pp_diaria
```

## Formato

Objeto tipo lista con 3 elementos.

## Valor

Lista en el mismo formato que devuelve
[`leer_surfer()`](https://docs.ropensci.org/agroclimatico/reference/leer_surfer.md)
con elementos:

- `niveles` (numérico), el nivel a que corresopnde cada color.

- `colores` (caracter), la representación hexadecimal del color de cada
  break.

- `paleta` (función), una función que toma un entero `n` y devuelve un
  vector de caracter con `n` colores interpolados a partir de los
  colores de la escala.

## Ejemplos

``` r

library(ggplot2)
library(dplyr)

pp_enero <- datos_nh_mensual |>
  filter(mes == unique(mes)[1])

# En el contexto de la función mapear():
mapear(pp_enero, precipitacion_mensual, lon, lat,
escala = escala_pp_mensual, cordillera = TRUE)


# Con ggplot2
# Los contornos llenos requieren que los datos estén en una grilla
# regular, necesitamos hacer una interpolación con kriging.
with(pp_enero, agroclimatico:::kringe(precipitacion_mensual, lon, lat)) |>
ggplot(aes(lon, lat)) +
 geom_contour(aes(z = var1.pred)) +
 geom_contour_filled(aes(z = var1.pred)) +
 scale_fill_inta(escala = escala_pp_mensual)
#> [using ordinary kriging]

```
