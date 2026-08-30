# Olas

Identifica periodos de persistencia de un evento definido a partir de
alguna condición lógica, por ejemplo días consecutivos donde la
temperatura mínima fue igual o menor a 0°C para calcular días acumulados
de heladas.

## Uso

``` r
olas(fecha, ..., remplaza.na = FALSE)
```

## Argumentos

- fecha:

  vector de fechas, la serie temporal debe estar completa, sin datos
  faltantes implicitos.

- ...:

  umbral o umbrales a calcular utilizando operadores lógicos.

- remplaza.na:

  lógico. Por defecto es FALSE, es decír que si la función encuentra un
  dato faltante "corta" la ola o periodo de persitencia. Si es TRUE, la
  función reemplaza cada NA por el valor previo en la serie, por lo
  tanto la ola no se interrumpe si hay NAs.

## Valor

Devuelve un data.frame con 3 variables fijas y las posibles variables
asociadas al agrupamiento:

- `ola` (caracter) nombre de la ola definido por el usuario (si los
  argumentos de `...` no tienen nombre, se usa `V1`, `V2`, etc...)

- `inicio` (fecha) fecha de inicio de la ola o periodo de persistencia

- `fin` (fecha) fecha de finalización de la ola o periodo de
  persistencia

- `duracion` (diferencia de fechas, tipo drtn) duración de la ola

Si una ola todavía no terminó, fin y longitud son NA.

## Detalles

La función Puede utilizarse en el contexto de
[`dplyr::summarise()`](https://dplyr.tidyverse.org/reference/summarise.html)
y
[`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html)
para hacer este cálculo por grupos.

## Ejemplos

``` r
data(NH0358)

library(dplyr)
NH0358 %>%
  reframe(olas(fecha, calor = t_max > 20)) %>%
  slice_head(n = 10)
#>      ola     inicio        fin duracion
#> 1  calor 1951-01-01 1951-01-22  22 days
#> 2  calor 1951-01-24 1951-02-13  21 days
#> 3  calor 1951-02-15 1951-03-31  45 days
#> 4  calor 1951-04-04 1951-04-09   6 days
#> 5  calor 1951-04-15 1951-04-20   6 days
#> 6  calor 1951-04-22 1951-04-24   3 days
#> 7  calor 1951-04-26 1951-04-29   4 days
#> 8  calor 1951-05-01 1951-05-06   6 days
#> 9  calor 1951-05-10 1951-05-13   4 days
#> 10 calor 1951-05-22 1951-05-22   1 days

NH0358 %>%
  reframe(olas(fecha, frio = t_min <= 0)) %>%
  slice_head(n = 10)
#>     ola     inicio        fin duracion
#> 1  frio 1951-06-06 1951-06-06   1 days
#> 2  frio 1951-06-26 1951-06-28   3 days
#> 3  frio 1951-06-30 1951-06-30   1 days
#> 4  frio 1951-07-02 1951-07-02   1 days
#> 5  frio 1951-07-06 1951-07-07   2 days
#> 6  frio 1951-07-31 1951-07-31   1 days
#> 7  frio 1951-08-03 1951-08-03   1 days
#> 8  frio 1951-08-05 1951-08-05   1 days
#> 9  frio 1951-08-15 1951-08-15   1 days
#> 10 frio 1951-08-28 1951-08-28   1 days
```
