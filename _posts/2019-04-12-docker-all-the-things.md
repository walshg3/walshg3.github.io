---
layout: post
title: Docker All The Things
description: "ship em over!"
headline: "Docker All The Things"
categories: 
  - Machine Learning
  - TensorFlow
  - Docker
tags: 
  - Machine Learning
  - TensorFlow
  - Docker

imagefeature: "docker.png"
imagecredit:
imagecreditlink:
comments: false
mathjax: null
featured: true
published: true
---

>[Docker](https://www.docker.com/) is a tool designed to make it easier to create, deploy, and run applications by using containers. **Containers** allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.

The Docker client runs on your machine and takes up some resources from your computer. It then uses these resources to run the desired containers. The Docker containers can be linked together to communicate with open ports. 

There are thousands of Docker Containers available on [Docker Hub](hub.docker.com). Docker is not a new concept and has been out for many years however I have just started learning about the concepts of dockerizing my environments to make things easier. 

Specifically, the Machine Learning Independent Study requires TensorFlow Python libraries. Before Docker and in other tutorials I needed to setup my own environment for TensorFlow using conda or venv. In order to handle all the dependencies TensorFlow needed I needed a virtual environment to hold everything. This was great once setup and I was content however frequently programming back and forth on my Mac and Windows computer I found most my time was spent worry about the environment and making sure the environment stayed the same between both systems. 

So how does Docker **help**? Well Docker Hub has a [TensorFlow container](https://hub.docker.com/r/tensorflow/tensorflow) that I could run on both machines. The container helps all the dependencies I needed to run anything TensorFlow related. This was crucial when I moved onto TensorFlow 2.0. Not having to worry about dependencies allowed me to spend more time learning about neural networks and less time on Stack overflow worrying about dependencies. 

In order to run my TensorFlow Container all I need to run is: 

```bash
docker run -it -u 501 --rm -p 8888:8888 tensorflow/tensorflow:latest-py3-jupyter
```

This TensorFlow Container users Jupyter notebooks which is preference for what I was working with at the time. Most of the TensorFlow Tutorials are written in notebooks to make learning easier. 

If you wanted to run the container with bash you would run:

```bash
docker run -it tensorflow/tensorflow bash
```

Docker can get a lot more advanced such as networking and adding volumes. Volumes are important if you plan on keeping you code outside the container. 

All in all its a great tool that i've had a lot of fun learning about. The whale is super cute too! 

<img src="https://www.brianweet.com/assets/docker-blog-1/docker-logo.png" alt=""  />

___

## Sources

“What Is Docker?” Opensource.com, opensource.com/resources/what-docker.

docker.com

hub.docker.com

