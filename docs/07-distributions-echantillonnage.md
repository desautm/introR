# (PART) L'estimation de paramètres et les tests d'hypothèses {-} 

# Les distributions d'échantillonnage

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


```r
ggplot(profiles_subset,aes(height)) +
  geom_histogram(bins = 20, color = "white") +
  labs(
    x = "Taille",
    y = "Fréquence",
    title = "Histogramme"
  )
```

<img src="07-distributions-echantillonnage_files/figure-html4/unnamed-chunk-3-1.png" width="672" />


```r
knitr::include_app("http://ismay.shinyapps.io/okcupidheights/")
```

<iframe src="http://ismay.shinyapps.io/okcupidheights/?showcase=0" width="672" height="400px"></iframe>


