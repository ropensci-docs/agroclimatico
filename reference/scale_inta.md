# Escalas de colores para precipitación y temperatura

Escalas para `color` y `fill` para variables discretas.

## Uso

``` r
scale_fill_inta(
  escala,
  name = waiver(),
  breaks = waiver(),
  drop = waiver(),
  ...
)

scale_color_inta(
  escala,
  name = waiver(),
  breaks = waiver(),
  drop = waiver(),
  ...
)
```

## Argumentos

- escala:

  escala de colores. Puede ser

  - una lista con elementos `niveles` y `paleta` (ver `[leer_surfer()]`
    y
    [escala_temp_min](https://docs.ropensci.org/agroclimatico/reference/escalas.md)).

  - una función que toma un entero `n` y devuelve un vector de caracter
    con `n` colores interpolados a partir de los colores de la escala.)

- name:

  nombre de la escala.

- breaks:

  niveles de la escala. Si no es
  [`waiver()`](https://ggplot2.tidyverse.org/reference/waiver.html),
  tiene prioridad por sobre los niveles definidos en `escala`.

- drop:

  lógico que indica si se muestran todos los valores o sólo los
  presentes en los datos. Por defecto, es `FALSE` si la escala define
  los niveles usando `breaks` o `escala`.

- ...:

  otros argumentos que se pasan a
  [`ggplot2::scale_fill_manual()`](https://ggplot2.tidyverse.org/reference/scale_manual.html)
  o
  [`ggplot2::discrete_scale()`](https://ggplot2.tidyverse.org/reference/discrete_scale.html).

## Valor

objeto ggproto compatible con ggplot2.

## Ejemplos

``` r
library(ggplot2)
library(dplyr)

pp_enero <- datos_nh_mensual |>
  filter(mes == unique(mes)[1])

# Los contornos llenos requieren que los datos estén en una grilla
# regular, necesitamos hacer una interpolación con kriging.
with(pp_enero, agroclimatico:::kringe(precipitacion_mensual, lon, lat)) |>
ggplot(aes(lon, lat)) +
 geom_contour(aes(z = var1.pred)) +
 geom_contour_filled(aes(z = var1.pred)) +
 scale_fill_inta(escala = escala_pp_mensual)
#> [using ordinary kriging]

```
