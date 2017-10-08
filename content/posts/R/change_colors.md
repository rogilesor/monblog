---
title: "raster image change color"
date: 2017-10-08
tags: [ "programmation", "R", "grid", "image"]
categories: ["r_language"]
---

Cet article présente comment transformer une image avec le language R. On isole une matrice qui associe à chaque pixel une couleur et on travaille sur cette matrice.

<!--more-->

## Première étape : isoler la matrice des couleurs

Il faut importer l'image avec la librairie png puis on utilise la fonction as.raster pour transformer l'image en matrice.
La matrice associe à chaque pixel une couleur. Cette matrice permettra par la suite de manipuler l'image.


```r
library(jpeg)
library(grid)
library(png)

test <- readPNG("test.png")
rtest <- as.raster(test)
dim(rtest)
```

```
## [1] 245 206
```

```r
rtest[12,24]
```

```
##      [,1]     
## [1,] "#FFFFFF"
```

## Changer les couleurs dans la matrice


```r
elt <- rtest == "#FFFFFF"
rtest[elt] <- "red"
head(rtest)
```

```
## [1] "red" "red" "red" "red" "red" "red"
```

## Tracer la nouvelle image

on utilise pour ca la librairie grid.


```r
require(grid)
pushViewport(viewport())
grid.raster(rtest,y=1, just="top")
```

![plot of chunk color1](/figure/color1-1.png)

