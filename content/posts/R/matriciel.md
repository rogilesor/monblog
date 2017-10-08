---
title: "Image_matricielle_grid"
date: 2017-10-08
tags: [ "programmation", "R", "grid", "image"]
categories: ["r_language"]
---



## Définition

Les images matricielles sont très bien définies dans wikipédia :

Une image matricielle, ou « carte de points » (de l'anglais bitmap), est une image constituée d'une matrice de points colorés. C'est-à-dire, constituée d'un tableau, d'une grille, où chaque case possède une couleur qui lui est propre et est considérée comme un point. Il s'agit donc d'une juxtaposition de points de couleurs formant, dans leur ensemble, une image.

En anglais on dit "raster image" pour image matricielle.

## Le package png

Le package png est utilisé pour importer des images.


```r
require(png)
setwd("~/Desktop/image_matricielle")
test <- readPNG("test.png")
```


## La fonction as.raster

La fonction __as.raster__ permet de transformer une image importée en matrice qui pourra ensuite être utilisée pour visualisation.


```r
rtest <- as.raster(test)
head(rtest)
```

```
## [1] "#FFFFFF" "#FFFFFF" "#FFFFFF" "#FFFFFF" "#FFFFFF" "#FFFFFF"
```

## L'utilisation de la fonction grid.raster

La fonction grid.raster permet de tracer l'image. C'est une fonction du grid package, cela veut dire qu'il faut d'abord appeler un Viewport


```r
require(grid)
pushViewport(viewport(angle=45))
grid.raster(rtest, y=1, just="top")
```

![plot of chunk b1](/figure/b1-1.png)

## Un gradient de couleur

Cela permet de nombreuses utilisations. Il est notamment possible de visualiser un gradient de couleur. Pour cela, il faudra d'abord utiliser la fonction hcl.

### La fonction hcl

crée un vecteur de couleur à partir de données "hue, chroma, luminance"


```r
hcl(0,80,seq(50,80,10))
```

```
## [1] "#C54E6D" "#E16A86" "#FE86A1" "#FFA2BC"
```

Il est possible de spécifier les lignes et colonnes


```r
matrix(hcl(0, 80, seq(50, 80, 10)),nrow=4, ncol=5)
```

```
##      [,1]      [,2]      [,3]      [,4]      [,5]     
## [1,] "#C54E6D" "#C54E6D" "#C54E6D" "#C54E6D" "#C54E6D"
## [2,] "#E16A86" "#E16A86" "#E16A86" "#E16A86" "#E16A86"
## [3,] "#FE86A1" "#FE86A1" "#FE86A1" "#FE86A1" "#FE86A1"
## [4,] "#FFA2BC" "#FFA2BC" "#FFA2BC" "#FFA2BC" "#FFA2BC"
```

### Tracer le gradiant de couleur

A partir de là, il sera très facile de tracer le gradient de couleur


```r
redGradient <- matrix(hcl(0, 80, seq(50, 80, 10)),nrow=4, ncol=5)
grid.raster(redGradient)
```

![plot of chunk b2](/figure/b2-1.png)

## Le package lattice

L'utilisation avec le package lattice est très intéressante


```r
require(lattice)

x <- rep(5,12)
x
```

```
##  [1] 5 5 5 5 5 5 5 5 5 5 5 5
```

```r
barchart(1:12 ~ x, origin=0, col="white",
                  panel=function(x, y, ...) {
                    panel.barchart(x, y, ...)
                    grid.raster(t(1:10/11), x=0,
                    width=x, y=y,
                    default.units="native",
                    just="left",
                    height=unit(2/37,"npc"))})
```

![plot of chunk b3](/figure/b3-1.png)

