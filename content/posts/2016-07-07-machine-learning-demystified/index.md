---
title: Machine Learning Demystified
author: Jacob Rozran
date: '2016-07-07'
slug: machine-learning-demystified
categories:
  - Machine Learning
  - Data Science
tags:
  - machine learning
  - data science
  - supervised learning
  - unsupervised learning
---

*The differences and applications of Supervised and Unsupervised Machine Learning.*

### Introduction

**Machine learning** is one of the buzziest terms thrown around in technology 
these days. Combine machine learning with **big data** in a Google search and 
you've got yourself an unmanageable amount of information to digest. In an 
(possibly ironic) effort to help navigate this sea of information, this post is 
meant to be an introduction and simplification of some common machine learning 
terminology and types with some resources to dive deeper.

### Supervised vs. Unsupervised Machine Learning

At the highest level, there are two different types of machine learning - 
supervised and unsupervised. Supervised means that we have historical information 
in order to learn from and make future decisions; unsupervised means that we 
have no previous information, but might be attempting to group things together 
or do some other type of pattern or outlier recognition.

In each of these subsets there are many methodologies and motivations; I'll 
explain how they work and give a simple example or two.

### Supervised Machine Learning

Supervised machine learning is nothing more than using historical information 
(read: data) in order to predict a future event or explain a behavior using 
algorithms. I know - this is vague - but humans use these algorithms based on 
previous learning everyday in their lives to predict things.

A very simple example: if it is sunny outside when we wake up, it is perfectly 
reasonable to assume that it will not rain that day. Why do we make this 
prediction? Because over time, we've learned that on sunny days it typically 
does not rain. We don't know for sure that today it won't rain but we're willing 
to make decisions based on our prediction that it won't rain.

Computers do this exact same thing in order to make predictions. The real gains 
come from Supervised Machine Learning when you have lots of accurate historical 
data. In the example above, we can't be 100% sure that it won't rain because 
we've also woken up on a few sunny mornings in which we've driven home after 
work in a monsoon - adding more and more data for your supervised machine 
learning algorithm to learn from also allows it to make concessions for these 
other possible outcomes.

Supervised Machine Learning can be used to classify (usually binary or yes/no 
outcomes but can be broader - is a person going to default on their loan? will 
they get divorced?) or predict a value (how much money will you make next year? 
what will the stock price be tomorrow?). Some popular supervised machine 
learning methods are regression (linear, which can predict a continuous value, 
or logistic, which can predict a binary value), decision trees, k-nearest 
neighbors, and naive Bayes.

My favorite of these methods is decision trees. A decision tree is used to 
classify your data. Once the data is classified, the average is taken of each 
terminal node; this value is then applied to any future data that fits this 
classification.

<center>
![Decision Tree of the Titanic Survivors](/img/machine_learning_demystified/tree.png)
</center>

The decision tree above shows that if you were a female and in first or second 
class, there was a high likelihood you survived. If you were a male in second 
class who was younger than 12 years old, you also had a high likelihood of 
surviving. This tree could be used to predict the potential outcomes of future 
sinking ships (morbid... I know).

### Unsupervised Machine Learning

Unsupervised machine learning is the other side of this coin. In this case, we 
do not necessarily want to make a prediction. Instead, this type of machine 
learning is used to find similarities and patterns in the information to cluster 
or group.

An example of this: Consider a situation where you are looking at a group of 
people and you want to group similar people together. You don't know anything 
about these people other than what you can see in their physical appearance. You 
might end up grouping the tallest people together and the shortest people 
together. You could do this same thing by weight instead... or hair length... or 
eye color... or use all of these attributes at the same time! It's natural in 
this example to see how "close" people are to one another based on different 
attributes.

What these type of algorithms do is evaluate the "distances" of one piece of 
information from another piece. In a machine learning setting you look for 
similarities and "closeness" in the data and group accordingly.

This could allow the administrators of a mobile application to see the different 
types of users of their app in order to treat each group with different rules 
and policies. They could cluster samples of users together and analyze each 
cluster to see if there are opportunities for targeted improvements.

The most popular of these unsupervised machine learning methods is called 
k-means clustering. In 
[k-means clustering](https://en.wikipedia.org/wiki/K-means_clustering), the 
goal is to partition your data 
into k clusters (where k is how many clusters you want - 1, 2,..., 10, etc.). To 
begin this algorithm, k *means* (or cluster centers) are randomly chosen. Each 
data point in the sample is clustered to the closest mean; the center (or 
centroid, to use the technical term) of each cluster is calculated and that 
becomes the new *mean*. This process is repeated until the mean of each cluster is 
optimized.

The important part to note is that the output of k-means is clustered data that 
is "learned" without any input from a human. Similar methods are used in 
[Natural Language Processing (NLP)](https://en.wikipedia.org/wiki/Natural_language_processing) 
in order to do [Topic Modeling](https://en.wikipedia.org/wiki/Topic_model).

### Resources to Learn More

There are an uncountable amount resources out there to dive deeper into this 
topic. Here are a few that I've used or found along my Data Science journey.

**UPDATE: I've written a whole post on this. You can find it [here](https://www.jakelearnsdatascience.com/posts/getting-started-with-data-science/)**

* O'Reilly has a [ton of great books](http://shop.oreilly.com/category/get/machine-learning-kit.do) 
that focus on various areas of machine learning.
* [edX](https://www.edx.org/course/subject/data-analysis-statistics) and 
[coursera](https://www.coursera.org/courses?languages=en&query=machine+learning) 
have a TON of self-paced and instructor-led learning courses in machine learning. 
There is a specific series of courses offered by Columbia University that look 
particularly applicable.
* If you are interested in learning machine learning and already have a 
familiarity with R and Statistics, 
[DataCamp has a nice, free program](https://www.datacamp.com/courses/introduction-to-machine-learning-with-r). 
If you are new to R, they have a 
[free program](https://www.datacamp.com/getting-started?step=2&track=r) for that, too.
* There are also many, many blogs out there to read about how people are using data science and machine learning.
