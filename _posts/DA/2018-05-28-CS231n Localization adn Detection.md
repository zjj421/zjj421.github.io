---
layout: post
title: CS231n Winter 2016 Lecture 8 Localization and Detection
category: DA
tags: DA
keywords:
description:
---

# Localization and Detection

bounding box: XY coordinates of the upper left hand corner and the width and height of the box. Just 4 numbers.

## Localization

### Simple Reciple for Classification and Localization

#### Step 1: Train a classification model(VGG, ResNet).

image -> convolution and pooling -> final conv feature map -> fully connected
layers -> class scores -> softmax loss.

#### Step 2: Attach new fully-connected "regression head" to the network.

image -> convolution and pooling -> final conv feature map

- Classification head: final conv feature map -> fully connected layers -> class scores
- Regression head: final conv feature map -> fully-connected layers -> box coordinates

#### Step 3

Train the regression head only with SGD and L2 loss.

image -> convolution and pooling -> final conv feature map -> fully-connected
layers -> box coordinates -> L2 loss

#### Step 4

At test time use both heads

> Notes:  Whre exactly you attach the regression head. This isn't too important
different people do it in different ways. Some attach it after the final
convolutional feature map layer(such as VGG and Overfeat) and some attach it  
after the last funlly connected layers from the classification network(such as
DeepPose, R-CNN).

### Localization as Regression
Localization and treating it as regression for a fixed number of objects.

The idea of actually localizing multiple objects the same time is pretty general and pretty powerful.

### Localization as Sliding Window
Overfeat: efficient sliding window by converting fully-connected layers into
convolutions.

Training time: Small image, 1 x 1 classifier output.

Test time: Larger image, 2 x 2 classifier output, only extra compute at
yello regions.(后期补图)

### ImageNet Classification and Localization

AlexNet(2012): Localization method not published.

Overfeat(2013): Multiscale convolutional regression with box merging.

VGG(2014, Localization Error(Top 5) is 25.3): Same as Overfeat, but fewer scales and locations; simpler method, gains
all due to deeper features.

ResNet(2015, Localization Error(Top 5) is 9): Different localization method(RPN) and much deeper features.

## Object Detection
It is hard to treat detection as straight-up regression because we have this
problem of variable size outputs.

### Detection as Classification

Problem: Need to test many positions and scales.

Solution: If your classifier is fast enough, just do it. You can also only look
at a tiny subset of possible positions.

#### Region Proposals

Region Proposals is this thing that takes in an input image and then outputs a
whole bunch of regions where may be an object might be located.

- "Class-agnostic(不可知)" object detector

Selective Search(还有其他的方法):

Bottom-up segmentation, merging regions at multiple scales.

### R-CNN

image -> regions of interest(RoI) from a proposal method(~2k) ->
warped image regions -> conv net -> Bbox reg and SVMs.

### Fast R-CNN

image -> conv net -> RoI -> RoI Pooling (single-level SPP)layer -> FCs ->
Softmax classifier and bounding Box regression.

未完待续...
