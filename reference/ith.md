# Índice de Temperatura y Humedad

Calcula el índice de temperatura y humedad (ITH)

## Uso

``` r
ith(temperatura, hr)
```

## Argumentos

- temperatura:

  vector numérico con valores (o valor) de temperatura en grados
  centígrados.

- hr:

  vector númerico (o valor) de la misma longitud que temperatura con la
  humedad relativa en porcentaje.

## Valor

Devuelve un valor o vector de valores con el ITH. Este valor es
utilizado como una medida de la intensidad de las condiciones de estrés
por calor a la que se encuentra expuesto el animal. Para bovinos se
categoriza como:

- **Normal** si ITH \< 75

- **Alerta** para ITH entre 75 y 78

- **Peligro** para ITH entre 79 y 83

- **Emergencia** para ITH \>= 84

## Referencias

- Armendano, J. I. ¿Cuándo se generan condiciones de estrés por calor en
  bovinos para carne?
  [link](https://inta.gob.ar/sites/default/files/inta_estres_por_calor_bovinos_para_carne.pdf)

- Armstrong, DV. 1994. Heat stress interaction with shade and
  cooling. J. Diary Sci. 77:2004-2050

## Ejemplos

``` r
ith(temperatura = 23, hr = 65)
#> [1] 70.4355

data(NH0358)

# En el contexto de mutate
library(dplyr)
NH0358 %>%
  filter(!is.na(hr)) %>%
  mutate(t_media = (t_max + t_min)/2) %>%
  mutate(ith = ith(t_media, hr)) %>%
  slice_head(n = 10)
#>    codigo codigo_nh      fecha t_max t_min precip lluvia_datos lluvia llovizna
#> 1      50      0358 1960-01-01  24.4  10.3    0.0            0      0        0
#> 2      50      0358 1960-01-02  26.2  11.8    0.0            0      0        0
#> 3      50      0358 1960-01-03  30.3  10.8    0.0            0      0        0
#> 4      50      0358 1960-01-04  33.5  16.4    0.0            0      0        0
#> 5      50      0358 1960-01-05  29.1  19.0    7.7            1      1        1
#> 6      50      0358 1960-01-06  31.4  15.3    0.0            0      0        0
#> 7      50      0358 1960-01-07  31.9  16.1    0.0            0      0        0
#> 8      50      0358 1960-01-08  33.8  17.4    0.0            0      0        0
#> 9      50      0358 1960-01-09  32.8  18.3    0.0            0      0        0
#> 10     50      0358 1960-01-10  33.1  18.9    0.0            0      0        0
#>    granizo nieve t_aire_max t_aire_min t_suelo_max t_suelo_min heliofania_efec
#> 1        0     0        7.7         NA          NA          NA            11.5
#> 2        0     0        8.0         NA          NA          NA             6.4
#> 3        0     0       11.4         NA          NA          NA            10.7
#> 4        0     0       11.1         NA          NA          NA            10.8
#> 5        0     0       15.9         NA          NA          NA             0.2
#> 6        0     0       13.2         NA          NA          NA            11.0
#> 7        0     0       11.5         NA          NA          NA            11.5
#> 8        0     0       13.9         NA          NA          NA            11.1
#> 9        0     0       15.4         NA          NA          NA            11.4
#> 10       0     0       14.1         NA          NA          NA            11.3
#>    heliofania_rel p_vapor hr   td rocio viento_10m viento_2m  rad etp t_media
#> 1              80     9.2 56  5.8     0          3       2.4 27.9 4.8   17.35
#> 2              45    11.1 56  8.5     0          2       1.6 19.1 3.9   19.00
#> 3              75    10.4 45  7.5     0         10       8.0 26.5 5.9   20.55
#> 4              75    10.7 41  8.0     0          4       3.2 26.6 5.7   24.95
#> 5               1    15.7 74 13.7     0          1       0.8  8.4 2.8   24.05
#> 6              77    13.0 58 10.9     0          0       0.0 26.9 5.0   23.35
#> 7              80    11.4 45  8.9     1          6       4.8 27.8 6.1   24.00
#> 8              78    12.3 42 10.0     0          7       5.6 27.1 6.4   25.60
#> 9              80    16.1 59 14.1     0         11       8.8 27.6 6.9   25.55
#> 10             79    12.4 48 10.1     0         13      10.4 27.4 7.4   26.00
#>         ith
#> 1  61.96434
#> 2  64.21560
#> 3  65.66553
#> 4  70.77370
#> 5  72.81753
#> 6  70.32707
#> 7  69.99700
#> 8  71.67448
#> 9  73.48225
#> 10 72.85120
```
