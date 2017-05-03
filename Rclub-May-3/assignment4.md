title: "assignment4"
author: "huiyingmiao"
date: "2017年4月29日"
output: html_document
---




```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

## R Markdown
## 3.6 Geometric objects
# left

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](assignment4_files/figure-html/unnamed-chunk-2-1.png)<!-- -->
# right

```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
## 3.6.1 Exercises
###1. What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?
geom_smooth(),geom_density(),geom_freqpoly();geom_boxplot();geom_histogram();geom_area(),geom_polygon().
###2.  

```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-4-1.png)<!-- -->
how about se?

###3. show.legend hasn't been shown before...   
###4.

```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

se=false----only show the core line~

###5. They are same.

```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-6-1.png)<!-- -->


```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

###6.Recreate the R code necessary to generate the following graphs.


```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(size=5) + 
  geom_smooth( group = drv,se=FALSE)  
group should be in the bracket as following, or code won't work.


```
## `geom_smooth()` using method = 'loess'
```

![](assignment4_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

