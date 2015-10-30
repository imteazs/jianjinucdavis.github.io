---
layout: post
title: Visualizing Map Data in China by Provinces in R
description: "visualizing map data in R."
modified: 2015-10-18
comments: true
share: true
tags: [visualization, R, maps]
---



I'm asked by a friend to visualize Muslim distribution in China. I accepted the task readily and excited having an opportunity to prioritize visualizing map data.

The final graph should show a map of China with color of different shapes representing density (or proportion) of musilim population for each province. Although being my first though, `ggmap` turned out to be not designed for this readily after some shallow research. I would definetely do more research to confirm this Insha'Allah. 

Fortunately, I found very informative and detailed hands-on [tutorial](http://cos.name/2009/07/drawing-china-map-using-r/) by Yixuan. BTW, this tutorial is in Chinese. Now, get our hands dirty with data!! I can't wait!

##### import data
The Data [source](http://www.360doc.com/content/14/0316/11/11971456_360980940.shtml) that I found online was of very poor formating. I decided to import it manually. The province names has to be imported in Chinese.


Briefly, here's how the data look like.

~~~r
head(Muslim_population)
~~~

~~~
##       Province Province_en Density_Muslim Distribution_Muslim
## 1       北京市     Beijing           1.76         0.011605416
## 2       天津市     Tianjin           0.20         0.008413926
## 3       河北省       Hebei           0.82         0.026353965
## 4       山西省      Shanxi           0.20         0.003046422
## 5 内蒙古自治区   Neimenggu           0.91         0.010203095
## 6       辽宁省    Liaoning           0.64         0.012911025
##   Distribution_category Density_category
## 1                     1                1
## 2                     1                0
## 3                     2                1
## 4                     1                0
## 5                     1                1
## 6                     1                1
~~~


#### import libraries

~~~r
library(maps)
library(mapdata)
library("maptools")
~~~


#### get .shp file
GPS data is needed to in order to plot province polygons. Thank [Yihui Xie](http://yihui.name/cn/2007/09/china-map-at-province-level/) for his work on researching where to get these data. Click [here](http://cos.name/wp-content/uploads/2009/07/chinaprovinceborderdata_tar_gz.zip) to download the zip file and unzip it into your working directory. The `.shp` file will be read it into R using 'maptools' and provide information on province polygons.


```r
# read .shp file
x=readShapePoly('bou2_4p.shp')
```

#### Plot a plain map of China


```r
plot(x)
```

`x` it will return a map of China if you ran it.

`x@data$NAME` are names of each province. If `x@data$NAME` showed names (in Chinese) of provinces, you don't have to do anything. If not, try convert the encodings see if names display works.


```r
x@data$NAME <- iconv(x@data$NAME, from = 'CP936', to = 'UTF-8')
```


Now we need to assign color to provinces to map our data. In the first figure, color of various shades corresponds to Muslim density for each province. In the second figure, color of various shades corresponds to the proportion of Muslim population in each province in relation to national Muslim population.


```r
densityColorCode <- data.frame(Density_category = c(0:3), 
                        Density_color = c("white", "light green", "green", "dark green"),
                        stringsAsFactors = FALSE)

density_color_df <- merge(Muslim_population, 
                  densityColorCode, 
                  by = "Density_category")

distributionColorCode <- data.frame(Distribution_category = c(0:3),
                                     Distribution_color = c("white", "#F5A9A9", "#FE2E2E", "#B40404"),
                                    stringsAsFactors = FALSE)

distribution_color_df <- merge(Muslim_population, distributionColorCode, by = "Distribution_category")
```

This function assigns colors to provinces (credit: Yixuan).

```r
getColor=function(mapdata,provname,provcol,othercol)
{
	f=function(x,y) ifelse(x %in% y,which(y==x),0)
	colIndex=sapply(mapdata@data$NAME,f,provname)
	fg=c(othercol,provcol)[colIndex+1]
	return(fg)
}
```


Now let's plot the map! `x` is our map data which tells R about province polygon information. `col` assigns colors to polygons. 

#### plot Muslim density for each province

```r

plot(x, 
     col=getColor(x, density_color_df$Province, density_color_df$Density_color, "white"), 
     xlab="",ylab="");

title("Muslim density in each province, China, 2010")
leg.txt <- c("<0.2%", "0.2-2%", "2.0%-20%", ">30%")
legend("bottom", leg.txt, horiz = TRUE, fill = densityColorCode$Density_color)
```

![plot of chunk unnamed-chunk-7](images/unnamed-chunk-7-1.png) 


#### plot distribution of Muslim population acrss China

```r

plot(x,
     col=getColor(x, 
                  distribution_color_df$Province, 
                  distribution_color_df$Distribution_color, 
                  "white"), 
     xlab="",ylab="")

title("Muslim Distribution in China, 2010")
leg.txt <- c("<0.2%", "0.2-2%", "2.0%-10%", ">50%")
legend("bottom", leg.txt, horiz = TRUE, 
       fill = distribution_color_df$Distribution_color)
```

![plot of chunk unnamed-chunk-8](images/unnamed-chunk-8-1.png) 



BTW, this [tutorial](http://bcb.dfci.harvard.edu/~aedin/courses/R/CDC/maps.html) introduced using both map and ggmap to visualize map data. 

In the next post, I'll play with ggmap. There are some REALLY REALLY cool things it can do!
