---
layout: page
title: "Software"
---

* [acm4r](http://cran.r-project.org/web/packages/acm4r/index.html)  
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/acm4r)](https://cran.r-project.org/package=acm4r) ![](http://cranlogs.r-pkg.org/badges/grand-total/acm4r?color=blue)
Fragment lengths or molecular weights from pairs of lanes are compared, and a number of matching bands are calculated using the Align-and-Count Method.

* [eclust](http://sahirbhatnagar.com/eclust/)  
A Statistical Software Tool for the Analysis of High-Dimensional Interactions. This software is written in the open source software environment R. It's main functionality is to fit statistical models for analyzing interactions between a high dimensional dataset (e.g. genomics, brain imaging), the environment and a response.

* [casebase](http://sahirbhatnagar.com/casebase/)  
This software is written in the open source software environment R. It's main functionality is to fit smooth-in-time parametric hazard functions using case-base sampling. This approach allows the explicit inclusion of the time variable into the model, which enables the user to fit a wide class of parametric hazard functions. For example, including time linearly recovers the Gompertz hazard, whereas including time logarithmically recovers the Weibull hazard; not including time at all corresponds to the exponential hazard. This is joint work with [Maxime Turgeon](http://turgeonmaxime.github.io/), [Olli Saarela](http://individual.utoronto.ca/osaarela/) and [James Hanley](http://www.medicine.mcgill.ca/epidemiology/hanley/)

* [manhattanly](https://cran.r-project.org/web/packages/manhattanly/)
[![Travis-CI Build Status](https://travis-ci.org/sahirbhatnagar/manhattanly.svg?branch=master)](https://travis-ci.org/sahirbhatnagar/manhattanly) [![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/manhattanly)](https://cran.r-project.org/package=manhattanly) ![](http://cranlogs.r-pkg.org/badges/grand-total/manhattanly?color=blue)
Create interactive Q-Q and manhattan plots that are usable from the R console, in the 'RStudio' viewer pane, in 'R Markdown' documents, and in 'Shiny' apps. Hover the mouse pointer over a point to show details or drag a rectangle to zoom. A manhattan plot is a popular graphical method for visualizing results from high-dimensional data analysis such as a (epi)genome wide association study (GWAS or EWAS), in which p-values, Z-scores, test statistics are plotted on a scatter plot against their genomic position. Manhattan plots are used for visualizing potential regions of interest in the genome that are associated with a phenotype. Interactive manhattan plots allow the inspection of specific value (e.g. rs number or gene name) by hovering the mouse over a cell, as well as zooming into a region of the genome (e.g. a chromosome) by dragging a rectangle around the relevant area. This work is based on the 'qqman' package by Stephen Turner and the 'plotly.js' engine. It produces similar manhattan and Q-Q plots as the 'manhattan' and 'qq' functions in the 'qqman' package, with the advantage of including extra annotation information and interactive web-based visualizations directly from R. Once uploaded to a 'plotly' account, 'plotly' graphs (and the data behind them) can be viewed and modified in a web browser.