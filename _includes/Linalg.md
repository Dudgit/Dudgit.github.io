---
layout: default
permalink: /linalg/
title: Basics of Linear Algebra
mathjax: true
---



<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>


# Standardization

Standardize mean that we subtract the mean of a feature from every element of it and dived it with it's standard deviation. $$X_i = \frac{X_i -\mu_i}{\sigma_i}$$, where $$i$$ is the index of the features. What it does it will make the mean of our data 0 while it's deviation to 1. If you substract a number from all other data point the new mean will be smaller with that number, therefore if you use the original mean you will end up with a new dataset having 0 mean. Same logic applies to the standard devaiation and we arrive to the equation.


# Angle between vectors
This is a super basic math concept people learn in their ealry studies. Yet we will see that this will lead many-many great deep learning concept.


# Covariance
To understand covariance matrix you will have to understand 