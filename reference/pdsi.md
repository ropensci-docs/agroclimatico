# Índice de Severidad de Sequía de Palmer

Calcula el Indice de Severidad de Sequía de Palmer. `psdi_ac()` calcula
la versión autocalibrada.

## Uso

``` r
pdsi(precipitacion, etp, cc = 100, coeficientes = pdsi_coeficientes())

pdsi_ac(precipitacion, etp, cc = 100, coeficientes = pdsi_coeficientes())
```

## Argumentos

- precipitacion:

  serie de precipitación sin datos faltantes (en mm). Ver sección
  Details.

- etp:

  serie de evapotranspiración potencial sin datos faltantes. Ver sección
  Details.

- cc:

  capacidad de campo (en mm).

- coeficientes:

  lista de coeficientes que devuelve
  [`pdsi_coeficientes()`](https://docs.ropensci.org/agroclimatico/reference/pdsi_coeficientes.md)

## Valor

Un vector de la misma longitud que `precipitacion` con el PDSI
correspondiente a cada caso.

## Detalles

El Índice de Severidad de Sequía de Palmer, propuesto por Palmer (1965)
es usado como indicador para cuantificar las condiciones de sequía a
largo plazo. El cálculo usa constantes definidas empíricamente,
originalmente utilizando datos meteorológicos de Kansas y de Iowa en
Estados Unidos. Estas constantes no representan necesariamente cualquier
región del planeta por lo que puede ser redefinidas para el cálculo del
índice usando la función del índice usando la función
[`pdsi_coeficientes()`](https://docs.ropensci.org/agroclimatico/reference/pdsi_coeficientes.md).

Alternativamente, Wells et al. (2004) propuso el Indice de Severidad de
Sequía de Palmer Autocalibrado que tiene la capacidad de ajustar las
constantes empíricas durante el cálculo del indice.

Si bien el cálculo de este indice funcionará para series de datos cortas
(datos diarios para un mes o datos mensuales para un año), es necesario
contar con una climatología, es decir 30 años para que el resultado sea
confiable.

## Referencias

Palmer (1965), Meteorological Drought. U.S Weather Bureau, Washington,
D.C. (book).

Wells et. al. (2004), A Self-Calibrating Palmer Drought Severity Index.
Journal of Climate
[doi:10.1175/1520-0442(2004)017\<2335:ASPDSI\>2.0.CO;2](https://doi.org/10.1175/1520-0442%282004%29017%3C2335%3AASPDSI%3E2.0.CO%3B2)

## Ejemplos

``` r

library(dplyr)

# datos aleatorios
set.seed(42)

datos <- data.frame(fecha = seq(as.Date("1985-01-01"), as.Date("2015-12-01"), by = "1 month"))
datos |>
  mutate(pp = rgamma(nrow(datos), shape = 2, scale = 10),
         etp = rgamma(nrow(datos), shape = 1, scale = 3),
         pdsi_ac = pdsi(pp, etp)) |>
  slice_head(n = 10)
#>         fecha        pp       etp    pdsi_ac
#> 1  1985-01-01 36.489561 4.4884365  0.6035107
#> 2  1985-02-01  8.881098 2.4454927 -0.6361097
#> 3  1985-03-01 15.592198 0.6427609 -0.6008359
#> 4  1985-04-01  4.521825 2.1359691 -1.1479653
#> 5  1985-05-01 13.728401 4.8577625 -1.2702747
#> 6  1985-06-01  8.028043 3.8066111 -1.7626929
#> 7  1985-07-01 49.905627 0.4327422  1.5345299
#> 8  1985-08-01 14.241745 1.6288137 -0.1455719
#> 9  1985-09-01  4.646857 1.4363694 -0.5643165
#> 10 1985-10-01  2.812335 4.3753527 -1.2851817

```
