---
title: "Advanced Bioinformatics 2019 Assessment"
author: '9507'
date: "9 May 2019"
output: 
  html_document:
    keep_md: true

---



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

## Including Plots

You can also embed plots, for example:

![](Durr-e-Maknoon_Tariq_9507_Advanced_Bioinformatics_Assignment_2019_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

## Task 1

```r
sum(5:55)
```

```
[1] 1530
```

## Task 2

```r
sumfun <- function(n) {sum(5:n)}
sumfun(10)
```

```
[1] 45
```

```r
sumfun(20)
```

```
[1] 200
```

```r
sumfun(100)
```

```
[1] 5040
```

## Task3

```r
Fibonacci <-numeric(12)
Fibonacci[1] <- Fibonacci[2] <- 1
for(i in 3:12) {Fibonacci[i] <- Fibonacci[i-2] + Fibonacci[i-1] }
print(Fibonacci)
```

```
 [1]   1   1   2   3   5   8  13  21  34  55  89 144
```
## Task4

```r
library(ggplot2)
data("mtcars")
Gear <- as.factor(mtcars$gear) 
ggplot(mtcars, aes(x=Gear, y=mpg, fill=Gear)) + geom_boxplot(alpha=0.3)
```

![](Durr-e-Maknoon_Tariq_9507_Advanced_Bioinformatics_Assignment_2019_files/figure-html/unnamed-chunk-4-1.png)<!-- -->


## Task 5

```r
distance <- lm(formula = dist ~ speed, data = cars)
summary(distance)
```

```

Call:
lm(formula = dist ~ speed, data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-29.069  -9.525  -2.272   9.215  43.201 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) -17.5791     6.7584  -2.601   0.0123 *  
speed         3.9324     0.4155   9.464 1.49e-12 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 15.38 on 48 degrees of freedom
Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
```
Task 5 answers:  

Fitted slope = 3.9324  

Intercept = -17.5791  

Standard deviation: Dist = 6.7584, speed = 0.4155  

## Task 6

```r
library(ggplot2)
data("cars")
ggplot(cars, aes(x=speed, y=dist)) + 
  geom_point(color='#2980B9', size = 4) + xlim(c(0, 25)) + 
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE, color='#2C3E50') + 
  labs(title='Linear relationship between speed and the breaking distance', x='Speed in mph', y='Breaking Distance in feet')
```

![](Durr-e-Maknoon_Tariq_9507_Advanced_Bioinformatics_Assignment_2019_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

## Task 7 (Part 1)

```r
library(ggplot2)
data("cars")
new_speed <- cars$speed * (5280/3600)
lm_1 <- lm(dist ~ 0 + new_speed + I(new_speed^2), cars)
summary(lm_1)
```

```

Call:
lm(formula = dist ~ 0 + new_speed + I(new_speed^2), data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-28.836  -9.071  -3.152   4.570  44.986 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)   
new_speed       0.84479    0.38180   2.213  0.03171 * 
I(new_speed^2)  0.04190    0.01366   3.067  0.00355 **
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 15.02 on 48 degrees of freedom
Multiple R-squared:  0.9133,	Adjusted R-squared:  0.9097 
F-statistic: 252.8 on 2 and 48 DF,  p-value: < 2.2e-16
```
Yes. We get reasonable results because 0.84479 is the slope of the line which in our case represents average reaction speed. It seems like a realistic average reaction speed for the driver to start breaking. 

## Task 7 (Part 2)

```r
y <- cars$dist
x <- cars$new_speed
ggplot(cars, aes(new_speed, dist)) + geom_point() + geom_smooth(method='lm', formula="y~0+x+I(x^2)") + labs(title ="Average reaction time for driver to start breaking", x="New Speed in seconds", y="Distance in feet")
```

![](Durr-e-Maknoon_Tariq_9507_Advanced_Bioinformatics_Assignment_2019_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

