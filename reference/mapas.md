# Mapas

Mapas de Argentina, sus provincias, departamentos y paises limítrofes.
Los mapas de departamentos surgen del repositorio público del [Instituto
Geográfico
Nacional](https://www.ign.gob.ar/NuestrasActividades/InformacionGeoespacial/CapasSIG),
mientas que el mapa de países limítrofes, Argentina y sus provincias son
parte del repositorio [Natural
Earth](https://www.naturalearthdata.com/).

## Uso

``` r
mapa_argentina()

mapa_provincias(provincias = NULL, departamentos = FALSE)

mapa_argentina_limitrofes()

mapa_departamentos(provincias = NULL)
```

## Argumentos

- provincias:

  vector de caracteres con los nombres de provincias a filtrar. Si es
  `NULL`, devuelve todas las provincias de Argentina.

- departamentos:

  lógico. Si es `TRUE` grafica los departamentos.

## Valor

Devuelve una tibble con las variables necesarias para generar un mapa
utilizando ggplot2 y sf.

## Detalles

Los nombres de las provincias e `mapa_provincias()` son: Buenos Aires,
Catamarca, Chaco, Chubut, Ciudad de Buenos Aires, Corrientes, Córdoba,
Entre Ríos, Formosa, Islas Malvinas (geometria separada de Tierra del
fuego), Jujuy, La Pampa, La Rioja, Mendoza, Misiones, Neuquén, Río
Negro, Salta, San Juan, San Luis, Santa Cruz, Santa Fe, Santiago del
Estero, Tierra del Fuego y Tucumán y se pueden utilizar para graficarlas
individualmente.

## Ejemplos

``` r
library(ggplot2)

# Solo Argentina
ggplot() +
  geom_sf(data = mapa_argentina())


# Argentina y sus provincias
ggplot() +
  geom_sf(data = mapa_provincias())


# Algunas provincias
ggplot() +
  geom_sf(data = mapa_provincias(provincias = c("La Pampa", "Córdoba")))


# Algunas provincias y sus departamentos
ggplot() +
  geom_sf(data = mapa_provincias(provincias = c("La Pampa", "Córdoba"),
                                 departamentos = TRUE))
#> Descargando mapa...
#> Warning: 'x' is NULL so the result will be NULL

```
