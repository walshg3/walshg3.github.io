---
layout: post
title: Google Developers Notes
description: "Much Notes"
headline: "Google Developers Notes"
categories: 
  - Machine Learning
  - TensorFlow
  - Independent Study
tags: 
  - Machine Learning
  - TensorFlow

imagefeature: "google-dev.jpg"
imagecredit:
imagecreditlink:
comments: false
mathjax: null
featured: true
published: true
---

This page's purpose is to display the notes I took on the Google Developers Machine Learning Recipes with Josh Gordon [Youtube series](https://goo.gl/KewA03). These notes are also available on the [Github Repo](https://github.com/walshg3/CSIS-4800-MACHINE-LEARNING) for this Independent Study. 

___


NOTE: In order to use the Anaconda libraries you need to open VSCode from Anaconda. 

Episode 1:

    Supervised Learing Recipe:
        Collect Training Data -> Train Classifier -> Make Predictions

        Collect Training Data: 
        In this case we are looking at fruit. 
        The Table would look something like 
        Weight | Texture | Label 
        
        Weight and Texture are FEATURES the better the feature the easier it is to discriminate data 
        The last column is called a LABEL and it identifies the type of finalized data to be selected (Orange and Apple)
        Features are INPUT to a Classifier and LABEL is OUTPUT
        The whole table is the TRAINING DATA. 

        the data will look like this when put in python:

        features = [[140, "smooth"], [130, "smooth"], [150, "bumpy"], [170, "bumpy"]]
        labels = ["apple", "apple", "orange", "orange"]

        Because sklearn uses real-valued features we need to change the strings to ints
            0 -> bumpy
            1 -> smooth
            0 -> apple
            1 -> orange

        Train Classifier:

        This exercise uses a Decision Tree
        
        A Classifier is a box of rules. 
        A Learning Algorith is the procedure that creates Classifiers.
            Finds patterns in data. 
            Included in the classifier Object and is called "Fit"
        There are many different types of classifiers
        You need to import the tree and classifier:

        clf = tree.DecisionTreeClassifier()

        Important Concepts:
            How does this work in the real world?
            How much training data do you need?
            How is the tree created?
            What makes a good feature?

Episode 2:

    There are MANY types of Classifiers
        EX.
        Decision Tree - Easy to Read and Understand 
        Artificial neural network
        Support Vector Machine
        
    Data Set being used is "Iris" 
        Has 3 different types of species by looking at Sepal Length and Width as well as Predal Length and Width as our Features and the Species as our Label
    Goals: 
        1. Import dataset
        2. Train a classifier
        3. Predict label for new flower
        4. Visualize the tree  

    1. Import dataset
        sklearn has the iris dataset built in so we can just import the set. 
        Note: There are errors thrown in the linter im using but everything compliles and runs fine. 
    
    2. Train the Classifier
        This was done by removing a datapoint and then running a fit on the data to see if it would properly predict the right data. 

    3. Predict label for new flower 
        After the fit was run a predict was run and it gave back the exact data there was before it was removed. This shows the prediction and training was accurate. 

    4. Visualize the tree
        Graphviz was used for generating a color coded tree then exported it to a pdf called "iris.pdf" within the same folder. 
        Created a great visual representation of how the model is making the decisions

    Important Notes:
        Every question a Tree asks must be about your Features. That means the better your features are, the better a tree you can build. 
        

Episode 3:

    What makes a Good Feature?

    Some features are good like height or weight but you usually need multiple features to properly predict. 
    Avoid useless features and independent. If you have Height in inches you dont need height in centimeters

    Ideal features are:
        informative
        independent
        simple

Episode 4:

    Machine Learning pipelines
    - scikit-learn has a handy function for splitting data sets into a training and a testing set
    - it's sklearn.model_selection.train_test_split(data_set_features,data_set_labels,test_fraction)
    - this function will return 1) training_features 2) testing_features 3) training_labels and 4) testing_labels
    - i.e. it returns a tuple of 4 elements
    - note, the test_fraction argument specifies the fraction of the data you want to use for testing
    - so if you put 0.5, it means you want to use half the data for testing (and the other half for training obviously)

    - recall that the .predict() method returns a list of predictions for the list of examples you pass it
    - you can use sklearn.metrics.accuracy_score(test_labels,predicted_labels) to compare two list of labels essentially

    - supervised learning is also known as function approximation because ultimately what you are doing is finding a function that matches your training examples well
    - you start with some general form of the function (e.g. y = mx+b) and then you tune the parameters such that it best describes your training examples (i.e. change m and b until you get a line that best splits your data)

    Key thing to take away from the video:
    Supervised learning is just function approximation. You start with a general function and then tweak the parameters of the function based on your training examples until your function describes the training data well.﻿

        
    Features = Label    
    F(x)        y 

    One way to think of learning is using training data to adjust the parameters of a model
    playground.tensorflow.org

Episode 5:
    Writing Classifier from scratch

    Creating K Nearest Neighbors with the pipeline.py program.
    Algorithm info from sklearn here:
    https://scikit-learn.org/stable/modules/neighbors.html

    K Nearest Neighbors tests the distance to the closest neighbor to classify the unknown data.
    If there is equidistance between both red and green sides the k = # of neighbors to consider.
    If k was 1 then it would look at the closest neighbor.
    If k was 3 then it would look at the 3 closest neighbors and make the decision from there. 

    Implementation:

    1. Find the nearest Straightline Distance:
        Will use the Eulidean Distance by measuring distance between two points and uses the formula found in formula.png
        Distance is in 2D space with 2 features but with 3 it will be in 3D or 4D. This is hard to visualize but ED will work perfect regardless. 

    2. Run rest of program with new pipeline

    -  recall, a classifier is first trained (where it receives a bunch of training inputs along with the corresponding outputs) and then it is asked to predict the output for new inputs.
    -  one basic way of implementing a classifier is to save all of your training input/output pairs, and then when you are asked to predict the output for a new input, return the output of the closest training input to your new input

    - so for example, let's say I give you the following training inputs (1, 12, 130) and their respective outputs (2, 14, 140).
    - and then I ask you to predict the output for a new input, 4
    - well, 4 is closest to 1, and the output for 1 was 2, so we will predict the output for 4 to be 2 as well

    - the inputs in the above example are 1 dimensional, but you can use the distance formula for 2, 3 or any number of dimensions


    Pros: 
        Relatively simple
    Cons:
        Computationally intensive
        Hard to represent relationships between features

    Episode 6: Image Classifier

        using tensorflow for Poets
        High level code

        In order to train tensorflow you need lots of images
        create a classifier to tell the difference between 5 types of flowers.
        
___

## Sources

Developers, Google. “Let's Write a Decision Tree Classifier from Scratch - Machine Learning Recipes #8.” YouTube, YouTube, 13 Sept. 2017, www.youtube.com/watch?v=LDRbO9a6XPU.







    