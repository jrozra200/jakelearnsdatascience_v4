---
title: Prime Number Patterns
author: Jacob Rozran
date: '2017-01-20'
slug: prime-number-patterns
categories:
  - Data Visualization
  - Prime Numbers
tags:
  - data visualization
  - prime numbers
  - R
  - plotly
  - D3.js
---

I found a very 
[thought provoking and beautiful visualization](https://www.jasondavies.com/primos/) 
on the [D3 Website](https://d3js.org/) regarding prime numbers. What the 
visualization shows is that if you draw periodic curves beginning at the origin 
for each positive integer, the prime numbers will be intersected by only two 
curves: the prime itself's curve and the curve for one.

When I saw this, my mind was blown. How interesting... and also how obvious. The 
definition of a prime is that it can only be divided by itself and one (duh). 
This is a visualization of that fact. The patterns that emerge are stunning.

I wanted to build the data and visualization for myself in R. While not as 
spectacular as the original I found, it was still a nice adventure. I used 
[Plotly](https://plot.ly/feed/) to visualize the data. The code can be found on 
[github](https://github.com/jrozra200/prime_number_patterns/blob/master/making_periodic_curves.R). 
Here is the [visualization](https://plot.ly/~rozran00/130):

<center>
![Prime Number Patterns](/img/prime_number_patterns/130.png)
</center>