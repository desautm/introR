# (PART) La combinatoire et les probabilités {-} 

# La combinatoire

## La factorielle

Pour calculer la factorielle d'un nombre en `R`, il faut utiliser la commande `factorial`. Par exemple, si nous voulons calculer 6!:


```r
factorial(6)
```

```
## [1] 720
```

## Les combinaisons

Pour calculer le nombre de combinaisons lorsque nous choisissons $k$ objets parmi $n$ (**sans** ordre), c'est-à-dire $C_k^n$, nous utilisons la commande `choose(n,k)`. Par exemple, si nous voulons calculer le nombre de combinaisons possibles au loto 6-49, $C_6^{49}$, nous avons:


```r
choose(49,6)
```

```
## [1] 13983816
```

## Les arrangements

Pour calculer le nombre d'arrangements lorsque nous choisissons $k$ objets parmi $n$ (**avec** ordre), c'est-à-dire $A_k^n$, nous utilisons les commandes `choose(n,k)` et `factorial`. En effet, nous savons que:

\begin{equation}
A_k^n = C_k^n \cdot k!
\end{equation}

et donc on peut calculer un arrangement en effectuant `choose(n,k)*factorial(k)`. Si nous voulons calculer le nombre de comités de 5 personnes nous pouvons former en choisissant parmi 12 personnes, $A_5^{12}$, nous avons:


```r
choose(12,5)*factorial(5)
```

```
## [1] 95040
```

