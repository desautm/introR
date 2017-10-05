# (PART) L'estimation de paramètres et les tests d'hypothèses {-} 

# Les distributions d'échantillonnage
<<<<<<< HEAD

## Paquetages utiles {-}

Chargeons tous les paquetages qui nous seront utiles.


```r
library(dplyr)
library(ggplot2)
library(okcupiddata)
library(mosaic)
```

## L'échantillonnage

Le paquetage `okcupiddata` [@R-okcupiddata] se trouve [ici](https://github.com/rudeboybert/okcupiddata).


```r
profiles_subset <- profiles %>% 
  filter(between(height, 55, 85))
```


