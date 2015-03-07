---
layout: page
title: "R tips"
comments: yes
---

> Here I present some `R` tips and tricks I have learned from various resources over the years.

***

* For math styles in `R` plots. Thanks to [@RLangTip](https://twitter.com/RLangTip)
{% highlight r %}
demo(plotmath)
{% endhighlight %}

* Converting a matrix of characters into numeric
{% highlight r %}
mat <- matrix(c("5","6","7","8","hello","world"),ncol=3)
class(mat) <- "numeric"
{% endhighlight %}
