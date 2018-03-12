---
output:
  pdf_document: default
  html_document: default
---
R: Presenting outputs
========================================================
author: Dr N Green
date: 14th June 2016
autosize: false
width: 2440
height: 1200
css: custom.css


CRAN Task View
=========================================================

![](cran-repro-research.png)

Scatter plot: add points of different colours and symbols
========================================================
class: small-code

![](pch-table.png)

Scatter plot: add points of different colours and symbols
========================================================

`points(x, y = NULL, type = "p", ...)`


```r
x <- rnorm(10, sd=5, mean=20)
y <- 2.5*x - 1.0 + rnorm(10, sd=9, mean=0)
plot(x,y,xlab="Independent", ylab="Dependent", main="Random Stuff")

x1 <- runif(8,15,25)
y1 <- 2.5*x1 - 1.0 + runif(8,-6,6)
??

x2 <- runif(8,15,25)
y2 <- 2.5*x2 - 1.0 + runif(8,-6,6)
??
```

![plot of chunk unnamed-chunk-2](R-plots-msc-figure/unnamed-chunk-2-1.png)




Scatter plot: legend
========================================================

`legend(x, y = NULL, legend, fill = NULL, col = par("col"),
       border = "black", lty, lwd, pch,
       angle = 45, density = NULL, bty = "o", bg = par("bg"),
       box.lwd = par("lwd"), box.lty = par("lty"), box.col = par("fg"),
       pt.bg = NA, cex = 1, pt.cex = cex, pt.lwd = lwd,
       xjust = 0, yjust = 1, x.intersp = 1, y.intersp = 1,
       adj = c(0, 0.5), text.width = NULL, text.col = par("col"),
       text.font = NULL, merge = do.lines && has.pch, trace = FALSE,
       plot = TRUE, ncol = 1, horiz = FALSE, title = NULL,
       inset = 0, xpd, title.col = text.col, title.adj = 0.5,
       seg.len = 2)'


```r
plot(x,y,xlab="Independent",ylab="Dependent",main="Random Stuff")
points(x1,y1,col=2,pch=3)
points(x2,y2,col=4,pch=5)
???
```

![plot of chunk unnamed-chunk-5](R-plots-msc-figure/unnamed-chunk-5-1.png)



Simple fitted lines
========================================================

`abline(a = NULL, b = NULL, h = NULL, v = NULL, reg = NULL,
       coef = NULL, untf = FALSE, ...)`
       
`lm(formula, data, subset, weights, na.action,
   method = "qr", model = TRUE, x = FALSE, y = FALSE, qr = TRUE,
   singular.ok = TRUE, contrasts = NULL, offset, ...)`
   
`lowess(x, y = NULL, f = 2/3, iter = 3, delta = 0.01 * diff(range(x)))`


```r
x <- rnorm(10,sd=5,mean=20)
y <- 2.5*x - 1.0 + rnorm(10,sd=9,mean=0)
x2 <- runif(8,15,25)
y2 <- 2.5*x2 - 1.0 + runif(8,-6,6)

plot(x,y,xlab="Independent",ylab="Dependent",main="Random Stuff")
points(x1,y1,col=2,pch=3)
points(x2,y2,col=4,pch=5)
legend(25,80,c("Original","one","two"),col=c(1,2,4),pch=c(1,3,5))

???
```

![plot of chunk unnamed-chunk-8](R-plots-msc-figure/unnamed-chunk-8-1.png)


With error lines
========================================================

`arrows(x0, y0, x1 = x0, y1 = y0, length = 0.25, angle = 30,
       code = 2, col = par("fg"), lty = par("lty"),
       lwd = par("lwd"), ...)`
       

```r
plot(x,y,xlab="Independent",ylab="Dependent",main="Random Stuff")
xHigh <- x
yHigh <- y + abs(rnorm(10,sd=3.5))
xLow <- x
yLow <- y - abs(rnorm(10,sd=3.1))
???
```

![plot of chunk unnamed-chunk-11](R-plots-msc-figure/unnamed-chunk-11-1.png)



Adding jitter
========================================================


```r
numberWhite <- ??
numberChipped <- ??

par(mfrow=c(1,2))
plot(numberWhite,numberChipped,xlab="Number White Marbles Drawn",
ylab="Number Chipped Marbles Drawn",main="Pulling Marbles")
plot(jitter(numberWhite),jitter(numberChipped),xlab="Number White Marbles Drawn",
ylab="Number Chipped Marbles Drawn",main="Pulling Marbles With Jitter")
```

![plot of chunk unnamed-chunk-14](R-plots-msc-figure/unnamed-chunk-14-1.png)



Mosaic plots
========================================================

`table(...,
      exclude = if (useNA == "no") c(NA, NaN),
      useNA = c("no", "ifany", "always"),
      dnn = list.names(...), deparse.level = 1)`
      

```r
mosaicplot(??, main="sixth plot")
```

![plot of chunk unnamed-chunk-17](R-plots-msc-figure/unnamed-chunk-17-1.png)




Pair-wise scatter plots
========================================================


```r
uData <- rnorm(20)
vData <- rnorm(20,mean=5)
wData <- uData + 2*vData + rnorm(20,sd=0.5)
xData <- -2*uData+rnorm(20,sd=0.1)
yData <- 3*vData+rnorm(20,sd=2.5)

pairs(?)
```

![plot of chunk unnamed-chunk-20](R-plots-msc-figure/unnamed-chunk-20-1.png)




Shaded areas
========================================================

`polygon(x, y = NULL, density = NULL, angle = 45,
        border = NULL, col = NA, lty = par("lty"),
        ..., fillOddEven = FALSE)`
        

```r
stdDev <- 0.75; x <- seq(-5,5,by=0.01); y <- dnorm(x,sd=stdDev)
right <- qnorm(0.95,sd=stdDev)
plot(x,y,type="l",xaxt="n",ylab="p",xlab=expression(paste('Assumed Distribution of',bar(x))),axes=FALSE,ylim=c(0,max(y)*1.05),xlim=c(min(x),max(x)),frame.plot=FALSE)
axis(1,at=c(-5,right,0,5), pos = c(0,0),labels=c(expression(' '),expression(bar(x)[cr]),expression(mu[0]),expression(' ')))
axis(2)
xReject <- seq(right,5,by=0.01);  yReject <- dnorm(xReject,sd=stdDev)
polygon(???, col='red')
```


![plot of chunk unnamed-chunk-23](R-plots-msc-figure/unnamed-chunk-23-1.png)



Different types of lines
========================================================

`par(..., no.readonly = FALSE)`


```r
x <- c(1:5); y <- x
par(pch=22, col="red")
par(mfrow=c(2,4))
opts = ???
for(i in 1:length(opts)){
heading = paste("type=",opts[i])
plot(x, y, type="n", main=heading)
lines(x, y, type=opts[i])
}
```

![plot of chunk unnamed-chunk-26](R-plots-msc-figure/unnamed-chunk-26-1.png)



Barplot
========================================================

`barplot(height, width = 1, space = NULL,
        names.arg = NULL, legend.text = NULL, beside = FALSE,
        horiz = FALSE, density = NULL, angle = 45,
        col = NULL, border = par("fg"),
        main = NULL, sub = NULL, xlab = NULL, ylab = NULL,
        xlim = NULL, ylim = NULL, xpd = TRUE, log = "",
        axes = TRUE, axisnames = TRUE,
        cex.axis = par("cex.axis"), cex.names = par("cex.axis"),
        inside = TRUE, plot = TRUE, axis.lty = 0, offset = 0,
        add = FALSE, args.legend = NULL, ...)`
        

```r
numberWhite <- rhyper(30,4,5,3)
numberWhite <- as.factor(numberWhite)

???
```


```
numberWhite
 0  1  2  3 
 5 12 12  1 
```

![plot of chunk unnamed-chunk-29](R-plots-msc-figure/unnamed-chunk-29-1.png)




plotly
========================================================


[plotly website here](https://plot.ly/r)



ggplot2: structure
========================================================

`ggplot(data = <default data set>,
       aes(x = <default x axis variable>,
           y = <default y axis variable>,
           ... <other default aesthetic mappings>),
       ... <other plot defaults>) +
       geom_<geom type>(aes(size = <size variable for this geom>,
                      ... <other aesthetic mappings>),
                  data = <data for this point geom>,
                  stat = <statistic string or function>,
                  position = <position string or function>,
                  color = <"fixed color specification">,
                  <other arguments, possibly passed to the _stat_ function) +
  scale_<aesthetic>_<type>(name = <"scale label">,
                     breaks = <where to put tick marks>,
                     labels = <labels for tick marks>,
                     ... <other options for the scale>) +
  theme(plot.background = element_rect(fill = "gray"),
        ... <other theme elements>)`

qplot: overlapping densities
========================================================

`qplot(x, y = NULL, ..., data, facets = NULL, margins = FALSE,
  geom = "auto", xlim = c(NA, NA), ylim = c(NA, NA), log = "",
  main = NULL, xlab = deparse(substitute(x)),
  ylab = deparse(substitute(y)), asp = NA, stat = NULL, position = NULL)`
  

```r
library(ggplot2)
data("mtcars")
mtcars$gear <- factor(mtcars$gear,levels=c(3,4,5), labels=c("3gears","4gears","5gears"))
mtcars$am <- factor(mtcars$am,levels=c(0,1), labels=c("Automatic","Manual"))
mtcars$cyl <- factor(mtcars$cyl,levels=c(4,6,8), labels=c("4cyl","6cyl","8cyl"))

qplot(mpg,
      data = ??,
      geom = ??,
      fill = ??,
      alpha = ??,
      main = "Distribution of Gas Milage", xlab="Miles Per Gallon", ylab="Density")
```

![plot of chunk unnamed-chunk-32](R-plots-msc-figure/unnamed-chunk-32-1.png)



qplot: facets and points
========================================================


```r
library(ggplot2)
data("mtcars")
mtcars$gear <- factor(mtcars$gear,levels=c(3,4,5), labels=c("3gears","4gears","5gears"))
mtcars$am <- factor(mtcars$am,levels=c(0,1), labels=c("Automatic","Manual"))
mtcars$cyl <- factor(mtcars$cyl,levels=c(4,6,8), labels=c("4cyl","6cyl","8cyl"))

qplot(??,
      ??,
      data=mtcars, shape=, color=, facets=gear~cyl, size=I(3), xlab="Horsepower", ylab="Miles per Gallon")
```

![plot of chunk unnamed-chunk-35](R-plots-msc-figure/unnamed-chunk-35-1.png)



hist vs geom_histogram
========================================================

[Rgraphics tutorial here](http://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html)


```r
par(mfrow=c(2,1))
hist(diamonds$carat)
hist(diamonds$carat, breaks = 500)
```

![plot of chunk unnamed-chunk-37](R-plots-msc-figure/unnamed-chunk-37-1.png)



ggplot2: Box plot and points with legend
========================================================


```r
plot(carat ~ clarity,
     data=subset(diamonds, cut == "Good"))
points(carat ~ clarity, col="red",
       data=subset(diamonds, cut == "Ideal"))
legend(0,3,
       c("Good", "Ideal"), title="cut",
       col=c("black", "red"),
       pch=c(1, 1))
```

![plot of chunk unnamed-chunk-39](R-plots-msc-figure/unnamed-chunk-39-1.png)

ggplot2
========================================================


```r
ggplot(subset(diamonds, cut %in% c("Good", "Ideal")),
       aes(x=clarity,
           y=carat,
           color=cut))+
  geom_point()
```

![plot of chunk unnamed-chunk-40](R-plots-msc-figure/unnamed-chunk-40-1.png)

Symbols 
========================================================


```r
## A look at all 25 symbols
df2 <- data.frame(x = 1:5 , y = 1:25, z = 1:25)
s <- ggplot(df2, aes(x = x, y = y))
s + geom_point(aes(shape = z), size = 4) + scale_shape_identity()
```

![plot of chunk unnamed-chunk-41](R-plots-msc-figure/unnamed-chunk-41-1.png)

```r
## While all symbols have a foreground colour, symbols 19-25 also take a
## background colour (fill)
```

Symbols (2)
========================================================


```r
s + geom_point(aes(shape = z), size = 4, colour = "Red") +
  scale_shape_identity()
```

![plot of chunk unnamed-chunk-42](R-plots-msc-figure/unnamed-chunk-42-1.png)

Symbols (3)
========================================================


```r
s + geom_point(aes(shape = z), size = 4, colour = "Red", fill = "Black") +
  scale_shape_identity()
```

![plot of chunk unnamed-chunk-43](R-plots-msc-figure/unnamed-chunk-43-1.png)

ColorBrewer2
========================================================

[ColorBrewer2](http://colorbrewer2.org)


Manipulate
========================================================

[manipulate examples](https://support.rstudio.com/hc/en-us/articles/200551906-Interactive-Plotting-with-Manipulate)








Options()
========================================================
* Sets and reports options. Lots of them.
*  
* `digits` from 3.1415927 using `options(digits = 2)` to 3.14
* Report value using e.g. `getOption("digits")`
*  
* `scipen()`

```eval
R> ran2 <- c(1.810032e+09, 4) 
R> options("scipen"=-100, "digits"=4)
R> ran2
[1] 1.81e+09 4.00e+00
R> options("scipen"=100, "digits"=4)
R> ran2
[1] 1810032000
```



Kable::
========================================================


```r
library(knitr)
kable(head(iris), format = "latex")
```


\begin{tabular}{r|r|r|r|l}
\hline
Sepal.Length & Sepal.Width & Petal.Length & Petal.Width & Species\\
\hline
5.1 & 3.5 & 1.4 & 0.2 & setosa\\
\hline
4.9 & 3.0 & 1.4 & 0.2 & setosa\\
\hline
4.7 & 3.2 & 1.3 & 0.2 & setosa\\
\hline
4.6 & 3.1 & 1.5 & 0.2 & setosa\\
\hline
5.0 & 3.6 & 1.4 & 0.2 & setosa\\
\hline
5.4 & 3.9 & 1.7 & 0.4 & setosa\\
\hline
\end{tabular}

```r
kable(head(iris), format = "html")
```

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 5.1 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.4 </td>
   <td style="text-align:right;"> 0.2 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4.9 </td>
   <td style="text-align:right;"> 3.0 </td>
   <td style="text-align:right;"> 1.4 </td>
   <td style="text-align:right;"> 0.2 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4.7 </td>
   <td style="text-align:right;"> 3.2 </td>
   <td style="text-align:right;"> 1.3 </td>
   <td style="text-align:right;"> 0.2 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4.6 </td>
   <td style="text-align:right;"> 3.1 </td>
   <td style="text-align:right;"> 1.5 </td>
   <td style="text-align:right;"> 0.2 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5.0 </td>
   <td style="text-align:right;"> 3.6 </td>
   <td style="text-align:right;"> 1.4 </td>
   <td style="text-align:right;"> 0.2 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5.4 </td>
   <td style="text-align:right;"> 3.9 </td>
   <td style="text-align:right;"> 1.7 </td>
   <td style="text-align:right;"> 0.4 </td>
   <td style="text-align:left;"> setosa </td>
  </tr>
</tbody>
</table>

printr::
========================================================


```r
x = matrix(rnorm(40), 5)

dimnames(x) = list(NULL, head(LETTERS, ncol(x)))

knitr::kable(x, digits = 2,
             caption = "A table produced by printr.")
```



|     A|     B|     C|     D|     E|     F|     G|     H|
|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|
|  0.65| -2.14|  0.43|  0.09| -0.69| -1.74| -1.05|  0.12|
| -0.60|  1.00| -1.08| -0.16|  1.53|  1.77|  0.36| -1.18|
| -0.59|  0.39|  0.36|  1.67|  0.43|  0.33|  1.69| -0.08|
|  0.07| -0.31| -0.25|  0.28|  1.41| -1.87| -1.87| -0.74|
| -1.51| -0.74| -2.01| -1.20| -0.03|  0.23|  0.28|  0.90|


Tables
========================================================


```r
library(xtable)

options(xtable.floating = FALSE)
options(xtable.timestamp = "")

data(tli)

xtable(tli[1:10, ])
```

```
% latex table generated in R 3.3.3 by xtable 1.8-2 package
% 
\begin{tabular}{rrlllr}
  \hline
 & grade & sex & disadvg & ethnicty & tlimth \\ 
  \hline
1 &   6 & M & YES & HISPANIC &  43 \\ 
  2 &   7 & M & NO & BLACK &  88 \\ 
  3 &   5 & F & YES & HISPANIC &  34 \\ 
  4 &   3 & M & YES & HISPANIC &  65 \\ 
  5 &   8 & M & YES & WHITE &  75 \\ 
  6 &   5 & M & NO & BLACK &  74 \\ 
  7 &   8 & F & YES & HISPANIC &  72 \\ 
  8 &   4 & M & YES & BLACK &  79 \\ 
  9 &   6 & M & NO & WHITE &  88 \\ 
  10 &   7 & M & YES & HISPANIC &  87 \\ 
   \hline
\end{tabular}
```

GLMs
========================================================


```r
fm3 <- glm(disadvg ~ ethnicty*grade, data = tli, family = binomial)
xtable(fm3)
```

```
% latex table generated in R 3.3.3 by xtable 1.8-2 package
% 
\begin{tabular}{rrrrr}
  \hline
 & Estimate & Std. Error & z value & Pr($>$$|$z$|$) \\ 
  \hline
(Intercept) & 3.1888 & 1.5966 & 2.00 & 0.0458 \\ 
  ethnictyHISPANIC & -0.2848 & 2.4808 & -0.11 & 0.9086 \\ 
  ethnictyOTHER & 212.1701 & 22122.7093 & 0.01 & 0.9923 \\ 
  ethnictyWHITE & -8.8150 & 3.3355 & -2.64 & 0.0082 \\ 
  grade & -0.5308 & 0.2892 & -1.84 & 0.0665 \\ 
  ethnictyHISPANIC:grade & 0.2448 & 0.4357 & 0.56 & 0.5742 \\ 
  ethnictyOTHER:grade & -32.6014 & 3393.4687 & -0.01 & 0.9923 \\ 
  ethnictyWHITE:grade & 1.0171 & 0.5185 & 1.96 & 0.0498 \\ 
   \hline
\end{tabular}
```


Flat tables
========================================================


```r
data(mtcars)
mtcars$cyl <- factor(mtcars$cyl, levels = c("4","6","8"),
labels = c("four","six","eight"))
tbl <- ftable(?, row.vars = c(2, 4), dnn = c("Cylinders", "V/S", "Transmission", "Gears"))
tbl
xftbl <- xtableFtable(tbl)
print.xtableFtable(xftbl)
```


```
          Cylinders    four    six    eight   
          Transmission    0  1   0  1     0  1
V/S Gears                                     
0   3                     0  0   0  0    12  0
    4                     0  0   0  2     0  0
    5                     0  1   0  1     0  2
1   3                     1  0   2  0     0  0
    4                     2  6   2  0     0  0
    5                     0  1   0  0     0  0
```

```
% latex table generated in R 3.3.3 by xtable 1.8-2 package
% 
\begin{tabular}{lll |rrrrrr}
  \hline
     &       & Cylinders    & \multicolumn{1}{l}{ four} & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{ six} & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{ eight} & \multicolumn{1}{l}{   } \\ 
      &       & Transmission & \multicolumn{1}{l}{    0} & \multicolumn{1}{l}{  1} & \multicolumn{1}{l}{   0} & \multicolumn{1}{l}{  1} & \multicolumn{1}{l}{     0} & \multicolumn{1}{l}{  1} \\ 
  V/S & Gears &              & \multicolumn{1}{l}{     } & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{    } & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{      } & \multicolumn{1}{l}{   } \\ 
   \hline
0   & 3     &              &    0 &  0 &   0 &  0 &    12 &  0 \\ 
      & 4     &              &    0 &  0 &   0 &  2 &     0 &  0 \\ 
      & 5     &              &    0 &  1 &   0 &  1 &     0 &  2 \\ 
  1   & 3     &              &    1 &  0 &   2 &  0 &     0 &  0 \\ 
      & 4     &              &    2 &  6 &   2 &  0 &     0 &  0 \\ 
      & 5     &              &    0 &  1 &   0 &  0 &     0 &  0 \\ 
   \hline
\end{tabular}
```

Flat tables
========================================================


```r
data(mtcars)
mtcars$cyl <- factor(mtcars$cyl, levels = c("4","6","8"),
labels = c("four","six","eight"))
tbl <- ftable(mtcars$cyl, mtcars$vs, mtcars$am, mtcars$gear, row.vars = c(2, 4), dnn = c("Cylinders", "V/S", "Transmission", "Gears"))
tbl
```

```
          Cylinders    four    six    eight   
          Transmission    0  1   0  1     0  1
V/S Gears                                     
0   3                     0  0   0  0    12  0
    4                     0  0   0  2     0  0
    5                     0  1   0  1     0  2
1   3                     1  0   2  0     0  0
    4                     2  6   2  0     0  0
    5                     0  1   0  0     0  0
```

```r
xftbl <- xtableFtable(tbl)
print.xtableFtable(xftbl)
```

```
% latex table generated in R 3.3.3 by xtable 1.8-2 package
% 
\begin{tabular}{lll |rrrrrr}
  \hline
     &       & Cylinders    & \multicolumn{1}{l}{ four} & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{ six} & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{ eight} & \multicolumn{1}{l}{   } \\ 
      &       & Transmission & \multicolumn{1}{l}{    0} & \multicolumn{1}{l}{  1} & \multicolumn{1}{l}{   0} & \multicolumn{1}{l}{  1} & \multicolumn{1}{l}{     0} & \multicolumn{1}{l}{  1} \\ 
  V/S & Gears &              & \multicolumn{1}{l}{     } & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{    } & \multicolumn{1}{l}{   } & \multicolumn{1}{l}{      } & \multicolumn{1}{l}{   } \\ 
   \hline
0   & 3     &              &    0 &  0 &   0 &  0 &    12 &  0 \\ 
      & 4     &              &    0 &  0 &   0 &  2 &     0 &  0 \\ 
      & 5     &              &    0 &  1 &   0 &  1 &     0 &  2 \\ 
  1   & 3     &              &    1 &  0 &   2 &  0 &     0 &  0 \\ 
      & 4     &              &    2 &  6 &   2 &  0 &     0 &  0 \\ 
      & 5     &              &    0 &  1 &   0 &  0 &     0 &  0 \\ 
   \hline
\end{tabular}
```

Markdown tables
========================================================


```r
library(pander)
pandoc.table(tli)
```

```

-------------------------------------------
 grade   sex   disadvg   ethnicty   tlimth 
------- ----- --------- ---------- --------
   6      M      YES     HISPANIC     43   

   7      M      NO       BLACK       88   

   5      F      YES     HISPANIC     34   

   3      M      YES     HISPANIC     65   

   8      M      YES      WHITE       75   

   5      M      NO       BLACK       74   

   6      F      NO       BLACK       82   

   4      M      NO       WHITE       69   

   3      F      YES     HISPANIC     17   

   3      M      NO      HISPANIC     37   

   7      M      NO       WHITE       83   

   6      M      YES     HISPANIC     78   

   6      F      NO       WHITE       84   
-------------------------------------------
```

```r
pandoc.table(tli, style="rmarkdown")
```

```


|  grade  |  sex  |  disadvg  |  ethnicty  |  tlimth  |
|:-------:|:-----:|:---------:|:----------:|:--------:|
|    6    |   M   |    YES    |  HISPANIC  |    43    |
|    7    |   M   |    NO     |   BLACK    |    88    |
|    5    |   F   |    YES    |  HISPANIC  |    34    |
|    6    |   F   |    NO     |   WHITE    |    91    |
|    5    |   F   |    NO     |   WHITE    |    50    |
|    7    |   M   |    NO     |   WHITE    |    83    |
|    4    |   F   |    YES    |   BLACK    |    58    |
|    4    |   M   |    YES    |  HISPANIC  |    85    |
|    7    |   F   |    NO     |   WHITE    |    52    |
|    5    |   M   |    NO     |   WHITE    |    86    |
|    4    |   F   |    YES    |   BLACK    |    79    |
|    8    |   M   |    NO     |   WHITE    |    48    |
|    5    |   M   |    NO     |   WHITE    |    91    |
|    3    |   M   |    YES    |  HISPANIC  |    89    |
|    7    |   F   |    NO     |   WHITE    |    91    |
|    5    |   F   |    YES    |   WHITE    |    79    |
|    7    |   M   |    NO     |   WHITE    |    83    |
|    6    |   M   |    YES    |  HISPANIC  |    78    |
|    6    |   F   |    NO     |   WHITE    |    84    |
```

Other HTML table
========================================================


```r
library("htmlTable")
htmlTable(tli)
```

<!--html_preserve--><table class='gmisc_table' style='border-collapse: collapse; margin-top: 1em; margin-bottom: 1em;' >
<thead>
<tr>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey;'> </th>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;'>grade</th>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;'>sex</th>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;'>disadvg</th>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;'>ethnicty</th>
<th style='border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;'>tlimth</th>
</tr>
</thead>
<tbody>
<tr>
<td style='text-align: left;'>1</td>
<td style='text-align: center;'>6</td>
<td style='text-align: center;'>M</td>
<td style='text-align: center;'>YES</td>
<td style='text-align: center;'>HISPANIC</td>
<td style='text-align: center;'>43</td>
</tr>
<tr>
<td style='text-align: left;'>2</td>
<td style='text-align: center;'>7</td>
<td style='text-align: center;'>M</td>
<td style='text-align: center;'>NO</td>
<td style='text-align: center;'>BLACK</td>
<td style='text-align: center;'>88</td>
</tr>
<tr>
<td style='text-align: left;'>99</td>
<td style='text-align: center;'>6</td>
<td style='text-align: center;'>M</td>
<td style='text-align: center;'>YES</td>
<td style='text-align: center;'>HISPANIC</td>
<td style='text-align: center;'>78</td>
</tr>
<tr>
<td style='border-bottom: 2px solid grey; text-align: left;'>100</td>
<td style='border-bottom: 2px solid grey; text-align: center;'>6</td>
<td style='border-bottom: 2px solid grey; text-align: center;'>F</td>
<td style='border-bottom: 2px solid grey; text-align: center;'>NO</td>
<td style='border-bottom: 2px solid grey; text-align: center;'>WHITE</td>
<td style='border-bottom: 2px solid grey; text-align: center;'>84</td>
</tr>
</tbody>
</table><!--/html_preserve-->

```r
library(hwriter)
hwrite(tli, border=0)
```

```
[1] "<table border=\"0\">\n<tr>\n<td>grade</td><td>sex</td><td>disadvg</td><td>ethnicty</td><td>tlimth</td></tr>\n<tr>\n<td>6</td><td>M</td><td>YES</td><td>HISPANIC</td><td>43</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>BLACK</td><td>88</td></tr>\n<tr>\n<td>5</td><td>F</td><td>YES</td><td>HISPANIC</td><td>34</td></tr>\n<tr>\n<td>3</td><td>M</td><td>YES</td><td>HISPANIC</td><td>65</td></tr>\n<tr>\n<td>8</td><td>M</td><td>YES</td><td>WHITE</td><td>75</td></tr>\n<tr>\n<td>5</td><td>M</td><td>NO</td><td>BLACK</td><td>74</td></tr>\n<tr>\n<td>8</td><td>F</td><td>YES</td><td>HISPANIC</td><td>72</td></tr>\n<tr>\n<td>4</td><td>M</td><td>YES</td><td>BLACK</td><td>79</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>88</td></tr>\n<tr>\n<td>7</td><td>M</td><td>YES</td><td>HISPANIC</td><td>87</td></tr>\n<tr>\n<td>3</td><td>M</td><td>NO</td><td>WHITE</td><td>79</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>84</td></tr>\n<tr>\n<td>8</td><td>M</td><td>NO</td><td>WHITE</td><td>90</td></tr>\n<tr>\n<td>5</td><td>M</td><td>NO</td><td>WHITE</td><td>73</td></tr>\n<tr>\n<td>8</td><td>F</td><td>NO</td><td>WHITE</td><td>72</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>BLACK</td><td>82</td></tr>\n<tr>\n<td>4</td><td>M</td><td>NO</td><td>WHITE</td><td>69</td></tr>\n<tr>\n<td>3</td><td>F</td><td>YES</td><td>HISPANIC</td><td>17</td></tr>\n<tr>\n<td>3</td><td>M</td><td>NO</td><td>HISPANIC</td><td>37</td></tr>\n<tr>\n<td>5</td><td>M</td><td>NO</td><td>WHITE</td><td>70</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>90</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>5</td><td>F</td><td>NO</td><td>WHITE</td><td>50</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>WHITE</td><td>83</td></tr>\n<tr>\n<td>4</td><td>F</td><td>YES</td><td>BLACK</td><td>58</td></tr>\n<tr>\n<td>4</td><td>M</td><td>YES</td><td>HISPANIC</td><td>85</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>52</td></tr>\n<tr>\n<td>5</td><td>M</td><td>NO</td><td>WHITE</td><td>86</td></tr>\n<tr>\n<td>4</td><td>F</td><td>YES</td><td>BLACK</td><td>79</td></tr>\n<tr>\n<td>8</td><td>M</td><td>NO</td><td>WHITE</td><td>48</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>BLACK</td><td>63</td></tr>\n<tr>\n<td>8</td><td>F</td><td>YES</td><td>WHITE</td><td>88</td></tr>\n<tr>\n<td>3</td><td>F</td><td>YES</td><td>HISPANIC</td><td>76</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>WHITE</td><td>79</td></tr>\n<tr>\n<td>8</td><td>M</td><td>NO</td><td>WHITE</td><td>87</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>HISPANIC</td><td>80</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>66</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>WHITE</td><td>68</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>92</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>57</td></tr>\n<tr>\n<td>8</td><td>F</td><td>NO</td><td>WHITE</td><td>57</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>WHITE</td><td>66</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>BLACK</td><td>88</td></tr>\n<tr>\n<td>8</td><td>F</td><td>NO</td><td>BLACK</td><td>59</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>87</td></tr>\n<tr>\n<td>4</td><td>M</td><td>YES</td><td>BLACK</td><td>59</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>WHITE</td><td>88</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>HISPANIC</td><td>75</td></tr>\n<tr>\n<td>5</td><td>M</td><td>YES</td><td>HISPANIC</td><td>93</td></tr>\n<tr>\n<td>7</td><td>M</td><td>YES</td><td>BLACK</td><td>77</td></tr>\n<tr>\n<td>3</td><td>M</td><td>NO</td><td>WHITE</td><td>85</td></tr>\n<tr>\n<td>3</td><td>F</td><td>NO</td><td>WHITE</td><td>84</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>80</td></tr>\n<tr>\n<td>3</td><td>M</td><td>YES</td><td>BLACK</td><td>80</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>90</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>BLACK</td><td>85</td></tr>\n<tr>\n<td>5</td><td>F</td><td>YES</td><td>HISPANIC</td><td>63</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>BLACK</td><td>59</td></tr>\n<tr>\n<td>6</td><td>M</td><td>YES</td><td>WHITE</td><td>85</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>OTHER</td><td>92</td></tr>\n<tr>\n<td>8</td><td>M</td><td>NO</td><td>HISPANIC</td><td>51</td></tr>\n<tr>\n<td>6</td><td>F</td><td>YES</td><td>OTHER</td><td>87</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>92</td></tr>\n<tr>\n<td>8</td><td>F</td><td>NO</td><td>WHITE</td><td>85</td></tr>\n<tr>\n<td>8</td><td>M</td><td>YES</td><td>BLACK</td><td>47</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>WHITE</td><td>78</td></tr>\n<tr>\n<td>8</td><td>M</td><td>YES</td><td>HISPANIC</td><td>86</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>WHITE</td><td>86</td></tr>\n<tr>\n<td>3</td><td>F</td><td>NO</td><td>BLACK</td><td>67</td></tr>\n<tr>\n<td>3</td><td>M</td><td>YES</td><td>BLACK</td><td>64</td></tr>\n<tr>\n<td>5</td><td>M</td><td>YES</td><td>HISPANIC</td><td>86</td></tr>\n<tr>\n<td>5</td><td>F</td><td>NO</td><td>WHITE</td><td>80</td></tr>\n<tr>\n<td>4</td><td>M</td><td>YES</td><td>BLACK</td><td>81</td></tr>\n<tr>\n<td>3</td><td>M</td><td>NO</td><td>WHITE</td><td>70</td></tr>\n<tr>\n<td>8</td><td>F</td><td>NO</td><td>WHITE</td><td>82</td></tr>\n<tr>\n<td>5</td><td>F</td><td>NO</td><td>WHITE</td><td>69</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>79</td></tr>\n<tr>\n<td>3</td><td>F</td><td>YES</td><td>BLACK</td><td>67</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>3</td><td>F</td><td>YES</td><td>HISPANIC</td><td>91</td></tr>\n<tr>\n<td>4</td><td>F</td><td>YES</td><td>HISPANIC</td><td>78</td></tr>\n<tr>\n<td>5</td><td>F</td><td>NO</td><td>WHITE</td><td>86</td></tr>\n<tr>\n<td>4</td><td>F</td><td>NO</td><td>WHITE</td><td>87</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>83</td></tr>\n<tr>\n<td>5</td><td>F</td><td>NO</td><td>WHITE</td><td>93</td></tr>\n<tr>\n<td>3</td><td>M</td><td>YES</td><td>BLACK</td><td>70</td></tr>\n<tr>\n<td>4</td><td>M</td><td>YES</td><td>BLACK</td><td>86</td></tr>\n<tr>\n<td>6</td><td>F</td><td>YES</td><td>BLACK</td><td>87</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>83</td></tr>\n<tr>\n<td>6</td><td>F</td><td>YES</td><td>BLACK</td><td>75</td></tr>\n<tr>\n<td>6</td><td>M</td><td>NO</td><td>WHITE</td><td>88</td></tr>\n<tr>\n<td>5</td><td>M</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>3</td><td>M</td><td>YES</td><td>HISPANIC</td><td>89</td></tr>\n<tr>\n<td>7</td><td>F</td><td>NO</td><td>WHITE</td><td>91</td></tr>\n<tr>\n<td>5</td><td>F</td><td>YES</td><td>WHITE</td><td>79</td></tr>\n<tr>\n<td>7</td><td>M</td><td>NO</td><td>WHITE</td><td>83</td></tr>\n<tr>\n<td>6</td><td>M</td><td>YES</td><td>HISPANIC</td><td>78</td></tr>\n<tr>\n<td>6</td><td>F</td><td>NO</td><td>WHITE</td><td>84</td></tr>\n</table>\n"
```


R and Word
========================================================

* `rtf::`


```r
library(rtf)
output <- "rtf_vignette.doc"
rtf <- RTF(output,width=8.5,height=11,font.size=10,omi=c(1,1,1,1))
done(rtf)
```

make new section

```r
addHeader(rtf,title="Section Header", subtitle="This is the subheading or section text.")
```
add paragraph

```r
addParagraph(rtf,"This is a new self-contained paragraph.\n")
```


```r
addNewLine(rtf)
addParagraph(rtf,"Normal, \\b this is bold\\b0, normal.\n")
addParagraph(rtf,"Normal, {\\b\\i bold-italic}, normal.\n")
```

add a table

```r
tab <- as.data.frame(head(iris)) # create a data.frame
colnames(tab)<-gsub("\\."," ",colnames(tab)) # format column names
addTable(rtf,tab,font.size=9,row.names=FALSE,NA.string="-")
```

R and Word (2)
========================================================

add plot

```r
addPlot(rtf,plot.fun=plot,width=6,height=6,res=300, iris[,1],iris[,2])
```


```r
addPageBreak(rtf, width=8.5, height=11, omi=c(1,1,1,1))
addSessionInfo(rtf)
done(rtf)
```

rtf output
========================================================

![](rtf-doc.png)


ReporteRs::
========================================================
 * http://davidgohel.github.io/ReporteRs/index.html
