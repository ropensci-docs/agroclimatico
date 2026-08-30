# Transformaciones estadísticas de variables

Las funciones `decil()` y `anomalia_porcentual()` devuelven estos
estadísticos para alguna variable dado un periodo de referencia
especificado.

## Uso

``` r
decil(variable, referencia = rep(TRUE, length(variable)))

anomalia_porcentual(
  variable,
  referencia = rep(TRUE, length(variable)),
  na.rm = FALSE
)
```

## Argumentos

- variable:

  vector de observaciones de la variable de interés.

- referencia:

  serie de observaciones para usar de referencia en el ajuste a la
  distribución teórica. Puede ser:

  - vector lógico que se usará para filtrar los datos de entrada.

  - vector numérico de observaciones.

  - la serie completa (opción por defecto).

- na.rm:

  lógico. Define si se utilizan o no valores faltantes en el cálculo de
  la anomalía porcentual.

## Valor

Para el cálculo de los deciles, devuelve un vector numérico con el decil
asociado a cada valor de la variable. En este caso la columna `deciles`
es de tipo doble ya que devuelve el valor exacto del decil sin
redondeos. Para el cálculo de la anomalía porcentual también devuelve un
vector numérico. Las funciones son compatibles con
[`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html)
y
[`dplyr::mutate()`](https://dplyr.tidyverse.org/reference/mutate.html).

## Detalles

Para recuperar el valor de la variable asociado a determinado decil se
puede utilizar la función
[`stats::quantile()`](https://rdrr.io/r/stats/quantile.html).

## Ejemplos

``` r
library(dplyr)
#> 
#> Adjuntando el paquete: ‘dplyr’
#> The following objects are masked from ‘package:stats’:
#> 
#>     filter, lag
#> The following objects are masked from ‘package:base’:
#> 
#>     intersect, setdiff, setequal, union
data(NH0358)

# Deciles de precipitación usando como referencia la serie completa
NH0358 %>%
  mutate(deciles = decil(precip)) %>%
  slice_head(n = 10)
#>    codigo codigo_nh      fecha t_max t_min precip lluvia_datos lluvia llovizna
#> 1       5      0358 1951-01-01  29.2   8.2    0.0            0     NA       NA
#> 2       5      0358 1951-01-02  31.3  17.4    0.0            0     NA       NA
#> 3       5      0358 1951-01-03  30.9  18.3    0.0            0     NA       NA
#> 4       5      0358 1951-01-04  32.9  20.1    5.2            1     NA       NA
#> 5       5      0358 1951-01-05  32.6  18.4    0.0            0     NA       NA
#> 6       5      0358 1951-01-06  30.4  10.3    0.0            0     NA       NA
#> 7       5      0358 1951-01-07  29.1  13.8    0.0            0     NA       NA
#> 8       5      0358 1951-01-08  31.4  16.4    0.0            0     NA       NA
#> 9       5      0358 1951-01-09  30.6  19.6    8.1            1     NA       NA
#> 10      5      0358 1951-01-10  28.4  16.9    9.2            1     NA       NA
#>    granizo nieve t_aire_max t_aire_min t_suelo_max t_suelo_min heliofania_efec
#> 1       NA    NA         NA         NA          NA          NA              NA
#> 2       NA    NA         NA         NA          NA          NA              NA
#> 3       NA    NA         NA         NA          NA          NA              NA
#> 4       NA    NA         NA         NA          NA          NA              NA
#> 5       NA    NA         NA         NA          NA          NA              NA
#> 6       NA    NA         NA         NA          NA          NA              NA
#> 7       NA    NA         NA         NA          NA          NA              NA
#> 8       NA    NA         NA         NA          NA          NA              NA
#> 9       NA    NA         NA         NA          NA          NA              NA
#> 10      NA    NA         NA         NA          NA          NA              NA
#>    heliofania_rel p_vapor hr td rocio viento_10m viento_2m rad etp  deciles
#> 1              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 2              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 3              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 4              NA      NA NA NA    NA         NA        NA  NA  NA 8.780583
#> 5              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 6              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 7              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 8              NA      NA NA NA    NA         NA        NA  NA  NA 7.634097
#> 9              NA      NA NA NA    NA         NA        NA  NA  NA 9.012704
#> 10             NA      NA NA NA    NA         NA        NA  NA  NA 9.082497

# Deciles mensuales
precip_mensual <- NH0358 %>%
  group_by(fecha = lubridate::floor_date(fecha, "month")) %>%
  summarise(precip = sum(precip, na.rm = TRUE))

precip_mensual %>%
  mutate(deciles = decil(precip))
#> # A tibble: 839 × 3
#>    fecha      precip deciles
#>    <date>      <dbl>   <dbl>
#>  1 1951-01-01   85.2   6.00 
#>  2 1951-02-01  156.    8.64 
#>  3 1951-03-01   32.1   1.91 
#>  4 1951-04-01   43.6   2.87 
#>  5 1951-05-01  243.    9.74 
#>  6 1951-06-01   27.2   1.60 
#>  7 1951-07-01    1.4   0.119
#>  8 1951-08-01   88     6.25 
#>  9 1951-09-01   25.3   1.45 
#> 10 1951-10-01   37     2.42 
#> # ℹ 829 more rows

# Deciles definiendo un periodo de referencia
precip_mensual %>%
  mutate(deciles = decil(precip,
                         referencia = lubridate::year(fecha) <= 1958))
#> # A tibble: 839 × 3
#>    fecha      precip deciles
#>    <date>      <dbl>   <dbl>
#>  1 1951-01-01   85.2   6.88 
#>  2 1951-02-01  156.    8.75 
#>  3 1951-03-01   32.1   2.19 
#>  4 1951-04-01   43.6   3.33 
#>  5 1951-05-01  243.    9.90 
#>  6 1951-06-01   27.2   1.56 
#>  7 1951-07-01    1.4   0.104
#>  8 1951-08-01   88     6.98 
#>  9 1951-09-01   25.3   1.35 
#> 10 1951-10-01   37     3.02 
#> # ℹ 829 more rows

# Anomalia porcentual usando como referencia la serie completa
NH0358 %>%
  mutate(anomalia = anomalia_porcentual(precip)) %>%
  slice_head(n = 10)
#>    codigo codigo_nh      fecha t_max t_min precip lluvia_datos lluvia llovizna
#> 1       5      0358 1951-01-01  29.2   8.2    0.0            0     NA       NA
#> 2       5      0358 1951-01-02  31.3  17.4    0.0            0     NA       NA
#> 3       5      0358 1951-01-03  30.9  18.3    0.0            0     NA       NA
#> 4       5      0358 1951-01-04  32.9  20.1    5.2            1     NA       NA
#> 5       5      0358 1951-01-05  32.6  18.4    0.0            0     NA       NA
#> 6       5      0358 1951-01-06  30.4  10.3    0.0            0     NA       NA
#> 7       5      0358 1951-01-07  29.1  13.8    0.0            0     NA       NA
#> 8       5      0358 1951-01-08  31.4  16.4    0.0            0     NA       NA
#> 9       5      0358 1951-01-09  30.6  19.6    8.1            1     NA       NA
#> 10      5      0358 1951-01-10  28.4  16.9    9.2            1     NA       NA
#>    granizo nieve t_aire_max t_aire_min t_suelo_max t_suelo_min heliofania_efec
#> 1       NA    NA         NA         NA          NA          NA              NA
#> 2       NA    NA         NA         NA          NA          NA              NA
#> 3       NA    NA         NA         NA          NA          NA              NA
#> 4       NA    NA         NA         NA          NA          NA              NA
#> 5       NA    NA         NA         NA          NA          NA              NA
#> 6       NA    NA         NA         NA          NA          NA              NA
#> 7       NA    NA         NA         NA          NA          NA              NA
#> 8       NA    NA         NA         NA          NA          NA              NA
#> 9       NA    NA         NA         NA          NA          NA              NA
#> 10      NA    NA         NA         NA          NA          NA              NA
#>    heliofania_rel p_vapor hr td rocio viento_10m viento_2m rad etp anomalia
#> 1              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 2              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 3              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 4              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 5              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 6              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 7              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 8              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 9              NA      NA NA NA    NA         NA        NA  NA  NA       NA
#> 10             NA      NA NA NA    NA         NA        NA  NA  NA       NA

#  Anomalia porcentual definiendo un periodo de referencia
precip_mensual %>%
  mutate(deciles = anomalia_porcentual(precip,
                         referencia = lubridate::year(fecha) <= 1958))
#> # A tibble: 839 × 3
#>    fecha      precip deciles
#>    <date>      <dbl>   <dbl>
#>  1 1951-01-01   85.2   0.100
#>  2 1951-02-01  156.    1.02 
#>  3 1951-03-01   32.1  -0.585
#>  4 1951-04-01   43.6  -0.437
#>  5 1951-05-01  243.    2.14 
#>  6 1951-06-01   27.2  -0.649
#>  7 1951-07-01    1.4  -0.982
#>  8 1951-08-01   88     0.137
#>  9 1951-09-01   25.3  -0.673
#> 10 1951-10-01   37    -0.522
#> # ℹ 829 more rows
```
