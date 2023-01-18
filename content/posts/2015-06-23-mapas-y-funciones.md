---
title: Mapas y funciones
author: JeronimoCarranza
date: '2015-06-29'
slug: 2015-06-29-mapas-y-funciones
categories: 
  - charlas
  - grupo
tags:
  - mapas
  - funciones
---


La última reunión fuimos poquitos, pero estuvo muy interesante. Miguel Ángel e Irene nos enseñaron a hacer mapas en R. Y Fran dio una clase maestra de por qué, cómo y cuándo hacer nuestras propias funciones. Dejo sus presentaciones enlazadas aquí: [Mapas](/posts/2015-06-23-mapas-y-funciones/representar-puntos.pdf) y [Funciones](/posts/2015-06-23-mapas-y-funciones/funciones_r_fbalao.pdf).

Nos tomaos un descanso por vacaciones, y nos vemos en Septiembre, seguramente para optimizar código de alguno de nosotros en “real-time”. Si alguien tiene código que vaya lento, o que no funcione del todo, es la oportunidad para ponerlo a punto entre todos.

Aquí el código que usó Irene:

```
library(maps)
```

```
## using the function maps () you can choose the longitude and latitude of interest

map(database="world") ##map of the World
map(database="world",xlim = c(-10, 5), ylim = c(35, 45)) # Map of Iberian Peninsula
```

```
##########
# draw.tropics
# draws lines (in the sea only) for the tropic of cancer and capricorn based on units of lat and long

draw.tropics = function(color = "grey", ltype = 2, lwidth = 0, ...){
 lines(c(-180, -106.5), c(23.5, 23.5), col = color, lty = ltype, lwd = lwidth) # tropic of cancer
 lines(c(-98, -16), c(23.5, 23.5), col = color, lty = ltype, lwd = lwidth)
 lines(c(59, 68), c(23.5, 23.5), col = color, lty = ltype, lwd = lwidth) 
 lines(c(117, 180), c(23.5, 23.5), col = color, lty = ltype, lwd = lwidth)
 lines(c(-180, -71), c(-23.5, -23.5), col = color, lty = ltype, lwd = lwidth) # tropic of capricorn
 lines(c(-47, 15), c(-23.5, -23.5), col = color, lty = ltype, lwd = lwidth)
 lines(c(36, 113), c(-23.5, -23.5), col = color, lty = ltype, lwd = lwidth) 
 lines(c(151, 180), c(-23.5, -23.5), col = color, lty = ltype, lwd = lwidth)
}
#####
```

```
##long and lat are two vectors with longitude and latitude of 20 localities of study in the Neotropics
long=c(-37.33333, -72.36100, -52.65000, -83.71806,
 -60.18300, -47.30222, -84.48056, -47.58333,
 -41.40283, -45.07750, -36.73417, -41.20000,
 -80.25000, -61.83333, -69.81667, -38.19583,
 -38.32111, -49.31700, -76.94300 ,-44.83300)

lat=c(-6.583333, -0.489000, -17.816667,
 9.515000, -2.610000 ,-24.543333,
 10.086111, -22.511111, -12.561408,
 -23.538167, -8.468056, -18.766667,
 -4.268056, -16.216667, 11.666667,
 -8.311944, -7.983333, -25.425000,
 17.874000 ,-23.366000)
```

```
##map of the Neotropics (using a tif format)
tiff(filename="map1.tif",height=1100,width=1500,pointsize=60)
maps::map("world", interior = FALSE,fill = FALSE, col = "grey40",lwd = lwdlen, xlim = c(-110, -30), ylim = c(-27, 27))
draw.tropics(lwidth = 3)
```

```
#we plot the 20 localities in the map
points(x = long, y = lat, pch=21, bg = "white", cex = 0.5) #draw circles for labels
for (i in seq(1,20,2)) text(x = long[i]-1, y = lat[i]-1, labels = i, cex = 0.25) #labels with the locality number
for (i in seq(2,20,2)) text(x = long[i]+1, y = lat[i]+1, labels = i, cex = 0.25) #labels with the locality number
```

```
dev.off()
```

