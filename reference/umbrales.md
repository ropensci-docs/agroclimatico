# Calcula la Ocurrencia de eventos a Partir de Umbrales

La función `umbrales()` permite contar la ocurrencia de eventos
definidos a partir de uno o más umbrales.

## Uso

``` r
umbrales(...)
```

## Argumentos

- ...:

  umbral o umbrales a calcular utilizando operadores lógicos.

## Valor

La función devuelve un data.frame con 4 variables fijas junto a posibles
variables asociadas a los agrupamientos.

Variables fijas

- `extremo` (caracter) nombre del extremo definido por el usuario (si
  los argumentos de `...` no tienen nombre, se usa `V1`, `V2`, etc...)

- `N` (numérico) ocurrencia del evento

- `prop` (numérico) proporción de eventos respecto del total de
  observaciones

- `na` (numérico) proporción de datos faltantes respecto del total de
  observaciones

## Detalles

Debe utilizarse en el contexto de
[`dplyr::summarise()`](https://dplyr.tidyverse.org/reference/summarise.html)
y opcionalmente
[`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html).
Esto permite calcular distintos umbrales y obtener resultados para
distintos grupos.

## Ejemplos

``` r
data(NH0358)
library(dplyr)

# Sin agrupar devuelve un único valor
NH0358 %>%
 summarise(umbrales(t_30 = t_max >= 30))
#>   extremo    N      prop          na
#> 1    t_30 3389 0.1330376 0.001606898

# Si se agrupan los datos devuelve un valor por cada grupo
NH0358 %>%
  group_by(fecha = lubridate::floor_date(fecha, "1 month")) %>%
  summarise(umbrales(t_30 = t_max >= 30))
#> # A tibble: 839 × 5
#>    fecha      extremo     N   prop    na
#>    <date>     <chr>   <int>  <dbl> <dbl>
#>  1 1951-01-01 t_30       21 0.677      0
#>  2 1951-02-01 t_30        5 0.179      0
#>  3 1951-03-01 t_30        4 0.129      0
#>  4 1951-04-01 t_30        1 0.0333     0
#>  5 1951-05-01 t_30        0 0          0
#>  6 1951-06-01 t_30        0 0          0
#>  7 1951-07-01 t_30        0 0          0
#>  8 1951-08-01 t_30        0 0          0
#>  9 1951-09-01 t_30        2 0.0667     0
#> 10 1951-10-01 t_30        0 0          0
#> # ℹ 829 more rows

# Se pueden calcular varios umbrales al mismo tiempo
NH0358 %>%
 reframe(umbrales(t_30 = t_max >= 30,
                    t_0  = t_min <= 0))
#>   extremo    N       prop          na
#> 1    t_30 3389 0.13303761 0.001606898
#> 2     t_0  914 0.03588254 0.001685283
```
