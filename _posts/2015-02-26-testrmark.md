---
title: "Testing RMarkdown"
author: "sahir"
date: '2015-02-26'
layout: post
comments: True
permalink: LaTeX-Jekyll
---

\newcommand{\mb}[1]{\mathbf{#1}}
\newcommand{\dnorm}[3]{\frac{1}{\sqrt{2\pi #3}} \expp{- \frac{\left( #1-#2\right) ^2}{2 #3}}  }
\newcommand{\dpois}[3]{\frac{\exp\left(-#2\right) #3 }{#1 !}}

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

<!--Continue-->
When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

$$ \mathbf{X}\_{n,p} = \mathbf{A}\_{n,k} \mathbf{B}\_{k,p} $$


Let $$Y_1,\ldots,Y_n$$ be a random sample from the 2 component Poisson mixture for $$y \in \mathbb{R}$$, with rates $$\theta_1,\theta_2$$ and mixing parameter $$0<\omega<1$$. Denote the vector of rate parameters $$\theta = (\theta_1,\theta_2)$$.
$$ f_{Y|\theta,\omega}(y|\theta,\omega) = \omega  + (1-\omega)$$

Let $$X_1, \ldots,X_n$$ be the unobserved data such that $$P(X_i=1)=\omega$$ and $$P(X_i=2)=1-\omega$$. The complete likelihood function is given by:
$$
\begin{align*}
\mathcal{L}_{\mb{X},\mb{Y}}(\theta,\omega|\mb{x},\mb{y}) &= \prod\limits_{i=1}^{n}\left[  \omega  \dpois{y_i}{\theta_1}{\theta_1^{y_i}}     \right]^{\mathbbm{1}_{\left\lbrace 1\right\rbrace }(x_i)} \left[  (1-\omega)  \dpois{y_i}{\theta_2}{\theta_2^{y_i}}     \right]^{\mathbbm{1}_{\left\lbrace 2\right\rbrace }(x_i)}    
\end{align*}
$$
And the complete log-likelihood (up-to a constant) is given by:
$$
\begin{equation}
\ell_{\mb{X},\mb{Y}}(\theta,\omega|\mb{x},\mb{y}) = \sumn \mathbbm{1}_{\left\lbrace 1\right\rbrace }(x_i)  \left[ \log \omega - \theta_1 + y_i \log \theta_1  \right] +\mathbbm{1}_{\left\lbrace 2\right\rbrace }(x_i)  \left[ \log(1-\omega) - \theta_2 + y_i \log \theta_2  \right]  \label{eq:logfmr2}
\end{equation}
$$




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

You can also embed plots, for example:

![plot of chunk cars](/figure/posts/2015-02-26-testrmark/cars-1.png) 

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

|                  |  mpg| cyl|  disp|  hp| drat|    wt|  qsec| vs| am| gear| carb|
|:-----------------|----:|---:|-----:|---:|----:|-----:|-----:|--:|--:|----:|----:|
|Mazda RX4         | 21.0|   6| 160.0| 110| 3.90| 2.620| 16.46|  0|  1|    4|    4|
|Mazda RX4 Wag     | 21.0|   6| 160.0| 110| 3.90| 2.875| 17.02|  0|  1|    4|    4|
|Datsun 710        | 22.8|   4| 108.0|  93| 3.85| 2.320| 18.61|  1|  1|    4|    1|
|Hornet 4 Drive    | 21.4|   6| 258.0| 110| 3.08| 3.215| 19.44|  1|  0|    3|    1|
|Hornet Sportabout | 18.7|   8| 360.0| 175| 3.15| 3.440| 17.02|  0|  0|    3|    2|
|Valiant           | 18.1|   6| 225.0| 105| 2.76| 3.460| 20.22|  1|  0|    3|    1|
|Duster 360        | 14.3|   8| 360.0| 245| 3.21| 3.570| 15.84|  0|  0|    3|    4|
|Merc 240D         | 24.4|   4| 146.7|  62| 3.69| 3.190| 20.00|  1|  0|    4|    2|
|Merc 230          | 22.8|   4| 140.8|  95| 3.92| 3.150| 22.90|  1|  0|    4|    2|
|Merc 280          | 19.2|   6| 167.6| 123| 3.92| 3.440| 18.30|  1|  0|    4|    4|
