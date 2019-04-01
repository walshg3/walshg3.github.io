---
layout: post
title: TensorFlow Flowers
description: "So many Flower!"
headline: "TensorFlow Flowers"
categories: 
  - Machine Learning
  - TensorFlow
  - Independent Study
tags: 
  - Machine Learning
  - TensorFlow

imagefeature: "tensorflow-android.png"
imagecredit:
imagecreditlink:
comments: false
mathjax: null
featured: true
published: true
---

Over the majority of my independent study on Machine Learning I have studied [TensorFlow Library](https://www.tensorflow.org/) made by google. While following [Josh Gordon's](https://twitter.com/random_forests) Machine Learning Recipes series on [youtube](https://www.youtube.com/watch?v=cKxRvEZd3Mw&list=PLOU2XLYxmsIIuiBfYad6rFYQU_jL2ryal) I discovered TensorFlow for Poets Code Lab which is a neural network designed for image recognition. By following this [Google Codelab](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/?utm_campaign=chrome_series_machinelearning_063016&utm_source=gdev&utm_medium=yt-desc#0) I was able to successfully create an application that recognizes the difference between daisy, sunflowers, dandelion, roses, tulips using only the trained neural network and a phone camera. I ran into a few hiccups along the way that I will write about below.

I recommend following the guide as it is very well written however it does not go into how to setup your ide and environment for the project. Keep in mind I am using MacOS for my development so if you are running Linux, Windows, or are throwing rocks to make sparks you might need to change accordingly. I used conda ([Anacondas](https://docs.anaconda.com/anaconda/navigator/) Package Manager) to create a python environment for the application. 

It is recommended to use either Docker containers or python virtual environments for projects like this. In order to create the python environment for TensorFlow I ran the following command in terminal: 

```bash
conda create -n tensorflow_env TensorFlow 
```
This will create a python environment with the base level packages needed including TensorFlow. From there all you have to do is activate the python environment in your terminal session:

```bash
conda activate tensorflow_env
```
Now we are in the activated python environment so any scripts for the TensorFlow guide that need specific imports will be able to run with no problems. 

Other than that, I was successfully able to create a neural network to identify the flowers. I will attach a few screenshots below of the application identifying the flowers: 

Roses: 

<img src="{{ site.url }}/images/flowers/rose1.png" alt="" width="200" />
<img src="{{ site.url }}/images/flowers/rose2.png" alt="" width="200"/>


<br>
<br>

Tulips:

<img src="{{ site.url }}/images/flowers/tulip.png" alt="" width="200"/>

<br>
<br>

Sunflowers:

<img src="{{ site.url }}/images/flowers/sunflower1.png" alt="" width="200"/>
<img src="{{ site.url }}/images/flowers/sunflower2.png" alt="" width="200"/>


How does this work you might be asking? Basically, a bunch of images was passed into googles [inception](https://ai.googleblog.com/2016/03/train-your-own-image-classifier-with.html) engine to looks specifically for flowers. After extensive training and testing the image classifier gets almost perfect results on flowers. The really cool thing with inception is you can use it as a base and train your own image classifier to identify any object as long as you have enough pictures to pass into the training.

On a final and hilarious note. I've been going around and seeing what kind of flowers my friends are :)

<img src="{{ site.url }}/images/flowers/friend1.png" alt="" width="200"/>
<img src="{{ site.url }}/images/flowers/friend2.png" alt="" width="200"/>
<img src="{{ site.url }}/images/flowers/friend3.png" alt="" width="200"/>
