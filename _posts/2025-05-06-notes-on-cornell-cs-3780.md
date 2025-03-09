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
- Definitions:
  - Supervised learning: "_make predictions from data_"
  - Classifier: "_a program to predict the correct label of each annotated data instance_"
  - Binary classification: a label is one of two possibilities
  - Multi-class classification: a label is one of K possibilities
  - Regression: the label space is the real numbers
  - Feature vector: _the input vector of a sample_
  - Hypothesis: a function such that, given a feature vector and its label from the training data, the function takes the feature vector and returns the label with high probability
  - Feature: a dimension of the feature vector
  - Dense feature vector: _the number of nonzero coordinates in the feature vector is large relative to the number of features_
  - Sparse feature vector: _the feature vector consists of mostly zeros_
  - Hypothesis class: _the set of possible hypothesis functions_, _the set of hypothesis functions we can possibly learn_
  - No Free Lunch Theorem: "_every successful ML algorithm must make assumptions. This also means that there is no single ML algorithm that works for every setting_"
  - Loss function / risk function: "_evaluates a hypothesis on our training data and tells us how bad it is_"
  - Loss: "_the higher the loss, the worse a hypothesis is - a loss of zero means it makes perfect predictions_"
  - Zero-one loss: "_counts how many mistakes a hypothesis function makes on the training set_"
  - Normalized zero-one loss / training error: "_the fraction of misclassified training samples_"
  - Overfitting: _get low error on the training data, but does horribly with samples not in the training data_
  - 
