# Calcula el SPI

Calcula el Índice Estandarizado de Precipitación para distintas escalas.
Las funciones `spi_indice` y `spei_indice` usan internamente a la
función [SPEI::spi](https://rdrr.io/pkg/SPEI/man/Drought-indices.html)
pero tienen la ventaja de devolver el resultado como un data.frame que
se puede usar de manera directa para el análisis de datos con dplyr.

## Uso

``` r
spi_indice(
  fecha,
  precipitacion,
  escalas,
  referencia = rep(TRUE, length(fecha)),
  distribucion = "Gamma",
  ...
)

spei_indice(fecha, balance, escalas, distribucion = "log-Logistic", ...)

spi_referencia(fecha, precipitacion)
```

## Argumentos

- fecha:

  vector de fechas.

- precipitacion:

  vector de precipitacion.

- escalas:

  vector numérico con las escalas requeridas. La unidad de la escala
  está dada por el vector de fechas. Si `escalas = 6` y los datos son
  mensuales entonces el cálculo del indice se hará en escalas de 6
  meses.

- referencia:

  serie de precipitación para usar de referencia en el ajuste a la
  distribución teórica. Puede ser:

  - vector lógico o numérico que se usará para filtrar los datos de
    entrada.

  - un data frame con columna `fecha` y `precipitacion`. La función
    `spi_referencia()` es un simple wrapper a
    [`data.frame()`](https://rdrr.io/r/base/data.frame.html) que le pone
    el nombre correcto a las variables.

- distribucion:

  distribución usada para ajustar los datos.

- ...:

  argumentos pasados a
  [SPEI::spi](https://rdrr.io/pkg/SPEI/man/Drought-indices.html)

- balance:

  balance entre precipitación y evapotranspiración potencial.

## Valor

Un data.frame con columnas

- `fecha` (fecha)

- `escala` (numérico) definidas en el argumento de entrada

- `spi` o `spei` (numérico)

## Detalles

La función `spi_indice` toma valores de precipitación mientras que
`spei_indice` toma valores del balance entre precipitación y
evapotranspiración potencial. Internamente hacen lo mismo; la única
diferencia es la distribución teórica usada por defecto para ajustar los
datos.

## Referencias

Vicente-Serrano, S. M., Beguería, S. and López-Moreno, J. I.: A
multiscalar drought index sensitive to global warming: The standardized
precipitation evapotranspiration index, J. Clim., 23(7),
[doi:10.1175/2009JCLI2909.1](https://doi.org/10.1175/2009JCLI2909.1) ,
2010.

R Package [SPEI: Calculation of the Standardized
Precipitation-Evapotranspiration
Index](https://cran.r-project.org/package=SPEI)

## Ejemplos

``` r

library(dplyr)
data(NH0358)

datos_mensuales <- NH0358 %>%
  group_by(fecha = lubridate::round_date(fecha, "month")) %>%
  reframe(precip = mean(precip, na.rm = TRUE),
          etp = mean(etp, na.rm = TRUE))

# Para escalas de 1 a 12 meses
datos_mensuales %>%
  reframe(spi_indice(fecha, precip, escalas = 1:12)) %>%
  slice_head(n = 10)
#> # A tibble: 10 × 3
#>    fecha      escala    spi
#>    <date>      <dbl>  <dbl>
#>  1 1951-01-01      1 -0.831
#>  2 1951-02-01      1  0.384
#>  3 1951-03-01      1  0.192
#>  4 1951-04-01      1 -0.567
#>  5 1951-05-01      1  1.80 
#>  6 1951-06-01      1 -1.07 
#>  7 1951-07-01      1 -0.636
#>  8 1951-08-01      1  0.549
#>  9 1951-09-01      1 -0.439
#> 10 1951-10-01      1 -1.07 

# Si tenemos nuevos datos y hay que calcular el spi nuevamente pero sin que
# cambien los valores previos, hay que usar `referencia`, por ejemplo usando
# los datos desde el comienzo de la seria hasta 2016

# Usando un vector lógico
datos_mensuales %>%
  reframe(spi_indice(fecha, precip, escalas = 1:12,
                     referencia = data.table::year(fecha) < 2016)) %>%
  slice_head(n = 10)
#> # A tibble: 10 × 3
#>    fecha      escala    spi
#>    <date>      <dbl>  <dbl>
#>  1 1951-01-01      1 -0.818
#>  2 1951-02-01      1  0.340
#>  3 1951-03-01      1  0.208
#>  4 1951-04-01      1 -0.609
#>  5 1951-05-01      1  1.86 
#>  6 1951-06-01      1 -1.10 
#>  7 1951-07-01      1 -0.601
#>  8 1951-08-01      1  0.532
#>  9 1951-09-01      1 -0.427
#> 10 1951-10-01      1 -1.04 

# O un data.frame
datos_2016 <- datos_mensuales %>%
 filter(data.table::year(fecha) < 2016)

datos_mensuales %>%
reframe(spi_indice(fecha, precip, escalas = 1:12,
                   referencia = spi_referencia(datos_2016$fecha, datos_2016$precip))) %>%
  slice_head(n = 10)
#> # A tibble: 10 × 3
#>    fecha      escala    spi
#>    <date>      <dbl>  <dbl>
#>  1 1951-01-01      1 -0.818
#>  2 1951-02-01      1  0.340
#>  3 1951-03-01      1  0.208
#>  4 1951-04-01      1 -0.609
#>  5 1951-05-01      1  1.86 
#>  6 1951-06-01      1 -1.10 
#>  7 1951-07-01      1 -0.601
#>  8 1951-08-01      1  0.532
#>  9 1951-09-01      1 -0.427
#> 10 1951-10-01      1 -1.04 

```
