---
title: "Statistical Power in t tests with Unequal Group Sizes"
author: "sahir"
date: "February 25, 2016"
output: html_document
layout: post
tags: [R, ggplot2, statistics, power, sample size, t test]
permalink: power_ttest
comments: yes
---


{% highlight text %}
## Error in library(pwr): there is no package called 'pwr'
{% endhighlight %}



{% highlight text %}
## Error: could not find function "pwr.t2n.test"
{% endhighlight %}



{% highlight text %}
## Warning in seq_len(nrow(ptab)): first element used of 'length.out'
## argument
{% endhighlight %}



{% highlight text %}
## Error in seq_len(nrow(ptab)): argument must be coercible to non-negative integer
{% endhighlight %}



{% highlight text %}
## Error in `colnames<-`(`*tmp*`, value = c("id", "n1=28, n2=1406.effect size", : attempt to set 'colnames' on an object with less than two dimensions
{% endhighlight %}



{% highlight text %}
## Error in combine_vars(vars, ind_list): Position must be between 0 and n
{% endhighlight %}



{% highlight text %}
## Error in factor(temp$group, levels = c("n1=28, n2=1406", "n1=144, n2=1290", : object 'temp' not found
{% endhighlight %}


When performing [Student's t-test](https://en.wikipedia.org/wiki/Student%27s_t-test) to compare difference in means between two group, it is a useful exercise to determine the effect of unequal sample sizes in the comparison groups on power. Large imbalances generally will not have adequate statistical power to detect even large effect sizes associated with a factor, leading to a high Type II error rate as shown in the figure below:


{% highlight text %}
## Error in ggplot(temp, aes(x = `effect size`, y = power, color = group)): object 'temp' not found
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'p' not found
{% endhighlight %}

<!--more-->

To jusity this reasoning I performed a power analysis for different group sizes. I considered the following group sizes:

1. n1 = 28, n2 = 1406: n1 represents 2% of the entire sample size of 1434
2. n1 = 144, n2 = 1290: n1 represents 10% of the entire sample size of 1434
3. n1 = 287, n2 = 1147: n1 represents 20% of the entire sample size of 1434
4. n1 = 430, n2 = 1004: n1 represents 30% of the entire sample size of 1434
5. n1 = 574, n2 = 860: n1 represents 40% of the entire sample size of 1434
6. n1 = 717, n2 = 717: equal size groups (this is optimal because it leads to the highest power for a given effect size)

In the figure above we plotted the power curves for the $t$-test, as a function of the effect size, assuming a Type I error rate of 5%. 


## Code

Here is the code used to produce the above plot

<script src="https://gist.github.com/sahirbhatnagar/9507cc24983103ad9f14.js"></script>







