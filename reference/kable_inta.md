# Formatea tablas con el estilo de INTA

Llama a
[`kableExtra::kbl()`](https://rdrr.io/pkg/kableExtra/man/kbl.html) con
valores por defecto apropiados acordes al estilo utilizado por INTA.

## Uso

``` r
kable_inta(x, ...)
```

## Argumentos

- x:

  Una tabla.

- ...:

  Otros argumentos que se pasan a
  [`kableExtra::kbl()`](https://rdrr.io/pkg/kableExtra/man/kbl.html)

## Valor

tabla, objeto kbl.

## Ejemplos

``` r

library(dplyr)
library(kableExtra)
#> 
#> Adjuntando el paquete: ‘kableExtra’
#> The following object is masked from ‘package:dplyr’:
#> 
#>     group_rows
metadatos <- metadatos_nh()

metadatos %>%
 head() %>%
 select(codigo_nh, estacion) %>%
 kable_inta(caption = "Ejemplo",
           col.names = c("Código", "Estación")) %>%
 kable_styling(latex_options = "scale_down")
#> <table class="table" style="margin-left: auto; margin-right: auto;">
#> <caption>Ejemplo</caption>
#>  <thead>
#>   <tr>
#>    <th style="text-align:left;"> Código </th>
#>    <th style="text-align:left;"> Estación </th>
#>   </tr>
#>  </thead>
#> <tbody>
#>   <tr>
#>    <td style="text-align:left;"> 0446 </td>
#>    <td style="text-align:left;"> Anguil </td>
#>   </tr>
#>   <tr>
#>    <td style="text-align:left;"> 0196 </td>
#>    <td style="text-align:left;"> Azul </td>
#>   </tr>
#>   <tr>
#>    <td style="text-align:left;"> 0221 </td>
#>    <td style="text-align:left;"> Bahía Blanca </td>
#>   </tr>
#>   <tr>
#>    <td style="text-align:left;"> 0400 </td>
#>    <td style="text-align:left;"> Balcarce </td>
#>   </tr>
#>   <tr>
#>    <td style="text-align:left;"> 0323 </td>
#>    <td style="text-align:left;"> Bariloche </td>
#>   </tr>
#>   <tr>
#>    <td style="text-align:left;"> 0216 </td>
#>    <td style="text-align:left;"> Barrow </td>
#>   </tr>
#> </tbody>
#> </table>
```
