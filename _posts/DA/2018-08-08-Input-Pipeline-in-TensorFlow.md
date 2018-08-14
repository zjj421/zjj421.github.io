---
layout: post
title: Input pipeline in TensorFlow
category: DA
tags: DA
keywords:
description:
---

Inference [here](https://www.tensorflow.org/performance/datasets_performance)

## Input Pipeline Structure

A typical TensorFlow training input pipeline can be framed as an *ETL* Process:
  1. **Extract**: Read data from persistent(固定的) storage --either local(e.g. HDD or SSD) or remote(e.g. [GCS](https://cloud.google.com/storage/) or [HDFS](https://en.wikipedia.org/wiki/Apache_Hadoop#Hadoop_distributed_file_system)).
  2. **Transform**: Use CPU cores to parse and perform preprocessing operation on the data such as image decompression(解压缩), data augmentation transformations(such as random crop, flips, and color distortions(颜色扭曲)), shuffling, and batching.
  3. **Load**: Load the transformed data onto the accelerator device(s)(for example, GPU(s) or TPU(s)) that execute the machine learning model.

## Optimizing Performance

### Pipelining 

To perform a training step, you must first extract and transform the training data and then feed it to a model running on a accelerator. However, in a naive synchronous(同步) implementation, while the CPU is preparing the data, the accelerator is sitting idle(空闲). Conversely, while the accelerator is training the model, the CPU is sitting idle. The training step time is thus the sum of both CPU pre-processing time and the accelerator training time.

**Pipelining** overlaps the preprocessing and model execution of a training step. While the accelerator is performing training step N, the CPU is preparing the data for step N + 1. Doing so reduces the step time to the maximum(as opposed to the sum) of the training and the time it takes to extract and transform the data.

