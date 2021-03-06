

# (PART) Les mesures associées aux données {-} 

# Les différentes mesures

Dans ce chapitre, nous verrons comment utiliser `R` pour calculer les mesures importantes permettant de résumer des données.

Nous allons charger les paquetages que nous allons utiliser:


```r
library(ggplot2)
library(nycflights13)
```

```
## Warning: le package 'nycflights13' a été compilé avec la version R 3.4.4
```

## Les mesures de tendance centrale

Les mesures de tendance centrale permettent de déterminer où se situe le « centre » des données. Les trois mesures de tendance centrale sont le mode, la moyenne et la médiane.

### Le mode

Le mode est la **modalité**, **valeur** ou **classe** possédant la plus grande fréquence. En d’autres mots, c’est la donnée la plus fréquente. 

Puisque le mode se préoccupe seulement de la donnée la plus fréquente, il n’est pas influencé par les valeurs extrêmes.

Lorsque le mode est une classe, il est appelé **classe modale**. 

Le mode est noté **Mo**. 

Le langage `R` ne possède pas de fonction permettant de calculer le mode. La façon la plus simple de le calculer est d'utiliser la fonction `table` de `R`.

Par exemple, si nous voulons connaître le mode de la variable `cut` de la base de données `diamonds`:


```r
table(diamonds$cut)
```

```
## 
##      Fair      Good Very Good   Premium     Ideal 
##      1610      4906     12082     13791     21551
```

Nous remarquons que le maximum est à la modalité _Ideal_ avec une fréquence de 21551.

Si nous nous intéressons au mode d'une variable quantitative discrète comme `cyl` de la base de données `mtcars` nous obtenons:


```r
table(mtcars$cyl)
```

```
## 
##  4  6  8 
## 11  7 14
```

Nous remarquons que le maximum est à la valeur _8_ avec une fréquence de 14.

Dans le cas d'une variable quantitative continue, pour calculer le mode, il faut commencer par séparer les données en classes. Nous utiliserons les mêmes classes utilisées à la section \@ref(freqquantitatives)


```r
carat_class = cut(diamonds$carat,
                  breaks = seq(from = 0, to = 6, by = 1),
                  right = FALSE)
table(carat_class)
```

```
## carat_class
## [0,1) [1,2) [2,3) [3,4) [4,5) [5,6) 
## 34880 16906  2114    34     5     1
```

La classe modale est donc la classe _[0,1)_ avec une fréquence de 34880.

### La médiane

La médiane, notée **Md**, est la valeur qui sépare une série de données classée en ordre croissant en deux parties égales. 

La médiane étant la valeur du milieu, elle est la valeur où le pourcentage cumulé atteint 50%. 

Puisque la médiane se préoccupe seulement de déterminer où se situe le centre des données, elle n’est pas influencée par les valeurs extrêmes. Elle est donc une mesure de tendance centrale plus fiable que la moyenne.

> Important : La médiane n’est définie que pour les variables quantitatives. En effet, si vous tentez d'utiliser la médiane pour des données autres que numériques, `R` vous donnera un message d'erreur.

La fonction `median` permet de calculer la médiane en langage `R`.

Par exemple, pour calculer la médiane de la variable `carat` de la base de données `diamonds`, nous avons:


```r
median(diamonds$carat)
```

```
## [1] 0.7
```

Ceci signifie que 50% des diamants ont une valeur en carat inférieure ou égale à 0.7 et que 50% des diamants ont une valeur en carat supérieure ou égale à 0.7.

Nous pouvons aussi obtenir que la médiane de la variable `price` de la base de données `diamonds` est donnée par:


```r
median(diamonds$price)
```

```
## [1] 2401
```

### La moyenne

La moyenne est la valeur qui pourrait remplacer chacune des données d’une série pour que leur somme demeure identique. Intuitivement, elle représente le centre d’équilibre d’une série de données. La somme des distances qui sépare les données plus petites que la moyenne devrait être la même que la somme des distances qui sépare les données plus grandes. 

> Important : La moyenne n’est définie que pour les variables quantitatives. En effet, si vous tentez d'utiliser la moyenne pour des données autres que numériques, `R` vous donnera un message d'erreur.

La fonction `mean` permet de calculer la moyenne en langage `R`.

Par exemple, pour calculer la moyenne de la variable `carat` de la base de données `diamonds`, nous avons:


```r
mean(diamonds$carat)
```

```
## [1] 0.7979397
```

Nous pouvons aussi obtenir que la moyenne de la variable `price` de la base de données `diamonds` est donnée par:


```r
mean(diamonds$price)
```

```
## [1] 3932.8
```

## Les mesures de dispersion

Les mesures de tendance centrale (mode, moyenne et médiane) ne permettent pas de déterminer si une série de données est principalement située autour de son centre, ou si au contraire elle est très dispersée. 

Les mesures de dispersion, elles, permettent de déterminer si une série de données est centralisée autour de sa moyenne, ou si elle est au contraire très dispersée. 

Les mesures de dispersion sont l’étendue, la variance, l’écart-type et le coefficient de variation. 

### L'étendue

La première mesure de dispersion, l’étendue, est la différence entre la valeur maximale et la valeur minimale.

L’étendue ne tenant compte que du maximum et du minimum, elle est grandement influencée par les valeurs extrêmes. Elle est donc une mesure de dispersion peu fiable.

La fonction `range` permet de calculer l'étendue d'une variable en langage `R`.

Par exemple, pour calculer l'étendue de la variable `carat` de la base de données `diamonds`, nous avons:


```r
range(diamonds$carat)
```

```
## [1] 0.20 5.01
```

Nous pouvons donc calculer l'étendue de la variable `carat` en soustrayant les deux valeurs obtenues par la fonction `range`, c'est-à-dire que l'étendue est  5.01-0.2 = 4.81.

### La variance

La variance sert principalement à calculer l’écart-type, la mesure de dispersion la plus connue.

> Attention : Les unités de la variance sont des unités^2^.

La fonction `var` permet de calculer la variance d'une variable en langage `R`.

Par exemple, pour calculer la variance de la variable `carat` de la base de données `diamonds`, nous avons:


```r
var(diamonds$carat)
```

```
## [1] 0.2246867
```

Ceci signifie que la variance de la variable `carat` est 0.2246867 carat^2^.

### L'écart-type

L’écart-type est la mesure de dispersion la plus couramment utilisée. Il peut être vu comme la « moyenne » des écarts entre les données et la moyenne.

Puisque l’écart-type tient compte de chacune des données, il est une mesure de dispersion beaucoup plus fiable que l’étendue.

Il est défini comme la racine carrée de la variance.

La fonction `sd` permet de calculer l''écart-type d'une variable en langage `R`.

Par exemple, pour calculer l'écart-type de la variable `carat` de la base de données `diamonds`, nous avons:


```r
sd(diamonds$carat)
```

```
## [1] 0.4740112
```

Ceci signifie que l'écart-type de la variable `carat` est 0.4740112 carat.

### Le coefficient de variation

Le coefficient de variation, noté C. V., est calculé comme suit : 

\begin{equation}
C.V. = \dfrac{\text{ecart-type}}{\text{moyenne}}\times 100\%
\end{equation}

Si le coefficient est inférieur à 15%, les données sont dites **homogènes**. Cela veut dire que les données sont situées près les unes des autres.

Dans le cas contraire, les données sont dites **hétérogènes**. Cela veut dire que les données sont très dispersées.

> Important : Le coefficient de variation ne possède pas d’unité, outre le symbole de pourcentage.

Il n'existe pas de fonctions en `R` permettant de calculer directement le coefficient de variation. Par contre, nous pouvons utiliser en conjonction les fonctions `sd` et `mean` pour le calculer.

Par exemple, pour calculer le coefficient de variation de la variable `carat` de la base de données `diamonds`, nous avons:


```r
sd(diamonds$carat)/mean(diamonds$carat)*100
```

```
## [1] 59.40439
```

Le C.V. de la variable `carat` est donc 59.4043906 %, ce qui signifie que les données sont hétérogènes, car le coefficient de variation est plus grand que 15%.

## Les mesures de position

Les mesures de position permettent de situer une donnée par rapport aux autres. Les différentes mesures de position sont la cote Z, les quantiles et les rangs.

Tout comme les mesures de dispersion, celles-ci ne sont définies que pour une variable quantitative.

### La cote z

Cette mesure de position se base sur la moyenne et l’écart-type.

La cote Z d’une donnée x est calculée comme suit : 

\begin{equation}
Z = \dfrac{x-\text{moyenne}}{\text{ecart-type}}
\end{equation}

> Important : La cote z ne possède pas d'unités.

Une cote Z peut être positive, négative ou nulle. 

| Cote Z | Interprétation |
|-------:|:---------------|
| Z>0 | donnée supérieure à la moyenne | 
| Z<0 | donnée inférieure à la moyenne |
| Z=0 | donnée égale à la moyenne |

Il n'existe pas de fonctions en `R` permettant de calculer directement la cote Z. Par contre, nous pouvons utiliser en conjonction les fonctions `sd` et `mean` pour la calculer.

Par exemple, si nous voulons calculer la cote Z d'un diamant de 3 carats, nous avons:


```r
(3-mean(diamonds$carat))/sd(diamonds$carat)
```

```
## [1] 4.645587
```

### Les quantiles

Un quantile est une donnée qui correspond à un certain pourcentage cumulé.

Parmi les quantiles, on distingue les quartiles, les quintiles, les déciles et les centiles. 

- Les quartiles Q~1~, Q~2~ et Q~3~, séparent les données en quatre parties égales.
Environ 25% des données sont inférieures ou égales à Q~1~.
Environ 50% des données sont inférieures ou égales à Q~2~.
Environ 75% des données sont inférieures ou égales à Q~3~.
- Les quintiles V~1~, V~2~, V~3~ et V~4~, séparent les données en cinq parties égales.
Environ 20% des données sont inférieures ou égales à V~1~.
Environ 40% des données sont inférieures ou égales à V~2~.
Etc.
- Les déciles D~1~, D~2~, ..., D~8~ et D~9~, séparent les données en dix parties égales. 
Environ 10% des données sont inférieures ou égales à D~1~. 
Environ 20% des données sont inférieures ou égales à D~2~.
Etc.
- Les centiles C~1~, C~2~, ..., C~98~ et C~99~, séparent les données en cent parties égales.
Environ 1% des données sont inférieures ou égales à C~1~.
Environ 2% des données sont inférieures ou égales à C~2~.
Etc.

> Il est utile de noter que certains quantiles se recoupent. 

La fonction `quantile` permet de calculer n'importe quel quantile d'une variable en langage `R`. Il suffit d'indiquer la variable étudiée ainsi que le pourcentage du quantile voulu.

Par exemple, si nous voulons calculer D~1~ pour la variable `carat`, nous allons utiliser la fonction `quantile` avec une probabilité de 0,1.


```r
quantile(diamonds$carat, 0.1)
```

```
##  10% 
## 0.31
```

Ceci implique que 10% des diamants ont une valeur en carat inférieure ou égale à 0.31 carat.

Nous pouvons calculer le troisième quartile Q~3~ de la variable `price` en utilisant la fonction `quantile` avec une probabilité de 0,75.


```r
quantile(diamonds$price, 0.75)
```

```
##     75% 
## 5324.25
```

Ceci implique que 75% des diamants ont un prix en dollars inférieur ou égal à 5324.25 $.

### La commande `summary`

La commande `summary` produit un sommaire contenant six mesures importantes:

1. `Min` : le minimum de la variable
2. `1st Qu.`: Le premier quartile, Q~1~, de la variable
3. `Median` : La médiane de la variable
4. `Mean` : La moyenne de la variable
5. `3rd Qu.` : Le troisième quartile, Q~3~, de la variable
6. `Max` : Le maximum de la variable

Nous pouvons donc produire le sommaire de la variable `price` de la base de données `diamonds` de la façon suivante:


```r
summary(diamonds$price)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##     326     950    2401    3933    5324   18823
```

### Le rang centile

Un rang centile représente le pourcentage cumulé, *exprimé en nombre entier*, qui correspond à une certaine donnée. Nous déterminerons les rangs centiles pour les variables continues seulement.

Les rangs centiles sont donc exactement l’inverse des centiles.

Il n'existe pas de fonctions dans `R` permettant de trouver directement le rang centile, mais il est facile d'utiliser la fonction `mean` pour le trouver. 

Par exemple, si nous voulons trouver le rang centile d'un diamant qui coûte 500\$, il suffit d'utiliser la commande suivante. La commande calcule la moyenne de toutes les valeurs en dollars des diamants coûtant 500\$ ou moins.


```r
mean(diamonds$price<=500)
```

```
## [1] 0.03242492
```

Ceci signifie que pour un diamant de 500\$, il y a 3.2424917 % des diamants qui ont une valeur égale ou inférieure.
