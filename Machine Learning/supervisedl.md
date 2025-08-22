---
layout: default
permalink: /suplearn/
title: Supervised learning
mathjax: true
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

In machine learning we are usually distinguish 2 major types of training:
- **Unsupervised learning**: The examples we just see before, when we simply try to find some inner structure in the data, without having any knowledge about that structure. Try to find the relation between points, based on metrics we defined.  
- **Supervised learning**: In this case we already know this relationship and we want to create a model, that can approximate it well. In contrast to unsupervised learning we have labeled data, meaning we know what the results should be, so we will change our method until it gives back the best possible results.  

This sounds a bit dumb, for the first time. Why would I want to learn the function that describes a relationship if I already know that? The truth is, we often don't know what is the exact policy to get the right labels from the corresponding features. Imagine the oldest example, that everybody uses for machine learning (I'm the same it seems XD). You have images of cats and dogs and you want to write a program that can decide which animal is in the picture. This is not a too complicated task for a human, very small children can easily tell you, yet if you want to program this...that would be a plenty of work. There are of course a lot of differences, for example their ears, their sizes, the shape of their face, etc. If you want to have a program that can do this for you, it has to take a lot of these into consideration, find these parts of the animals on the picture, since an animal can be anywhere in the image, and based on that compute what is the animal. This sounds a pretty long and (for me at least) impossible to program without machine learning.  

To make it simple, in supervised learning we have a data that consist of parts:
- **Features**: This is the observation, the dimensionality of the data. It can be protein levels in patients or the pixels of an image, attributes of a car, etc.  
- **Targets**: Or in other words the labels, is what we want to approximate with our models. This can be the type of animal that is on the picture, the max speed of a car, estimated price of a house, probability of student become the friend of an other one, etc.  

With these labeled data, we can define a so called hypothesis function, such as:
$$ \hat{y} = h(\theta,X) $$.  

This means that we make an approximation to the labels $$ \hat{y} $$, that small hat is just a fancy way to express that it should be the same dimension as the labels, that are represented with $$ y $$, but we only try to approximate them with our model. The model we want to use for approximation is the $$h(\theta,X)$$ or often written as $$h_{\theta}(X)$$, this means that our model is trying to approximate the target from the features we had, but the model itself has its own parameters, and these are represented with the $$\theta$$.
*Note: Theta and X don't represent single values, we just use them with one parameter for simpler and more general notation. Both of them can be any finite number.*  

In the [next section](/linreg/) we will talk about linear regression with more depths, I will talk a little bit about it anyways so you can understand supervised learning more easily. The most simple version of supervised learning when we want to approximate a one dimensional linear relationship.  
$$\hat{y} = h(\theta,x) = w_0 + x \cdot w_1 $$.
Wait, wait, wait. I'm using $$\theta$$ for the function, yet in the other side there are $$w_0,w_1$$, where are they come from? As I said earlier, $$\theta$$ contains all the parameters of the model in itself, so it's more convenient to write it like this. With only 2 parameters it's okay but imagine it with hundreds or thousands or even more (as we will see later in deep learning). To sum it up, $$\theta$$ is just a notation that this model will have some parameters and we will store them in one variable. Now as we cleared this up, let's understand the original equation. The target is approximated with the multiple of the feature and some extra correction constant. Imagine that you have to convert Fahrenheit to Celsius. The equation for that is:
$$C = (F-32)\cdot \frac{5}{9} = F\cdot \frac{5}{9} - 32\frac{5}{9}$$

[Back to Home](/)