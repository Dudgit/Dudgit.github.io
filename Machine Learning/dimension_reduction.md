---
layout: default
permalink: /dim_red/
title: Dimension Reduction
mathjax: true
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# About dimension reduction
Let's start from the beginning! In machine learning we want to process observations or so called features, that represents something in reality.
 This can be attributes of a car, gene sequences, protein levels, energy levels, pixels of a photo, etc.
 The dimension of our data simply telling us, how many number we need to describe something.
 As you would imagine this can vary based on what kind of experiment you are doing, or in general what kind of problem you want to understand.
 If you want to determine if a car is going faster than it should, you only need to measure its speed.
 This is a one dimensional problem, since we only need one number to be able to decide if the car is speeding or not.
When you want to make a simulation about the movement of planets in the solar system, you need to know their positions and masses. 
This example is a 4 dimensional problem, since we need 3 number for the positions (x,y,z) and 1 for the for the mass. Going further in this thought process if you want to work with protein levels and you need tens of hundreds of numbers to describe what's going on, you are working with high dimensional data.  
It's important to mention that the number of data you need to describe one sample is different from the number of observations you have. Going back to the planet example. If you work with a 4 dimensional problem it means you are using 4 numbers to describe the planets. You have let's say 10 planet in the solar system you are dealing with, this doesn't change the dimensionality of the problem.
It only means that you will have $$4 \times 10$$ number in your data.  
So far so good, we know the meaning of dimension, now let's take a look about dimension reduction. Example comes again! Let's say you want to decide how affordable a life in a country. You can check the cost of living and entertainment there and also how much people usually earn. To describe this you can make it into a 2 dimensional problem, but do you really have to? You can also just divide these 2 numbers to know what is the percentage of your earned money that you have to spend on living.
In general dimension reduction means that you take data and turn it into a lower dimensional one. It the example we took 2 dimensions and turned them into 1. In reality you can imagine it's usually a more significant change. 
  
Why do we want to reduce dimension? Very good question! And the answer can be multiple thing. One thing is that you can imagine that your computer has limitations. The more number it needs to process the more time it takes to do so.
If you turn your data into something lower dimensional version of it, but with the similar expressiveness (the meaning of the data remains the same), it is very likely to arrive into the same conclusion.
The other good thing about dimension reduction is that it enables visualization. Unfortunatelly we don't have good tools to visualize 100 dimensional data. We can define distances between them, and scientist talk about high dimensional spaces, but these seems very very abstract.
If you can turn a 100 dimensional problem into a 3 dimensional you can create nice figures about it. For example you can create a visualization of how similar countries they are to each other based on many of their attributes (like location, economy, etc).


<p align="center">
  <img src="/assets/images/dimred.png" alt="Description" width="800" height="400"/>
   <figcaption>Figure 1: The visualization of how similar countries are with a lower dimensional representation.</figcaption>
</p>



# Principal Component Analysis (PCA)
PCA is a linear method to achieve dimension reduction. I belive in show don't tell, so let's make see the steps of this method and then try to understand it. Trust me it's going to be super easy, barely an inconvinience. I will include most of the math needed here but if you need a little bit more detailed explanation you can find [here](/linalg/)

- **Standardize data**: We want to calculate statistical properties that are meaningful only if we standardize the data.
{% include standardization.md %}


- **Compute covariance matrix**: $$\Sigma_{ij} = E[(X_i-\mu_i)(X_j-\mu_j)]$$.

- **Solve eigenvalue problem**: Find the eigenvectors and the corresponding eigenvectors for $$\Sigma$$. {% include eigenvalue.md %} Good thing that these vector are orthogonal to each other, meaning they are in a different axis.

- **Select top 3-5 largest** We select the eigenvectors with the largest eigenvalues and they will be the bases for our new embedding space. It only mean if we multiply our data points with these newly selected vectors (or put them into a matrix and do the matrix multiplication), our data points will be converted into a few dimensional version of itself, where few is determined by how much eigenvectors we chose. The new data we have is embedded, and we are happy.  
 
PCA is an effective tool to compress our data into this lower dimensional version of it. We can use it to find outliers since it's much easier to detect datapoint that are very different from the others in lower dimension.
<!---
Illustratiooooonnnn
-->

[Back to Home](/)