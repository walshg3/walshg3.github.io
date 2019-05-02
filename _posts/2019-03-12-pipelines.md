---
layout: post
title: Pipelines and KNeighbors Classifier
description: "PKNeighborsClassifier pipeline"
headline: "Making a Pipeline"
categories: 
  - Machine Learning
  - TensorFlow
  - Independent Study
tags: 
  - Machine Learning
  - TensorFlow

imagefeature: "pipes.jpeg"
imagecredit:
imagecreditlink:
comments: false
mathjax: null
featured: true
published: true
---

On Episode 4 of the Google Developers Machine Learning Recipes with Josh Gordon [Youtube series](https://goo.gl/KewA03) we are going to try to create a pipline to predict and train data as well as implement a high level approach of K Nearest Neighbors. 

Machine Learning pipelines
  * scikit-learn has a handy function for splitting data sets into a training and a testing set
  * it's sklearn.model_selection.train_test_split(data_set_features,data_set_labels,test_fraction)
  * this function will return 1) training_features 2) testing_features 3) training_labels and 4) testing_labels
  * i.e. it returns a tuple of 4 elements
  * note, the test_fraction argument specifies the fraction of the data you want to use for testing
  * so if you put 0.5, it means you want to use half the data for testing (and the other half for training obviously)
  * recall that the .predict() method returns a list of predictions for the list of examples you pass it
  * you can use sklearn.metrics.accuracy_score(test_labels,predicted_labels) to compare two list of labels essentially
  * supervised learning is also known as function approximation because ultimately what you are doing is finding a function that matches your training examples well
  * you start with some general form of the function (e.g. y = mx+b) and then you tune the parameters such that it best describes your training examples (i.e. change m and b until you get a line that best splits your data)

## Prerequisites 
I am using MacOS for my development so if you are running Linux, Windows, or are throwing rocks to make sparks you might need to change accordingly. I used conda ([Anacondas](https://docs.anaconda.com/anaconda/navigator/) Package Manager) to create a python environment for the application. 

It is recommended to use either Docker containers or python virtual environments for projects like this. In order to create the python environment for TensorFlow I ran the following command in terminal: 

```bash
conda create -n tensorflow_env TensorFlow 
```
This will create a python environment with the base level packages needed including TensorFlow. From there all you have to do is activate the python environment in your terminal session:

```bash
conda activate tensorflow_env
```
Now we are in the activated python environment so any scripts for the TensorFlow guide that need specific imports will be able to run with no problems. 

The code I used is available on my [github](https://github.com/walshg3/CSIS-4800-MACHINE-LEARNING/blob/master/Google%20Developers%20Machine%20Learning%20Recipes%20Series/pipeline.py) 

## My thoughts on the video

The concepts of pipelines were pretty intuitive to understand. It allowed me to fully understand the [TensorFlow Playground](https://playground.tensorflow.org) and understand the importance of layers in a neural network. 

Supervised learning is just function approximation. You start with a general function and then tweak the parameters of the function based on your training examples until your function describes the training data well.
       
Features = Label    
F(x)        y 

K Nearest Neighbors is a really interesting concept. Being able to have a computer create a prediction based off the Euclidian distance on a straight line is a really interesting idea. I am looking forward to diving in depth of how to make K Nearest Neighbors in a future episode. I would also like to do research on how K Nearest Neighbors is being used in the real world.


---

## Sources 

Developers, Google. “Let's Write a Pipeline - Machine Learning Recipes #4.” YouTube, YouTube, 11 May 2016, www.youtube.com/watch?v=84gqSbLcBFE&list=PLOU2XLYxmsIIuiBfYad6rFYQU_jL2ryal&index=5&t=2s.