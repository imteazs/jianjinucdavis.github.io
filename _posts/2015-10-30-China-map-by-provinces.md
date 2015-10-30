---
layout: post
title: Plotting China Map by Provinces
modified: 2015-10-30
comments: true
share: true
tags: [visualization, map]
---



A friend asked me to plot Muslim distribution in China for his presentation on "History and Culture of Chinese Muslims". Well, what a great opportunity to learn map visualization! 

It begins with Data [source](http://www.360doc.com/content/14/0316/11/11971456_360980940.shtml). Oh messy messy data...


Here's how the clean data looked like.

~~~
##       Province Province_en Density_Muslim Distribution_Muslim
## 1       北京市     Beijing           1.76         0.011605416
## 2       天津市     Tianjin           0.20         0.008413926
## 3       河北省       Hebei           0.82         0.026353965
## 4       山西省      Shanxi           0.20         0.003046422
## 5 内蒙古自治区   Neimenggu           0.91         0.010203095
## 6       辽宁省    Liaoning           0.64         0.012911025
##   Distribution_category Density_category
## 1                     1                2
## 2                     0                0
## 3                     1                1
## 4                     0                0
## 5                     1                1
## 6                     1                1
~~~

### import libraries

{% highlight r %}
library(maps)
library(mapdata)
library("maptools")
{% highlight r %}


GPS data, contained in ".shp" file, provides information on map polygons. ".shp" file can be read using R package `maptools`. Download [GPS data on China provinces](http://cos.name/wp-content/uploads/2009/07/chinaprovinceborderdata_tar_gz.zip) and unzip it into your working directory. Thank [Yihui](http://yihui.name/cn/2007/09/china-map-at-province-level/) for researching data sources. 

### read .shp file

{% highlight r %}
x=readShapePoly('bou2_4p.shp')
{% endhighlight %}


`x@data$NAME` gives province names. I have to convert the encoding for normal display. Don't worry about it if yours' look good naturally.

{% highlight r %}
x@data$NAME <- iconv(x@data$NAME, from = 'CP936', to = 'UTF-8')
{% endhighlight %}


Before assigning colors to provinces (polygons) to map the data, I used `RColorBrewer` **to choose colors of gradient scales** representing variations in data.


{% highlight r %}
# more colors: http://www.r-bloggers.com/color-palettes-in-r/
library(RColorBrewer)
mypalette_density<-brewer.pal(3,"Greens")
mypalette_distribution<-brewer.pal(3,"YlOrRd")
{% endhighlight %}

In the first figure, color shades corresponds to Muslim density for each province. In the second figure, color shades corresponds to Muslim distribution across China. I created `color code dataframes` in which colors shades I chose corresponded to designated category of density (or distribution). Merge the `color code dataframes` with raw data by designated category will allow us to generate new data frames in which color codes corresponded to each provinces.

{% highlight r %}
densityColorCode <- data.frame(Density_category = c(0:3), 
                        Density_color = c("white", mypalette_density),
                        stringsAsFactors = FALSE)

density_color_df <- merge(Muslim_population, 
                  densityColorCode, 
                  by = "Density_category")

distributionColorCode <- data.frame(Distribution_category = c(0:3),
                                     Distribution_color = c("white",mypalette_distribution),
                                    stringsAsFactors = FALSE)


distribution_color_df <- merge(Muslim_population, distributionColorCode, by = "Distribution_category")
{% endhighlight %}

This function is used to assign color to provinces.
{% highlight r %}
# Function credit: Yixuan
getColor=function(mapdata,provname,provcol,othercol)
{
	f=function(x,y) ifelse(x %in% y,which(y==x),0)
	colIndex=sapply(mapdata@data$NAME,f,provname)
	fg=c(othercol,provcol)[colIndex+1]
	return(fg)
}
{% endhighlight %}

Now let's plot the map! `x` is our map data which tells R about province polygon information. `col` assigns colors to polygons. 

#### plot Muslim density for each province

{% highlight r %}
plot(x, 
     col=getColor(x, density_color_df$Province, density_color_df$Density_color, "white"), 
     xlab="",ylab="")

title("Muslim density in each province, China, 2010")
leg.txt <- c("<0.2%", "0.2-1%", "1.0%-5%", ">5%")
legend("bottom", leg.txt, horiz = TRUE, fill = densityColorCode$Density_color)
{% endhighlight %}

![plot of chunk unnamed-chunk-6](images/unnamed-chunk-6-1.png) 


#### plot distribution of Muslim population across China

{% highlight r %}
plot(x,
     col=getColor(x, 
                  distribution_color_df$Province, 
                  distribution_color_df$Distribution_color, 
                  "white"), 
     xlab="",ylab="")

title("Muslim Distribution in China, 2010")
leg.txt <- c("<1%", "1-5%", "5%-10%", ">10%")
legend("bottom", leg.txt, horiz = TRUE, 
       fill = distributionColorCode$Distribution_color)
{% highlight r %}

![plot of chunk unnamed-chunk-7](images/unnamed-chunk-7-1.png) 


Now we have our maps! Have fun playing with map data! 

#### additional resources:

This [tutorial](http://bcb.dfci.harvard.edu/~aedin/courses/R/CDC/maps.html) introduced using both map and ggmap to visualize map data in R. 
