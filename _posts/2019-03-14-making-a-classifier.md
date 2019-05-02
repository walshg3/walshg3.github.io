---
layout: post
title: Making the KNeighbors Classifier
description: "Making the K nearest neighbors classifier from scratch"
headline: "Making a Classifier"
categories: 
  - Machine Learning
  - TensorFlow
  - Independent Study
tags: 
  - Machine Learning
  - TensorFlow

imagefeature: "graph.jpg"
imagecredit:
imagecreditlink:
comments: false
mathjax: null
featured: true
published: true
---



K Nearest Neighbors tests the distance to the closest neighbor to classify the unknown data.
If there is equidistance between both red and green sides the k = # of neighbors to consider.
If k was 1 then it would look at the closest neighbor.
If k was 3 then it would look at the 3 closest neighbors and make the decision from there. Creating K Nearest Neighbors with the pipeline.py program.
Algorithm info from sklearn [here](https://scikit-learn.org/stable/modules/neighbors.html)

On Episode 5 of the Google Developers Machine Learning Recipes with Josh Gordon [Youtube series](https://goo.gl/KewA03) we are going to create the K Nearest Neighbors Classifier from scratch and compare it with a less accurate classifier to show how effective it is. 

Writing Classifier from scratch:


Implementation:

1. Find the nearest Straight-line Distance:
    Will use the Euclidean Distance by measuring distance between two points and uses the formula found in formula.png
    Distance is in 2D space with 2 features but with 3 it will be in 3D or 4D. This is hard to visualize but ED will work perfect regardless. 

    ```python
    def euc(a,b):
    return distance.euclidean(a,b)
    ```
2. Run rest of program with new pipeline
- recall, a classifier is first trained (where it receives a bunch of training inputs along with the corresponding outputs) and then it is asked to predict the output for new inputs.
- one basic way of implementing a classifier is to save all of your training input/output pairs, and then when you are asked to predict the output for a new input, return the output of the closest training input to your new input
- so for example, let's say I give you the following training inputs (1, 12, 130) and their respective outputs (2, 14, 140).
- and then I ask you to predict the output for a new input, 4
- well, 4 is closest to 1, and the output for 1 was 2, so we will predict the output for 4 to be 2 as well
- the inputs in the above example are 1 dimensional, but you can use the distance formula for 2, 3 or any number of dimensions

Pros: 
   * Relatively simple

Cons:
   * Computationally intensive
   * Hard to represent relationships between features

Using a Random Point as the classifier:

```python
def predict(self,X_test):
    predictions = []
    for row in X_test:
        label = random.choice(self.y_train)
        predictions.append(label)
    return predictions
```
This prediction got 0.33333 as a result because there is not a very good classifier 

Next, we will use the **Euc Distance** as our classifier:

```python
def predict(self,X_test):
        predictions = []
        for row in X_test:
            label = self.closest(row)
            predictions.append(label)
        return predictions

    #Keep track of closest point so far:
def closest(self,row):
    best_dist= euc(row,self.X_train[0])
    best_index = 0

    #iterate over all distances 
    for i in range(1, len(self.X_train)):
        dist = euc(row, self.X_train[i])
        #if a closer distance is found update variables 
        if dist < best_dist:
            best_dist = dist
            best_index = i
    #use the index to return the label for the closest training example
    return self.y_train[best_index]

```

The prediction made using the Euc Distance gets us within the 90th percentile! This is much better than our randomly selected point used before. 

The really interesting thing about K Nearest Neighbors is that it is being used to solve real world problems. In a paper written by Chen, Hui-Ling he explains how he is using K Nearest Neighbors as 
>"An efficient Parkinson’s disease diagnostic system using fuzzy k-nearest neighbor method(FKNN). Experimental results have demonstrated that the FKNN-based system greatly outperforms support vector machines approaches and other methods in the literature. The best classification accuracy (96.07%) obtained by the FKNN-based system using a 10-fold cross validation method can ensure a reliable diagnostic model for detection of PD. Promisingly, the proposed system might serve as a new candidate of powerful tools for diagnosing PD with excellent performance." (Hui-Ling 2012)

Even if the system is only helping with diagnosing Parkinsons it is a clear example that the K Nearest Neighbor classification is changing peoples lives. 



Understanding how these classifiers work and why is really important in machine learning. The Euc Distance is much better for the Iris dataset compared to the Decision Tree and it goes to show how different classifiers will get better results so knowing how to use a bunch of them will can be helpful.



---

## Sources

Abu-Aisheh, Zeina, Romain Raveaux, and Jean-Yves Ramel. "Efficient k-Nearest Neighbors Search in Graph Space." Pattern Recognition Letters, 2018.

Chen, Hui-Ling, et al. "An Efficient Diagnosis System for Detection of Parkinson's Disease using Fuzzy k-Nearest Neighbor Approach." Expert Systems with Applications, vol. 40, no. 1, 2013, pp. 263.

Developers, Google. “Writing Our First Classifier - Machine Learning Recipes #5.” YouTube, YouTube, 8 June 2016, www.youtube.com/watch?v=AoeEHqVSNOw&list=PLOU2XLYxmsIIuiBfYad6rFYQU_jL2ryal&index=5.

Xu, Yong, et al. "Coarse to Fine K Nearest Neighbor Classifier." Pattern Recognition Letters, vol. 34, no. 9, 2013, pp. 980-986.

