---
title: "Limma Moderated and Ordinary t-statistics"
author: "sahir"
date: "February 7, 2017"
output: html_document
layout: post
tags: [R, statistics, t test, genomics, limma]
permalink: limma_ttest
comments: yes
---

When analyzing large amounts of genetic and genomic data, the first line of analysis is usually some sort of univariate test. That is, conduct a statistical test for each SNP or CpG site or Gene and then correct for multiple testing. The [limma](https://bioconductor.org/packages/release/bioc/html/limma.html) package on Bioconductor is a popular method for computing _moderated_ t-statistics using a combination of the `limma::lmFit` and `limma::eBayes` functions. In this post, I show how to calculate the _ordinary_ t-statistics from `limma` output.


<!--more-->




First we load the required packages

{% highlight r %}
# clear workspace
rm(list=ls())

if (!requireNamespace("pacman", quietly = TRUE)) 
  install.packages("pacman")

# this will install (if you dont already have it) and load the package
pacman::p_load("minfi")
pacman::p_load("minfiData")
pacman::p_load("limma")
pacman::p_load("CpGassoc")

# check the data that is available in the minfiData package
pacman::p_data("minfiData")
{% endhighlight %}



{% highlight text %}
##   Data        Description                                                                           
## 1 MsetEx      An example dataset for Illumina's Human Methylation 450k dataset, after preprocessing.
## 2 MsetEx.sub  An example dataset for Illumina's Human Methylation 450k dataset, after preprocessing.
## 3 RGsetEx     An example dataset for Illumina's Human Methylation 450k dataset.                     
## 4 RGsetEx.sub An example dataset for Illumina's Human Methylation 450k dataset.
{% endhighlight %}

Next, we extract some sample data and create a covariate of interest

{% highlight r %}
# get the M-values for the sample data
DT <- minfi::getM(MsetEx.sub)

dim(DT)
{% endhighlight %}



{% highlight text %}
## [1] 600   6
{% endhighlight %}



{% highlight r %}
# rows are CpGs and columns are samples
head(DT)
{% endhighlight %}



{% highlight text %}
##            5723646052_R02C02 5723646052_R04C01 5723646052_R05C02
## cg00050873          3.502348         0.4414491          4.340695
## cg00212031         -3.273751         0.9234662         -2.614777
## cg00213748          2.076816        -0.1309465          1.260995
## cg00214611         -3.438838         1.7463950         -2.270551
## cg00455876          1.839010        -0.9927320          1.619479
## cg01707559         -3.303987        -0.6433201         -3.540887
##            5723646053_R04C02 5723646053_R05C02 5723646053_R06C02
## cg00050873        0.24458355        -0.3219281         0.2744392
## cg00212031       -0.21052257        -0.6861413        -0.1397595
## cg00213748       -1.10373279        -1.6616553        -0.1270869
## cg00214611        0.29029649        -0.2103599        -0.6138630
## cg00455876       -0.09504721        -0.2854655         0.6361273
## cg01707559       -0.74835377        -0.4678048        -1.1345421
{% endhighlight %}



{% highlight r %}
# create a fake covariate. 3 intact and 3 degraded samples
tissue <- factor(c(rep("Intact",3), rep("Degraded",3)))
design <- model.matrix(~ tissue)
{% endhighlight %}

Then we calculate the moderated and ordinary t-statistics and compare them:

{% highlight r %}
# limma fit
fit <- lmFit(DT, design)
fit_ebayes <- eBayes(fit)

# ordinary t-statistic
ordinary.t <- fit$coefficients[,"tissueIntact"] / 
  fit$stdev.unscaled[,"tissueIntact"] / 
  fit$sigma

plot(x = ordinary.t, 
     y = fit_ebayes$t[,"tissueIntact"], 
     xlab = "ordinary t-statistic", 
     ylab = "moderated t-statistic")
abline(a = 0, b = 1, col = "red")
{% endhighlight %}

![plot of chunk unnamed-chunk-2](/figure/posts/2017-02-07-ttest_limma/unnamed-chunk-2-1.png)


We can calculate the corresponding p-values from the ordinary t-statistics. This is given by 

{% highlight r %}
# t-distribution with n-p-1 degrees of freedom 
# (n: number of samples, p:number of covariates excluding intercept)
ordinary.pvalue <- pt(q = abs(ordinary.t), 
                      df = dim(DT)[2]-(ncol(design)-1)-1, 
                      lower.tail = F) * 2
{% endhighlight %}

We can also use the [`CpGassoc`](https://cran.r-project.org/package=CpGassoc) package to calculate ordinary t-statistics and compare the result to our manual calculations:


{% highlight r %}
# compare result with CpGassoc package (regular t-test)
t_test_mvalues <- CpGassoc::cpg.assoc(
  beta.val = minfi::getBeta(MsetEx.sub),
  indep = tissue,
  fdr.cutoff = 0.05,
  logit.transform = TRUE)

# these should be equal
plot(t_test_mvalues$results$P.value, ordinary.pvalue)
abline(a = 0, b = 1, col = "red")
{% endhighlight %}

![plot of chunk unnamed-chunk-4](/figure/posts/2017-02-07-ttest_limma/unnamed-chunk-4-1.png)

{% highlight r %}
# t-statistic is the squared F.statistic (in certain cases) 
plot(t_test_mvalues$results$F.statistic, ordinary.t^2)
abline(a = 0, b = 1, col = "red")
{% endhighlight %}

![plot of chunk unnamed-chunk-4](/figure/posts/2017-02-07-ttest_limma/unnamed-chunk-4-2.png)




