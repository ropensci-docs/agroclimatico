# Completa una Serie de Datos

La función permite completar una serie de datos temporales definiendo
alguna resolución disponible. Es compatible con datos agrupados por
[`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html).

## Uso

``` r
completar_serie(datos, fecha, resolucion, rango = range(fecha))
```

## Argumentos

- datos:

  tabla (data.frame, data.table, tibble) a completar.

- fecha:

  variable tipo fecha (Date, IDate, POSIXct, etc).

- resolucion:

  texto que define resolución de salida de los datos. Puede ser
  cualquier valor aceptado por el argumento `by` de la función
  [`seq.Date()`](https://rdrr.io/r/base/seq.Date.html) o su traducción
  al español. Es decir, "día" (o "dia"), "semana", "mes", "trimestre" o
  "año", así como los plurales.

- rango:

  un vector cuyo rango define el período a completar. Es útil si se
  quiere que múltiples grupos de datos tengan el mismo rango de fechas.
  Es posible definir un rango por fuera del rango original de los datos
  para homogeneizar series temporales.

## Valor

Devuelve un data.frame con las mismas variables de origen. La variable
asociada a las fechas ahora se encuentra completa para la resolución
indicada y el resto de las variables se completan con NA.

## Ejemplos

``` r
# Datos de prueba completos
datos <- data.frame(fechas = seq(as.Date("2013-01-01"), as.Date("2015-12-01"),
                             by = "1 month"),
                    pp = 1)

set.seed(42)
datos_perdidos <- sample(nrow(datos), nrow(datos)/10)
datos$pp[datos_perdidos] <- NA
datos_incompletos <- na.omit(datos) #Serie de datos a completar

completar_serie(datos_incompletos, fechas, resolucion = "1 mes")
#>        fechas pp
#> 1  2013-02-01  1
#> 2  2013-03-01  1
#> 3  2013-04-01  1
#> 4  2013-05-01  1
#> 5  2013-06-01  1
#> 6  2013-07-01  1
#> 7  2013-08-01  1
#> 8  2013-09-01  1
#> 9  2013-10-01 NA
#> 10 2013-11-01  1
#> 11 2013-12-01  1
#> 12 2014-01-01  1
#> 13 2014-02-01  1
#> 14 2014-03-01  1
#> 15 2014-04-01  1
#> 16 2014-05-01  1
#> 17 2014-06-01  1
#> 18 2014-07-01  1
#> 19 2014-08-01  1
#> 20 2014-09-01  1
#> 21 2014-10-01  1
#> 22 2014-11-01  1
#> 23 2014-12-01  1
#> 24 2015-01-01 NA
#> 25 2015-02-01  1
#> 26 2015-03-01  1
#> 27 2015-04-01  1
#> 28 2015-05-01  1
#> 29 2015-06-01  1
#> 30 2015-07-01  1
#> 31 2015-08-01  1
#> 32 2015-09-01  1
#> 33 2015-10-01  1
#> 34 2015-11-01  1
#> 35 2015-12-01  1
```
