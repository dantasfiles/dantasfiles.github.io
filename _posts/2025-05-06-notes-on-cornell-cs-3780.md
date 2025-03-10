---
title: Notes on 🐻<i>Introduction to Machine Learning</i>
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

I was curious to learn what has been updated since I took a [version of CS 3780](https://dantasfiles.com/2001/01/22/cornell-junior-spring.html), so I am reading through the [lecture slides for the Spring 2025 semester](https://www.cs.cornell.edu/courses/cs3780/2025sp/)

I use these notes to keep track of my thoughts while reading and to record anything that sticks out to me as interesting. The notes are incomplete as I have not yet finished reading the slides

##  Introduction
- I've heard many definitions of machine learning and artificial intelligence, but the ones use by this course are machine learning: "_programs that improve with experience, a subfield of artificial intelligence_" and artificial intelligence: "_programs that demonstrate 'intelligence' in some sense_"
- The slides contain a fun flowchart: _(training data + training output → program / model) + test data → test output_

## ML basics
- Definitions adapted from notes:
  - [Supervised learning](https://en.wikipedia.org/wiki/Supervised_learning): "_make predictions from data_"
  - [Classifier](https://en.wikipedia.org/wiki/Statistical_classification): "_a program to predict the correct label of each annotated data instance_"
  - [Binary classification](https://en.wikipedia.org/wiki/Binary_classification): a label is one of two possibilities
  - [Multi-class classification](https://en.wikipedia.org/wiki/Multiclass_classification): a label is one of K possibilities
  - [Regression](https://en.wikipedia.org/wiki/Regression_analysis): the label space is the real numbers
  - [Feature vector](https://en.wikipedia.org/wiki/Feature_(machine_learning)#Feature_vectors): _the input vector of a sample_
  - [Feature](https://en.wikipedia.org/wiki/Feature_(machine_learning)): a dimension of the feature vector
  - Dense feature vector: _the number of nonzero coordinates in the feature vector is large relative to the number of features_
  - Sparse feature vector: _the feature vector consists of mostly zeros_
  - Hypothesis class: _the set of possible hypothesis functions_, _the set of hypothesis functions we can possibly learn_, "_encodes your assumptions about the data set / distribution_"
  - [No Free Lunch Theorem](https://en.wikipedia.org/wiki/No_free_lunch_theorem): "_every successful ML algorithm must make assumptions. This also means that there is no single ML algorithm that works for every setting_", "_you must make assumptions in order to learn. no Algorithm Works in all settings_"
  - [Loss function](https://en.wikipedia.org/wiki/Loss_function) / risk function: "_evaluates a hypothesis on our training data and tells us how bad it is_", "_tells us how good
a model did on an instance_"
  - Loss: "_the higher the loss, the worse a hypothesis is - a loss of zero means it makes perfect predictions_"
  - [Zero-one loss](https://en.wikipedia.org/wiki/Loss_function#0-1_loss_function): "_counts how many mistakes a hypothesis function makes on the training set_"
  - Normalized zero-one loss / training error: "_the fraction of misclassified training samples_"
  - [Overfitting](https://en.wikipedia.org/wiki/Overfitting): _get low error on the training data, but does horribly with samples not in the training data_
  - [Weak law of large numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers#Weak_law): "_the empirical average of data drawn from a distribution converges to its mean_"
  - [Feature extraction](https://en.wikipedia.org/wiki/Feature_engineering): Selecting "_part of instances we deem relevant for predicting output_"
  - Model / program / hypothesis: function from input to "_label / output we would like to predict_"

## K-nearest neighbors and the curse of dimensionality
- Definitions:
  - [k-NN algorithm](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm): "_or a test input, assign the most common label amongst its k most similar training inputs_"
  - [Bayes optimal classifier](https://en.wikipedia.org/wiki/Bayes_classifier): "_you knew P(y|x), then you would simply predict the most likely label_"
- According to Wikipedia: "[_Minkowski distance](https://en.wikipedia.org/wiki/Minkowski_distance) is typically used with p being 1 or 2, which correspond to the [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry) and the [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance), respectively. In the limiting case of p reaching infinity, we obtain the [Chebyshev distance](https://en.wikipedia.org/wiki/Chebyshev_distance)_"
- 

