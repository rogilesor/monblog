---
title: "extraire une légende d'un graphe ggplot2"
date: 2017-11-10T18:08:02+01:00
draft: true
tags: [ "programmation", "R", "legend", "ggplot2","ggally"]
categories: ["r_language"]
---

Ce post explique comment isoler une légende d'un graphique fait avec ggplot2.
<!--more-->

# Comment extraire une légende d'un graphique sous ggplot2 ?

Il faut utiliser le package GGally qui fournit des fonctions très utiles. Pour extraire une légende, il faut utiliser la fonction grab_legend. 

Par exemple :


```r
library(ggplot2)
library(GGally)
```

```
## Error in library(GGally): there is no package called 'GGally'
```

```r
histPlot <- qplot(
  x = Sepal.Length,
  data = iris,
  fill = Species,
  geom = "histogram",
  binwidth = 1/4
)
(right <- histPlot)
```

![plot of chunk grab_legend](figure/grab_legend-1.png)

```r
grab_legend(right)
```

```
## Error in eval(expr, envir, enclos): impossible de trouver la fonction "grab_legend"
```

# Comment enregistrer cette légende au format svg ?

Il faut utiliser les package grid et gridSVG :


```r
require(grid)
require(gridSVG)

vp <- viewport(x = 0.5,y = 0.5,width = 1,height = 1)
pushViewport(vp)

grab_legend(right)
```

```
## Error in eval(expr, envir, enclos): impossible de trouver la fonction "grab_legend"
```

```r
grid.export("legend_grab.svg")
```

![plot of chunk grab_legend_svg](figure/grab_legend_svg-1.png)![plot of chunk grab_legend_svg](figure/grab_legend_svg-2.png)

