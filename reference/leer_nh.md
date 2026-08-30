# Lectura de Archivos con Formato NH

Lee uno o más archivos siempre que mantengan el formato NH de ancho
fijo.

## Uso

``` r
leer_nh(archivos)
```

## Argumentos

- archivos:

  Caracter o vector de caracteres con nombre y ubicación de los archivos
  a leer.

## Valor

Devuelve un data.frame con tantas filas como líneas en el o los archivos
leidos y las 25 variables presentes.

## Detalles

La función está preparada para leer datos diarios con el formato NH que
incluye 25 variables:

- `codigo` (caracter)

- `codigo_nh` (caracter), variable llave para acceder a los metadatos de
  estaciones

- `fecha` (fecha)

- `t_max` (numérico), temperatura máxima en grados centígrados

- `t_min` (numérico), temperatura mínima en grados centígrados

- `precip` (numérico), precipitación acumulada en milímetros

- `lluvia_datos` (numérico), ocurrencia de precipitación 1 indica lluvia

- `lluvia` (numérico), ocurrencia de lluvia

- `llovizna` (numérico), ocurrencia de llovizna

- `granizo` (numérico), ocurrencia de granizo

- `nieve` (numérico), ocurrencia de nieve

- `t_min_5cm` (numérico), temperatura mínima a intemperie a 5cm en
  grados centígrados

- `t_min_50cm` (numérico), temperatura mínima a intemperie a 50cm en
  grados centígrados

- `t_suelo_5cm` (numérico), temperatura media del suelo a 5cm en grados
  centígrados

- `t_suelo_10cm` (numérico), temperatura media del suelo a 10cm en
  grados centígrados

- `heliofania_efec` (numérico), heliofanía efectiva en horas

- `heliofania_rel` (numérico), heliofanía relativa en porcentaje

- `p_vapor` (numérico), tensión de vapor en hPa

- `hr` (numérico), humedad relativa en porcentaje

- `td` (numérico), temperatura de rocío en grados centígrados

- `rocio` (numérico), ocurrencia de rocío

- `viento_10m` (numérico), viento a 10 metros en km/h

- `viento_2m` (numérico), viento a 2 metros en km/h

- `rad` (numérico), radiación en MJ/m2

- `etp` (numérico), evapotranspiración en milímetros

## Ver también

[`metadatos_nh()`](https://docs.ropensci.org/agroclimatico/reference/metadatos_nh.md)
devuelve los metadatos de las estaciones meteorológicas.

## Ejemplos

``` r
archivo <- system.file("extdata", "NH0358.DAT", package = "agroclimatico")
datos <- leer_nh(archivo)
```
