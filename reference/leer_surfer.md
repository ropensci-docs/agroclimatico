# Lee escalas de Surfer

Lee archivos en el formato "Level File Format" de Surfer (ver
http://surferhelp.goldensoftware.com/topics/level_file_format.htm).

## Uso

``` r
leer_surfer(archivo, color = c("primario", "secundario"))
```

## Argumentos

- archivo:

  ruta al archivo a laeer.

- color:

  caracter que indica qué color leer. Puede ser "primario" (que
  corresponde a "FFGColor") o "secundario" (que corresponde a
  "FBGColor"). No tiene efecto si el archivo es formato LVL1

## Valor

Si el archivo es LVL1, un vector con los niveles. Si el archivo es LVL2
o LVL3, una lista con elementos:

- `niveles` (numérico), el nivel a que corresopnde cada color.

- `colores` (caracter), la representación hexadecimal del color de cada
  break.

- `paleta` (función), una función que toma un entero `n` y devuelve un
  vector de caracter con `n` colores interpolados a partir de los
  colores de la escala.

## Ejemplos

``` r
escala <- system.file("extdata", "escala_pp_mensual.lvl", package = "agroclimatico")

escala_pp_mensual <- leer_surfer(escala)

# Valores a los que corresponde cada color
escala_pp_mensual$niveles
#>  [1]  -Inf -10.0   0.0   0.1   2.0   5.0  10.0  20.0  30.0  40.0  50.0  75.0
#> [13] 100.0 200.0 300.0 400.0 500.0   Inf

# Ver los colores
scales::show_col(escala_pp_mensual$colores)


# Obtener más colores usando la misma paleta
muchos_colores <- escala_pp_mensual$paleta(25)
scales::show_col(muchos_colores)

```
