# (PART) L'estimation de paramètres et les tests d'hypothèses {-} 

# Les distributions d'échantillonnage

# Paquetages utiles {-}

Chargeons tous les paquetages qui nous seront utiles.


```r
library(dplyr)
```

```
## 
## Attachement du package : 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(ggplot2)
library(okcupiddata)
library(mosaic)
```

```
## Le chargement a nécessité le package : lattice
```

```
## Le chargement a nécessité le package : ggformula
```

```
## 
## New to ggformula?  Try the tutorials: 
## 	learnr::run_tutorial("introduction", package = "ggformula")
## 	learnr::run_tutorial("refining", package = "ggformula")
```

```
## Le chargement a nécessité le package : mosaicData
```

```
## Le chargement a nécessité le package : Matrix
```

```
## 
## The 'mosaic' package masks several functions from core packages in order to add 
## additional features.  The original behavior of these functions should not be affected by this.
## 
## Note: If you use the Matrix package, be sure to load it BEFORE loading mosaic.
```

```
## 
## Attachement du package : 'mosaic'
```

```
## The following object is masked from 'package:Matrix':
## 
##     mean
```

```
## The following objects are masked from 'package:dplyr':
## 
##     count, do, tally
```

```
## The following objects are masked from 'package:stats':
## 
##     binom.test, cor, cor.test, cov, fivenum, IQR, median,
##     prop.test, quantile, sd, t.test, var
```

```
## The following objects are masked from 'package:base':
## 
##     max, mean, min, prod, range, sample, sum
```

## L'échantillonnage

Le paquetage `okcupiddata` se trouve [https://github.com/rudeboybert/okcupiddata](ici)


```r
profiles_subset <- profiles %>% 
  filter(between(height, 55, 85))
```

