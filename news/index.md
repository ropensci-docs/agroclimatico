# Registro de cambios

## agroclimatico 1.1.0

### 05/12/2024

El paquete pasá la revisión de rOpenSci, cambia la versión a 1.1.0

### 26/11/2024- [Revisión para rOpenSci, 2](https://github.com/ropensci/software-review/issues/599)

- Mejora en ejemplos de:
  [`decil()`](https://docs.ropensci.org/agroclimatico/reference/decil.md),
  [`anomalia_porcentual()`](https://docs.ropensci.org/agroclimatico/reference/decil.md),
  [`olas()`](https://docs.ropensci.org/agroclimatico/reference/olas.md).

- Mejoras en la documentación de:
  [`pdsi()`](https://docs.ropensci.org/agroclimatico/reference/pdsi.md),
  [`spi_indice()`](https://docs.ropensci.org/agroclimatico/reference/spi_indice.md).

### 29/07/2024- [Revisión para rOpenSci, 2](https://github.com/ropensci/software-review/issues/599)

- Mejora ejemplos en:
  [`ith()`](https://docs.ropensci.org/agroclimatico/reference/ith.md),
  [`spi_indice()`](https://docs.ropensci.org/agroclimatico/reference/spi_indice.md),
  [`pdsi()`](https://docs.ropensci.org/agroclimatico/reference/pdsi.md),
  [`umbrales()`](https://docs.ropensci.org/agroclimatico/reference/umbrales.md)

- Resuelve bug en
  [`olas()`](https://docs.ropensci.org/agroclimatico/reference/olas.md)
  cuando la serie no está completa

- Agrega argumento `remplaza.na` a la función
  [`olas()`](https://docs.ropensci.org/agroclimatico/reference/olas.md)
  para remplazar `NA`s e incluirlos en la ola.

### 29/05/2024 - [Revisión para rOpenSci](https://github.com/ropensci/software-review/issues/599)

- Mejora la documentación de casi todas las funciones:

  - Ahora hay menos errores de tipeo
  - Hay más ejemplos con datos reales
  - Referencias a papers y fuentes de información

- Agrega datos de una segunda estación meteorológica para calculos por
  grupo y datos mensuales para mapas.

- Ahora
  [`mapear()`](https://docs.ropensci.org/agroclimatico/reference/mapear.md)
  recibe el data.frame de datos como primer argumento

- Arregla error en `compeltar_serie()` para que acepte tanto “dia” como
  “1 dia”

### 04/12/2023

- Cambia el nombre del paquete a agroclimatico

### 30/11/2023

- Cambia el nombre del paquete de agromet a agroclimr
- Cambia el nombre de las funciones `spi()` y `spei()` a
  [`spi_indice()`](https://docs.ropensci.org/agroclimatico/reference/spi_indice.md)
  y
  [`spei_indice()`](https://docs.ropensci.org/agroclimatico/reference/spi_indice.md)
