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

***

* Converting a matrix of characters into numeric
{% highlight r %}
mat <- matrix(c("5","6","7","8","hello","world"),ncol=3)
class(mat) <- "numeric"
{% endhighlight %}

***

* Running the equivalent of `knitHTML` in `RStudio` on the command line. Note you must install [pandoc first](https://github.com/rstudio/rmarkdown/blob/master/PANDOC.md#newer-systems-debianubuntufedora)
{% highlight r %}
rmarkdown::render("source.Rmd")
{% endhighlight %}

***

* Passing command line arguments using `rmarkdown::render()`. Thanks to [sjackman](https://github.com/rstudio/rmarkdown/issues/319)  

**source.Rmd**
{% highlight r %}
```{r}
args <- commandArgs(trailingOnly = TRUE)
args[1]+args[2]
```
{% endhighlight %}

**script.sh**
{% highlight Bash shell scripts %}
Rscript -e 'rmarkdown::render("source.Rmd")' 0.5 0.7
{% endhighlight %}
