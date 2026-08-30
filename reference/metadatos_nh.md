# Tabla de Metadatos de Estaciones NH

Devuelve los metadatos de estaciones incluyendo el código único,
ubicación (latitud y longitud) y el nombre.

## Uso

``` r
metadatos_nh(
  codigo = NULL,
  provincia = NULL,
  organismo = NULL,
  lat = NULL,
  lon = NULL
)
```

## Argumentos

- codigo, provincia, organismo:

  carácter o vector de caracteres para filtrar según código de estación,
  provincia u organismo.

- lat:

  vector numérico con las latitudes límite de la región de interés.

- lon:

  vector numérico con las longitudes límite de la región de interés
  (entre -180 y 180).

## Valor

data.frame con los metadatos de las estaciones cuyas columnas incluye:

- `codigo_nh` (caracter), variable llave para acceder a los metadatos de
  estaciones

- `estacion` (caracter), nombre de la estación

- `provincia` (caracter), provincia donde se encuentra la estación

- `organismo` (caracter), organismo a cargo de la estación

- `lat` (numérico), longitud

- `lon` (numérico), latitud

- `altura` (numérico), altura sobre el nivel del mar de la estación

## Detalles

Esta función por defecto devuelve la lista completa de estaciones pero
alternativamente se puede devolver estaciones específicas a partir de
sus códigos o todas las estaciones incluidas en una región. Además
incluye un método plot para visualizar rápidamente la ubicación de las
estaciones.

## Ejemplos

``` r
# listado completo de estaciones
head(metadatos_nh(), n = 10)
#>    codigo_nh      estacion    provincia organismo    lat    lon altura
#> 1       0446        Anguil     La Pampa      INTA -36.50 -63.98    165
#> 2       0196          Azul Buenos Aires       SMN -36.75 -59.83    132
#> 3       0221  Bahía Blanca Buenos Aires       SMN -38.73 -62.17     83
#> 4       0400      Balcarce Buenos Aires      INTA -37.75 -58.30    130
#> 5       0323     Bariloche    Río Negro       SMN -41.15 -71.17    840
#> 6       0216        Barrow Buenos Aires      INTA -38.32 -60.25    120
#> 7       0067   Bella Vista   Corrientes      INTA -28.43 -58.92     70
#> 8       0008 Benito Juárez Buenos Aires       SMN -37.72 -59.78    207
#> 9       0189       Bolívar Buenos Aires       SMN -36.25 -61.10     93
#> 10      0343     Bordenave Buenos Aires      INTA -37.85 -63.02    212

# listado de estaciones específicas
metadatos_nh(codigo = c("0001", "0011"))
#>   codigo_nh    estacion provincia organismo   lat    lon altura
#> 1      0001   La Quiaca     Jujuy       SMN -22.1 -65.60   3459
#> 2      0011 Las Lomitas   Formosa       SMN -24.7 -60.58    130

# Filtrar por provincias
metadatos_nh(provincia = c("La Pampa", "Catamarca"))
#>   codigo_nh     estacion provincia organismo    lat    lon altura
#> 1      0446       Anguil  La Pampa      INTA -36.50 -63.98    165
#> 2      0044    Catamarca Catamarca       SMN -28.60 -65.77    454
#> 3      0334 General Pico  La Pampa       SMN -35.70 -63.75    145
#> 4      0192   Santa Rosa  La Pampa       SMN -36.57 -64.27    191
#> 5      0065    Tinogasta Catamarca       SMN -28.07 -67.57   1201
#> 6      0188    Victorica  La Pampa       SMN -36.22 -65.43    312

# Filtrar por organismo
metadatos_nh(organismo = "INTA")
#>    codigo_nh            estacion           provincia organismo    lat    lon
#> 1       0446              Anguil            La Pampa      INTA -36.50 -63.98
#> 2       0400            Balcarce        Buenos Aires      INTA -37.75 -58.30
#> 3       0216              Barrow        Buenos Aires      INTA -38.32 -60.25
#> 4       0067         Bella Vista          Corrientes      INTA -28.43 -58.92
#> 5       0343           Bordenave        Buenos Aires      INTA -37.85 -63.02
#> 6       0997              Canals             Córdoba      INTA -33.57 -62.88
#> 7       0358            Castelar        Buenos Aires      INTA -34.67 -58.65
#> 8       0988       Castelli,J.J.               Chaco      INTA -25.45 -60.63
#> 9       0423          Cerro Azul            Misiones      INTA -27.65 -55.43
#> 10      0487     Colonia Benítez               Chaco      INTA -27.42 -58.93
#> 11      0497   Conc. del Uruguay          Entre Ríos      INTA -32.48 -58.23
#> 12      0496           Concordia          Entre Ríos      INTA -31.36 -58.12
#> 13      0464         El Colorado             Formosa      INTA -26.30 -59.37
#> 14      0444            Famaillá             Tucumán      INTA -27.05 -65.42
#> 15      0038    General Villegas        Buenos Aires      INTA -34.92 -62.73
#> 16      0421    Hilario Ascasubi        Buenos Aires      INTA -39.38 -62.62
#> 17      0442         La Consulta             Mendoza      INTA -33.73 -69.12
#> 18      0550            La María Santiago del Estero      INTA -28.23 -64.15
#> 19      0416          Las Breñas               Chaco      INTA -27.08 -61.12
#> 20      0910           Las Rosas            Santa Fe      INTA -32.48 -61.57
#> 21      0438            Manfredi             Córdoba      INTA -31.82 -63.77
#> 22      0502       Marcos Juárez             Córdoba      INTA -32.68 -62.12
#> 23      0498            Mercedes          Corrientes      INTA -29.17 -58.02
#> 24      0472            Oliveros            Santa Fe      INTA -32.55 -60.85
#> 25      0114              Paraná          Entre Ríos      INTA -31.83 -60.52
#> 26      0145           Pergamino        Buenos Aires      INTA -33.93 -60.55
#> 27      0098             Rafaela            Santa Fe      INTA -31.18 -61.55
#> 28      0437         Reconquista            Santa Fe      INTA -29.25 -59.73
#> 29      0415 P. Roque Saenz Peña               Chaco      INTA -26.87 -60.45
#> 30      0445            San Juan            San Juan      INTA -31.37 -68.32
#> 31      0492           San Pedro        Buenos Aires      INTA -33.68 -59.68
#> 32      0439      Villa Mercedes            San Luis      INTA -33.72 -65.48
#> 33      0046       Zavalla-Univ.            Santa Fe      INTA -33.02 -60.88
#> 34      0989   Capilla del Monte             Córdoba      INTA -30.87 -64.55
#>    altura
#> 1     165
#> 2     130
#> 3     120
#> 4      70
#> 5     212
#> 6      NA
#> 7      22
#> 8      NA
#> 9     270
#> 10     54
#> 11     21
#> 12     48
#> 13     78
#> 14    363
#> 15    117
#> 16     22
#> 17    940
#> 18    169
#> 19    102
#> 20     NA
#> 21    292
#> 22    110
#> 23    100
#> 24     26
#> 25    110
#> 26     65
#> 27    100
#> 28     42
#> 29     90
#> 30    618
#> 31     28
#> 32    515
#> 33     50
#> 34     NA

# listados de estaciones en una región
metadatos_nh(lat = c(-30, -20), lon = c(-65, -55))
#>    codigo_nh             estacion           provincia organismo    lat    lon
#> 1       0067          Bella Vista          Corrientes      INTA -28.43 -58.92
#> 2       0988        Castelli,J.J.               Chaco      INTA -25.45 -60.63
#> 3       0081                Ceres            Santa Fe       SMN -29.88 -61.95
#> 4       0423           Cerro Azul            Misiones      INTA -27.65 -55.43
#> 5       0487      Colonia Benítez               Chaco      INTA -27.42 -58.93
#> 6       0470           Corrientes          Corrientes       SMN -27.47 -58.82
#> 7       0080        Curuzu Cuatia          Corrientes       SMN -29.78 -57.98
#> 8       0464          El Colorado             Formosa      INTA -26.30 -59.37
#> 9       0483              Formosa             Formosa       SMN -26.20 -58.23
#> 10      0550             La María Santiago del Estero      INTA -28.23 -64.15
#> 11      0416           Las Breñas               Chaco      INTA -27.08 -61.12
#> 12      0011          Las Lomitas             Formosa       SMN -24.70 -60.58
#> 13      0498             Mercedes          Corrientes      INTA -29.17 -58.02
#> 14      0021                Metán               Salta       SMN -25.48 -64.80
#> 15      0057                Oberá          Corrientes       SMN -27.48 -55.13
#> 16      0339                 Orán               Salta       SMN -23.15 -64.32
#> 17      0346   Paso de los Libres          Corrientes       SMN -29.68 -57.15
#> 18      0362              Posadas            Misiones       SMN -27.37 -55.97
#> 19      0309          Reconquista            Santa Fe       SMN -29.18 -59.70
#> 20      0437          Reconquista            Santa Fe      INTA -29.25 -59.73
#> 21      0489          Resistencia               Chaco       SMN -27.45 -59.05
#> 22      0458            Río Hondo Santiago del Estero       SMN -27.29 -64.56
#> 23      0006            Rivadavia               Salta       SMN -24.17 -62.90
#> 24      0034  P. Roque Saenz Peña               Chaco       SMN -26.82 -60.45
#> 25      0415  P. Roque Saenz Peña               Chaco      INTA -26.87 -60.45
#> 26      0062  Santiago del Estero Santiago del Estero       SMN -27.77 -64.30
#> 27      0326             Tartagal               Salta       SMN -22.65 -63.82
#> 28      0082 V.Maria del Río Seco             Córdoba       SMN -29.90 -63.68
#> 29      0522             Yaciretá          Corrientes       SMN -27.57 -56.68
#> 30      0075             Mercedes          Corrientes       SMN -29.23 -58.08
#>    altura
#> 1      70
#> 2      NA
#> 3      88
#> 4     270
#> 5      54
#> 6      62
#> 7      73
#> 8      78
#> 9      60
#> 10    169
#> 11    102
#> 12    130
#> 13    100
#> 14    855
#> 15    343
#> 16    357
#> 17     70
#> 18    133
#> 19     53
#> 20     42
#> 21     52
#> 22    280
#> 23    205
#> 24     92
#> 25     90
#> 26    199
#> 27    450
#> 28    341
#> 29     72
#> 30    107

# gráfico
plot(metadatos_nh())

```
