# (PART) La présentation des données {-} 

# Introduction {#intro}

## Tibbles

Pour être en mesure d'effectuer des  calculs statistiques, il nous faut une structure qui soit en mesure de garder en mémoire une base de données. Ces structures se nomment des "tibbles" dans R.

### Prérequis

Pour être en mesure d'utiliser le paquetage **tibble**, nous devons charger le paquetage **tibble** et le paquetage **knitr**. Pour ce faire, il suffit d'utiliser la commande suivante:


```r
library(tibble)
library(knitr)
```

Si vous exécutez ce code et vous recevez le message d'erreur suivant "there is no package called 'tibble'", vous allez devoir installer le paquetage et ensuite charger la librairie.

```
install.packages("tibble")
library(tibble)
```

Vous faites la même chose pour le paquetage **knitr**.

Vous devez installer le paquetage une seule fois, mais vous devez le charger à chaque fois que vous démarrez une session en R.

### Un exemple de "tibble"

Pour comprendre ce qu'est un "tibble", nous allons utiliser deux paquetages: "nycflights13" et "diamonds". Si ce n'est pas déjà fait, vous devez les installer et ensuite les charger.


```r
library(nycflights13)
```

```
## Warning: le package 'nycflights13' a été compilé avec la version R 3.4.4
```

```r
library(ggplot2)
```

Nous allons étudier le paquetage "nycflights13" qui contient 5 bases de données contenant des informations concernant les vols intérieurs en partance de New York en 2013, à partir des aéroports de Newark Liberty International (EWR), John F. Kennedy International (JFK) ou LaGuardia (LGA). Les 5 bases de données sont les suivantes:

- flights: information sur les 336,776 vols
- airlines: lien entre les codes IATA de deux lettres et les noms de compagnies d'aviation (16 au total)
- planes: information de construction sur les 3 322 avions utilisés
- weather: données météo à chaque heure (environ 8 710 observations) pour chacun des trois aéroports.
- airports: noms des aéroports et localisations

### La base de données flights

Pour visualiser facilement une base de données sous forme "tibble", il suffit de taper son nom dans la console. Nous allons utiliser la base de données flights. Par exemple:


```r
flights
```

```
## # A tibble: 336,776 x 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
##  1  2013     1     1      517            515      2.00      830
##  2  2013     1     1      533            529      4.00      850
##  3  2013     1     1      542            540      2.00      923
##  4  2013     1     1      544            545     -1.00     1004
##  5  2013     1     1      554            600     -6.00      812
##  6  2013     1     1      554            558     -4.00      740
##  7  2013     1     1      555            600     -5.00      913
##  8  2013     1     1      557            600     -3.00      709
##  9  2013     1     1      557            600     -3.00      838
## 10  2013     1     1      558            600     -2.00      753
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

Nous allons décortiquer la sortie console:

- `A tibble: 336,776 x 19`: un "tibble" est une façon de représenter une base de données en R. Cette base de données possède:
    * `336 776` lignes
    * `19` colonnes correspondant aux 19 variables décrivant chacune des observations
- `year month` `day` `dep_time` `sched_dep_time` `dep_delay` `arr_time` sont différentes colonnes, en d'autres mots des variables, de cette base de données.
- Nous avons ensuite 10 lignes d'obervations correspondant à 10 vols
- `... with 336,766 more rows, and 12 more variables:` nous indique que 336 766 lignes et 12 autres variables ne pouvaient pas être affichées à l'écran.

Malheureusement cette sortie écran ne nous permet pas d'explorer les données correctement. Nous verrons à la section \@ref(explorertibbles) comment explorer des `tibbles`.

### La base de données `diamonds` {#donneesdiamonds}

La base de données `diamonds` est composée des variables suivantes:

- `price` : prix en dollars US
- `carat` : poids du diamant en grammes
- `cut` : qualité de la coupe (Fair, Good, Very Good, Premium, Ideal)
- `color` : couleur du diamant (J (pire) jusqu'à D (meilleur))
- `clarity` : une mesure de la clarté du diamant (I1 (pire), SI2, SI1, VS2, VS1, VVS2, VVS1, IF (meilleur))
- `x` : longueur en mm
- `y` : largeur en mm
- `z` : hauteur en mm
- `depth` : z / mean(x, y) = 2 * z / (x + y)
- `table` : largeur du dessus du diamant par  rapport à son point le plus large


```r
diamonds
```

```
## # A tibble: 53,940 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1 0.230 Ideal     E     SI2      61.5  55.0   326  3.95  3.98  2.43
##  2 0.210 Premium   E     SI1      59.8  61.0   326  3.89  3.84  2.31
##  3 0.230 Good      E     VS1      56.9  65.0   327  4.05  4.07  2.31
##  4 0.290 Premium   I     VS2      62.4  58.0   334  4.20  4.23  2.63
##  5 0.310 Good      J     SI2      63.3  58.0   335  4.34  4.35  2.75
##  6 0.240 Very Good J     VVS2     62.8  57.0   336  3.94  3.96  2.48
##  7 0.240 Very Good I     VVS1     62.3  57.0   336  3.95  3.98  2.47
##  8 0.260 Very Good H     SI1      61.9  55.0   337  4.07  4.11  2.53
##  9 0.220 Fair      E     VS2      65.1  61.0   337  3.87  3.78  2.49
## 10 0.230 Very Good H     VS1      59.4  61.0   338  4.00  4.05  2.39
## # ... with 53,930 more rows
```

### Comment explorer des "tibbles" {#explorertibbles}

Voici les façons les plus communes de comprendre les données se trouvant à l'intérieur d'un "tibble":

    1. En utilisant la fonction `View()` de RStudio.C'est la commande que nous utiliserons le plus fr?quemment.
    2. En utilisant la fonction `glimpse()` du paquetage knitr
    3. En utilisant la fonction `kable()`
    4. En utilisant l'opérateur `$` pour étudier une seule variable d'une base de données

1. `View()`:

Éxécutez `View(flights)` dans la console de RStudio et explorez la base de données obtenue. 

Nous remarquons que chaque colonnes représentent une variable différente et que ces variables peuvent être de différents types. Certaines de ces variables, comme `distance`, `day` et `arr_delay` sont des variables dites quantitatives. Ces variables sont numériques par nature. D'autres variables sont dites qualitatives.

Si vous regardez la colonne à l'extrème-gauche de la sortie de `View(flights)`, vous verrez une colonne de nombres. Ces nombres représentent les numéros de ligne de la base de données. Si vous vous promenez sur une ligne de même nombre, par exemple la ligne 5, vous étudiez une unité statistique.

2. `glimpse`:

La seconde façon d'explorer une base de données est d'utiliser la fonction `glimpse()`. Cette fonction nous donne la majorité de l'information précédente et encore plus.


```r
glimpse(flights)
```

```
## Observations: 336,776
## Variables: 19
## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,...
## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 55...
## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 60...
## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2...
## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 7...
## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 7...
## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -...
## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV",...
## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79...
## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN...
## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR"...
## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL"...
## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138...
## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 94...
## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5,...
## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, ...
## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013...
```

3. `kable()`:

La dernière façon d'étudier l'entièreté de la base de données est d'utiliser la fonction `kable()`. Nous allons explorer les codes des différentes compagnies d'aviation de deux façons.


```r
airlines
```

```
## # A tibble: 16 x 2
##    carrier name                       
##    <chr>   <chr>                      
##  1 9E      Endeavor Air Inc.          
##  2 AA      American Airlines Inc.     
##  3 AS      Alaska Airlines Inc.       
##  4 B6      JetBlue Airways            
##  5 DL      Delta Air Lines Inc.       
##  6 EV      ExpressJet Airlines Inc.   
##  7 F9      Frontier Airlines Inc.     
##  8 FL      AirTran Airways Corporation
##  9 HA      Hawaiian Airlines Inc.     
## 10 MQ      Envoy Air                  
## 11 OO      SkyWest Airlines Inc.      
## 12 UA      United Air Lines Inc.      
## 13 US      US Airways Inc.            
## 14 VX      Virgin America             
## 15 WN      Southwest Airlines Co.     
## 16 YV      Mesa Airlines Inc.
```

```r
kable(airlines)
```



carrier   name                        
--------  ----------------------------
9E        Endeavor Air Inc.           
AA        American Airlines Inc.      
AS        Alaska Airlines Inc.        
B6        JetBlue Airways             
DL        Delta Air Lines Inc.        
EV        ExpressJet Airlines Inc.    
F9        Frontier Airlines Inc.      
FL        AirTran Airways Corporation 
HA        Hawaiian Airlines Inc.      
MQ        Envoy Air                   
OO        SkyWest Airlines Inc.       
UA        United Air Lines Inc.       
US        US Airways Inc.             
VX        Virgin America              
WN        Southwest Airlines Co.      
YV        Mesa Airlines Inc.          

À première vue, les deux sorties sont semblables sauf que la seconde est beaucoup plus agréable visuellement dans un document R Markdown.

4. L'opérateur `$`:

Finalement, l'opérateur `$` nous permet d'explorer une seule variable à l'intérieur d'une base de données. Par exemple, si nous désirons étudier la variable `name` de la base de données `airlines`, nous obtenons:


```r
airlines$name
```

```
##  [1] "Endeavor Air Inc."           "American Airlines Inc."     
##  [3] "Alaska Airlines Inc."        "JetBlue Airways"            
##  [5] "Delta Air Lines Inc."        "ExpressJet Airlines Inc."   
##  [7] "Frontier Airlines Inc."      "AirTran Airways Corporation"
##  [9] "Hawaiian Airlines Inc."      "Envoy Air"                  
## [11] "SkyWest Airlines Inc."       "United Air Lines Inc."      
## [13] "US Airways Inc."             "Virgin America"             
## [15] "Southwest Airlines Co."      "Mesa Airlines Inc."
```

## Types de variables

Nous pouvons utiliser différents types de variables avec le langage `R`.

### Variables qualitatives

Une variable qualitative est une variable dont les résultats possibles sont des **mots**. Les différents **mots** que peuvent prendre une telle variable sont appelées des **modalités**.

#### Variables qualitatives à échelle nominale

On observe ce type de variable lorsqu’il n’y a pas d’ordre croissant naturel dans les **modalités** de la variable. Par exemple, la variable _couleur des cheveux_ est à échelle nominale. L'ordre « blonds, bruns, roux, noirs, autre » est un ordre aussi valable que 
« bruns, noirs, roux, blonds, autre ».

Dans la base de données `nycflights13`, la variable `origin` provenant des données `flights` est une variable qualitative nominale.


```r
unique(flights$origin)
```

```
## [1] "EWR" "LGA" "JFK"
```

Autre que l'ordre alphabétique, nous n'avons pas d'autre ordre logique à imposer à l'aéroport d'origine des vols.

#### Variables qualitatives à échelle ordinale

On observe ce type de variable lorsqu’il existe un ordre croissant dans les modalités de la variable. Par exemple, la variable _degré de satisfaction_ est à échelle ordinale. Il est possible de classer les modalités en ordre décroissant en écrivant : Très satisfait  >  Satisfait  >  Insatisfait  >  Très insatisfait.

Dans la base de données `diamonds`, la variable `cut` est une variable qualitative à échelle ordinale.


```r
unique(diamonds$cut)
```

```
## [1] Ideal     Premium   Good      Very Good Fair     
## Levels: Fair < Good < Very Good < Premium < Ideal
```

Nous remarquons que les modalités de cette variable possèdent un ordre. Cet ordre est indiqué par les symboles `<` dans la sortie `R`.

### Variables quantitatives

Une variable quantitative est une variable dont les résultats possibles sont des **nombres**. Les différents nombres que peuvent prendre une telle variable sont appelées des **valeurs**.

#### Variables quantitatives discrètes

On observe ce type de variable lorsque les valeurs sont énumérables, c’est-à-dire lorsqu’il n’existe pas de valeur possible entre deux valeurs consécutives. Par exemple, la variable _nombre de cours suivis pendant cette session_ est une variable quantitative discrète. Les valeurs de ces variables peuvent être : 3, 4, 5, 6, 7,... Il est impossible de suivre 4,6 cours durant une session.

Dans la base de données `nycflights13`, la variable `engines` provenant des données `planes` est une variable quantitative discrète. Cette variable représente le nombre de moteurs de l'avion en question.


```r
unique(planes$engines)
```

```
## [1] 2 1 4 3
```

Dans la sortie `R` les valeurs ne sont pas en ordre croissant mais elles le seront lorsque nous les représenterons sous forme de tableau ou de graphique.

#### Variables quantitatives continues

On observe ce type de variable lorsqu’il existe une infinité de valeurs entre deux autres. Par exemple, la variable _masse d’un étudiant (en lbs)_ est une variable quantitative continue. Entre 130 et 131 lbs, il existe une infinité de valeurs telles que 130,54 lbs.

Dans la base de données `diamonds`, nous allons observer la variable `carat`. Voici les 25 premiers éléments de ces valeurs.


```r
diamonds$carat[1:25]
```

```
##  [1] 0.23 0.21 0.23 0.29 0.31 0.24 0.24 0.26 0.22 0.23 0.30 0.23 0.22 0.31
## [15] 0.20 0.32 0.30 0.30 0.30 0.30 0.30 0.23 0.23 0.31 0.31
```
