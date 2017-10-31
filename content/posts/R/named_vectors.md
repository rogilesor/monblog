---
title: "Manipuler les noms de vecteurs"
date: 2017-10-31T20:17:13+01:00
draft: true
tags: [ "programmation", "R", "vecteur", "noms","name"]
categories: ["r_language"]
---

Ce petit post permet donne quelques indications pour une manipulations rapides des noms des éléments des vecteurs.

<!--more-->

# creer un vecteur avec des noms



```r
mv <- c(x = 1, y = 2, z = 4)
```

# retrouver des valeurs


```r
mv["x"]
```

```
## x 
## 1
```

```r
mv[1]
```

```
## x 
## 1
```



# affecter facilement des noms aux vecteurs



```r
require(purrr)
set_names(1:3,c("a","b","c"))
```

```
## a b c 
## 1 2 3
```

```r
mv2 <- set_names(1:3,c("a","b","c"))
mv2
```

```
## a b c 
## 1 2 3
```


# subsetting


```r
mv2[c("a","b")]
```

```
## a b 
## 1 2
```


# retrouver les noms


```r
names(mv2)
```

```
## [1] "a" "b" "c"
```

# effacer les noms


```r
names(mv2) <- NULL
mv2
```

```
## [1] 1 2 3
```




