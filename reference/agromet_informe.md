# Formato de salida para Informes

Los formatos utilizan como base
[`rmarkdown::pdf_document()`](https://pkgs.rstudio.com/rmarkdown/reference/pdf_document.html)
y una plantilla específica de LaTex.

## Uso

``` r
agromet_informe(..., latex_engine = "xelatex")
```

## Argumentos

- ...:

  cualquier argumento que requiera
  [`rmarkdown::pdf_document()`](https://pkgs.rstudio.com/rmarkdown/reference/pdf_document.html).

- latex_engine:

  Caracter con el compilador de latex a usar.

## Valor

documento compilado.

## Ejemplos

``` r
if (FALSE) { # \dontrun{
agromet_informe("Informe.Rmd")
} # }
```
