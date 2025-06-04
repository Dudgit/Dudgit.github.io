---
layout: default
permalink: /dim_red/
title: Dimension Reduction
---


# About dimension reduction
Sometimes handling data is not that easy as it sounds. As science grows we need to process more and more data, not just in the sense of observations but also in the sense of features. Often we can find structures and outliers if we plot the dataset, but sometimes it seems impossible because of its dimensionality. TODO: Add some more motivation and explanation.


A smart approach is to find a lower dimensional space for our data (usually 2-3), where originally similar points are close to each other and the different points are far away. In dimension reduction we want to have a lower dimensional data representation which can be used for either visualization or for machine learning purposes.

Data is represented by tensors or in the simplest way with matricies. If you need some reminder (or some explanation) click [here](/linalg/). The number of rows in this matrix, means how much sample we have. 

# Principal Component Analysis (PCA)
PCA is a linear method to achieve dimension reduction. I belive in show don't tell, so let's make see the steps of this method and then try to understand it. Trust me it's going to be super easy, barely an inconvinience.

- **Standardize data**: We want to calculate statistical properties that are meaningful only if we standardize the data. Standardize mean that we subtract the mean of a feature from every element of it and dived it with it's standard deviation. \(X_i = \frac{X_i -\mu_i}{\sigma_i}\), where \(i\) is the index of the features.

- **Compute covariance matrix**: \(\Sigma_{ij} = E[(X_i-\mu_i)(X_j-\mu_j)]\).

- **Solve eigenvalue problem**: Find the eigenvectors and the corresponding eigenvectors for \(\Sigma\).

- **Select top 3-5 largest** We select the eigenvectors with the largest eigenvalues and they will be the bases for our new embedding space. We can convert all of our data into these embeddings.
