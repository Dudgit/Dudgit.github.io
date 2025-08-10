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
The other good thing about dimension reduction is that it enables visualization. Unfortunately we don't have good tools to visualize 100 dimensional data. We can define distances between them, and scientist talk about high dimensional spaces, but these seems very very abstract.
If you can turn a 100 dimensional problem into a 3 dimensional you can create nice figures about it. For example you can create a visualization of how similar countries they are to each other based on many of their attributes (like location, economy, etc).


<p align="center">
  <img src="/assets/images/dimred.png" alt="Description" width="800" height="400"/>
   <figcaption>Figure 1: The visualization of how similar countries are with a lower dimensional representation.</figcaption>
</p>
  
In the followig chapter I'll explain 2 major dimension reduction method. In reality there are many of them you can chose and maybe I'll update this later to include some more. There are methods that will be not included here, for example embedding with deep neural network, since they belong to a different section. This two method is a very good starting point in my opinion what is the basic idea behind dimension reduction.


# Principal Component Analysis (PCA)
PCA is a linear method to achieve dimension reduction. I belive in show don't tell, so let's make see the steps of this method and then try to understand it. Trust me it's going to be super easy, barely an inconvinience. I will include most of the math needed here but if you need a little bit more detailed explanation you can find [here](/linalg/)

- **Standardize data**: We want to calculate statistical properties that are meaningful only if we standardize the data.
{% include standardization.md %}


- **Compute covariance matrix**: $$\Sigma_{ij} = E[(X_i-\mu_i)(X_j-\mu_j)]$$.

- **Solve eigenvalue problem**: Find the eigenvectors and the corresponding eigenvectors for $$\Sigma$$. {% include eigenvalue.md %} Good thing that these vector are orthogonal to each other, meaning they are in a different axis.

- **Select top 3-5 largest** We select the eigenvectors with the largest eigenvalues and they will be the bases for our new embedding space. It only mean if we multiply our data points with these newly selected vectors (or put them into a matrix and do the matrix multiplication), our data points will be converted into a few dimensional version of itself, where few is determined by how much eigenvectors we chose. The new data we have is embedded, and we are happy.  
 
Intuitively every eigenvector multiplies the data by its expressiveness (or with some kind of weight) and will give us a new number which created as a weighted sum of all the features, in other words we compress all the information into one number. Using multiple eigenvectors we will arrive at a new vector that express the same information, but with much less dimension.
PCA is an effective tool to compress our data into this lower dimensional version of it. We can use it to find outliers since it's much easier to detect datapoint that are very different from the others in lower dimension.
<!---
Illustratiooooonnnn
-->
# t-SNE
The so called t-distributed Stochastic Neighbor Embedding. Even the name itself is so hard to understand you just want to skip this whole section. It happened to me when I was a student. We are in the same section so we already know that this is part of the dimension reduction/embedding part of machine learning. The problem with PCA is that some outliers can significantly reduce the visualization strength of the method. And an other thing it does not keep the hierarchical structure of our visualization. If we want to visualize how likely it is that kids will become friends and we have data like their interest, their age and their school we will probably end up with school as the most dominant feature, since other kids are less likely to meet at the first place. School (or geographical position) is a feature that is hierarchically important, but it does not determine friendship, just a good indicator if it's possible even or not. And yes there are exceptions to it too. All in all PCA is not the best for visualization, but it is very good to find outliers our use it's results as the features of a training. For visualization there is a method called t-SNE, which approaches this whole data reduction in a different way.  

Let's say I have some high dimensional data. I want to know how likely it is that a certain data chose an other data point as it's neighbor. We don't actually look for the closes points, but we want to transform the distances with a kernel (Gaussian). This can be written in the following formula:  

$$K(x_i,x_j) = exp(-\frac{|x_i -x_j|^2}{2\sigma_i^2}) $$   

Woah, we will need a little explanation. Let's start with the $$ \sigma $$ expression, which is just denotes for the standard deviation of our data, nothing fancy. The $$exp$$ is naturally the power of the Euler number $$e$$. In the numerator we can alternatively write $$||x_i -x_j||$$, which means we want to calculate the distance, but the form I wrote I think it's easy to see. Now the whole pair choosing probability (What is the probability that i will choose j as it's pair) can be written as:  
$$ p_{j|i} =  \frac{K(x_i,x_j)}{\sum_{k \neq i}K(x_i,x_k) } $$  
If we work with probabilities we want the sum of our probabilities to be 1, so the easiest way to enforce it, that we divide every element with the sum of the elements. This is what the denominator is. So what we do is calculate this probability for every element or data point and this will give us a probability distribution.   

Should we focus more on the local structures  or more on the global ones? This is very much your choice, when you are about to explore your data. To be able to tell our models what to focus on, we can define a new hyperparameter called perplexity. This is simply calculated as:  
$$Perp(P_i) = 2^{H(P_i)}$$  
where $$H(P_i)$$ is it's Shannon entropy, calculated as:
$$H(P_I) = -\sum_j p_{j|i}log_2p_{j|i}$$
So what we do is give a number to our algorithm, that will tell our model how much should it concentrate on the local or the global structures, this is the perplexity. The model will change $$\sigma$$ until our the perplexity of our distribution is the same as the perplexity we defined. Smaller perplexity will force our methods to concentrate more on the local structures.


<!---
Distribution visualization
-->

<!---
Add perplexity
-->
We are almost there, but we have to survive a little bit more maths. In the lower dimensional version we want or values to have the same distances from each other. Or not exactly that, but something with similar meaning. We want our lower dimensional data to have this same distribution of neighbors as in the high dimensional case. The problem is that using a Gaussian kernel (the one we used earlier) is usually not the best option. Let me give you an alternative, the so called Student-t distribution.  

<p align="center">
  <img src="/assets/images/gauss_student.png" alt="Description" width="800" height="400"/>
   <figcaption>Figure 2: Gaussian distribution and Student-t distribution.</figcaption>
</p>

Amazing, another way to create a slightly different figure! Understanding histograms is very easy, but tells us a lot about our data (or it's distribution). If we imagine it as an experiment on the x-axis we see what values we observed and on the y-axis we see how many times we did observe it. In other words we have the values and their quantity. But often we want it to be independent from the number of observations we had, or in other words we just want to get its density (which is just a normalized version of the count). As you can see in this case (with the right parameters) the Studen-t distribution is a bit wider and not as tall as the Gaussian (or in other name normal distribution). This means that if you transform numbers, using our new kernel, the outputs will have a bit higher probability to be a bigger number. When we want to visualize our data we want far away points to visualized far and close points to be close (in other words be as similar to the original one as possible), but we don't want them to ruin our visualization. If you put far away point too far that would make the closer point look even more close. This is called by the creators of the t-SNE algorithm as the crowding problem.   

The overall process of the algorithm is very simple. We calculate $$ p_{j|i}$$ as we discussed above. Then randomly create low dimensional points (hence the name stochastic, which is just a fancy way to say random), that will correspond to the higher dimensional points. For these we also calculate a pair choosing distribution, but with the Studen-t kernel:  

$$G(x_i,x_j) = (1+|x_i-x_j|^2)^{-1}$$  

So the new points distribution is calculated as: $$q_{j|i} = \frac{G(x_i,x_j)}{\sum_{k \neq l } G(x_i,x_k)}$$  
Naturally at the first step they will not likely to be similar, so we have to tune our low dimensional representation. Fortunately, we can compare distributions very easily. There is a metric called the Kullback-Leibler divergence, which aims to compare 2 distributions. And how much can one distribution express the other one. We compare our data with this method, which is the following calculation:  

$$KL(P||Q) = \sum_{i \neq j} p_{j|i} log(\frac{p_{j|i}}{q_{j|i}}) $$

This will give us a number, a distance or a loss, depends on you how do you want to call it. In the end we just want to minimize this loss, so change the values of the lower dimensional representation, until this expression is as low as it is possible. 

In a step-by-step guide to refresh the whole algorithm:
* Calculate p distribution with Gaussian kernel on the data we want to embed.  
* Randomly initialize lower dimensional data point (likely 2-3 dimensional).  
* Compute the q distribution with the Student-t kernel.
* Calculate the KL divergence between the two distribution.
* Change low dimensional data to make the divergence smaller.


*Note: We will not learn gradient descent here, we will talk about it in the deep learning session, so for first it will look like a bit magic.*   
<p align="right">[Next topic (clustering)](/clustering/)</p>  

[Topics](/topics/)  
[Back to Home](/)