# Días Promedio

Calcula el primer y último día del año promedio a partir de una serie de
fechas.

## Uso

``` r
dias_promedio(fechas)
```

## Argumentos

- fechas:

  vector de fechas

## Valor

La función devuelve un data.frame con 4 variables fijas y variables
extras en el caso de hacer el cálculo para distintos grupos:

- `variable` (caracter) primer_dia o ultimo_dia según corresponda

- `dia` (numérico) día del mes

- `mes` (numérico) mes de ocurrencia

- `dia_juliano` (numérico) día del año

## Detalles

Esta función solo requiere un vector de fechas para calcular el primer y
último día del año en promedio. Si este vector incluye todos los días de
muchos años el resultado será el 1° de enero y el 31 de diciembre. Pero
si solo se utilizan las fechas que cumplen con una determinada
condición, por ejemplo aquellos días donde la temperatura mínima fue
menor o igual a 0°C, entonces devuelve el primer y último día de
ocurrencia en promedio para este evento.

La función se puede usar tanto con la sintaxis de base como con dplyr
(ver ejemplos). En el caso de dplyr es necesario usar la función
[`dplyr::reframe()`](https://dplyr.tidyverse.org/reference/reframe.html)
ya que `dias_promedio()` devuelve un data.frame. Es posible hacer
cálculos agrupando datos con
[`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html).

## Ejemplos

``` r
data(NH0358)

# Usando la serie completa
dias_promedio(NH0358$fecha)
#>      variable   dia   mes dia_juliano
#>        <fctr> <int> <int>       <int>
#> 1: primer_dia     1     1           1
#> 2: ultimo_dia    31    12         365

# Filtrando los datos para un determinado evento
library(dplyr)
NH0358 %>%
  filter(t_min <= 0) %>%
  reframe(dias_promedio(fecha))
#>     variable dia mes dia_juliano
#> 1 primer_dia  28   5         148
#> 2 ultimo_dia  31   8         243

# Por grupos, si tenemos por ejemplo más de una estación
data(NH0114)

rbind(NH0358, NH0114) %>%
  filter(t_min <= 0) %>%
  group_by(codigo_nh) %>%
  reframe(dias_promedio(fecha))
#> # A tibble: 4 × 5
#>   codigo_nh variable     dia   mes dia_juliano
#>   <chr>     <fct>      <int> <int>       <int>
#> 1 0114      primer_dia    30     6         181
#> 2 0114      ultimo_dia     7     8         219
#> 3 0358      primer_dia    28     5         148
#> 4 0358      ultimo_dia    31     8         243
```
