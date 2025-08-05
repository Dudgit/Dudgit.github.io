---
layout: default
permalink: /clustering/
title: Clustering methods
mathjax: true
---
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# About clustering
Clustering is an umbrella term for algorithms that will do unsupervised classification. Unsupervised meaning that the results are not definitive, they are not labelled. Similarly to [dimension reduction](/dim_red/) we can't test our results in validation dataset, to be able tell how good our method is. Although we can have metrcis to approximate how good our method is, but more about this later.

# K-means
This method is so easy I'm not even sure you will ever get here to read it. In K-means the parameter of our model is how many clusters I want to end up. The number of clusters is denoted by K. For simplicity let's say this is three, so K=3. We have our data that we want to cluster and we place 3 (or K in general) points randomly in their space. If they are 2 dimensional points we will choose 2 numbers as their position, if they are 6 dimensional points we will 6 numbers as their position and so on. After we dropped these points, often called centroiods, we will calculate the distance of every data points from these new points. Based on the distance of the 3 new points we will label every original data. Every point will belong to a cluster of a centroid, that is the closest to them. The cluster positions are defined randomly in the beginning, so we have to do something to optimize it right. For the next step we will calculate the mean of every of the positions of every cluster and place a new centroid there. We will calculate the distances again, re-label the data points and repeat the whole process until the centroid of the clusters are converged.  

It is important to mention, that this method can be very sensitive to outliers or different scaling. Imagine if you want to cluster weapons based on their attributes, like damage, attack speed, crit chance, crit hit modifier. Playing a game or an early stage of an MMO, where your damage is 2, your attack speed is 1.25 hit/second, you have 0.8 crit chance and 1.5 crit hit modifier or values similar to these the clustering would work very well. But if you are playing an RPG in a later stage, where damage can be in an insane magnitude, while crit chance is between 0-1 and crit hit modifier is also in a lower magnitude around 1.5-3, the distance you calculate will always be determined by the damage. The other sensitivity is outliers, since if you put a point with extremely high values, the center of one of the clusters will be moved more toward to that. Imagine if every value is in between 0-10 and there is an extremely high value, like $$10^6$$. This would move the mean of one of the clusters, maybe so much that points, that would originally belong there would become part of other clusters. This is iteratively can ruin a complete cluster. To avoid these kind of problems:

 - **Visualiza and analzye**: Often you can find a big outlier if you just look at some visualization. Or you can find statistical incoherence.
 - **Know your data**: This is partially belong the the previous advice, but having domain knowledge will always help you understand if these points are meaningful or you just need to drop them.
 - **Standardize**: As I gather more and more experience in machine learning I start to belive it's always a go to. If you standardize your data, you will get rid of the different scaling problem.
# Hierarchical
This one is super easy, since it does not require tons of equations. In hierarchical clustering we start from a lot of data points, which we want to connect into clusters. As the first step we connect every data point with its closest neighbor. We will repeat this step until we arrive with one big cluster, that includes ever point. We only have to decide what should we call distance when we have more than one data point. - Keep in mind having 1 data point means only 1 observed data, it does not specify the dimensionality of the points, these can be vectors with 100 or 1000 entries. - The most common approach is just to use the Euclidean distance of these new clusters, which is:  

$$ 
d(a, b) = \sqrt{\sum_i(a_i-b_i)^2},
$$  

Where $$a$$ and $b$ are cluster of data points and $$i$$ indexing through their elements. If it makes sense to your work, you can define different metrics, like the average of all possible pair distance or the closest two element between 2 clusters. The only question is, when should I stop building these clusters? 
<!---
Illustratiooooonnnn
 We just define a good distance metric and we start to connect things. Defining distances is a new thing to you? Fear no more, if you got so far this one will be a peace of cake. Naturally when we are talking about distance we talk about the Euclidean distance, which is the square root of the summed square distances. Meaning that if I have a data point with multiple dimension and I want to check it's distance from an other one I calculate the following:
$$
d(a, b) = \sqrt{\sum_i(a_i-b_i)^2},
$$
where i is just the index to go through every dimension of our data points, $$a$$ and $$b$$ are the data points that I want to compare. This is the metric people usually use, but just because it's the most common doesn't mean it's the only one.  
-->
# Metrics
In clustering a common problem is how to determine the number of clusters we will create. I will tell you about two methods that are very popular. The firs one is the so called Elbow method.



[Back to Home](/)