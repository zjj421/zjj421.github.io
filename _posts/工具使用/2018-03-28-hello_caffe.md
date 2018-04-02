---
layout: post
title: Training With Your Own Dataset on Caffe
category: 工具使用
tags: 工具使用
keywords:
description:
---

> 参考自[这里](https://chunml.github.io/ChunML.github.io/project/Training-Your-Own-Data-On-Caffe/)

## Caffe使用基本流程（以下代码需要修改！）

1. 准备数据
  - 创建train.txt和val.txt.(文件中每一行为数据id, 标签(从0开始)，中间以空格隔开。)
  > What the two files do is to tell our Network where to look for each image and its corresponding class.

  - 数据转换为LMDB格式。（提高数据读取速度。）
  ```
    sudo cp examples/imagenet/create_imagenet.sh examples/DogsCatsKaggle/
    修改之：
    EXAMPLE=examples/DogsCatsKaggle
    DATA=data/DogsCatsKaggle
    TOOLS=build/tools

    TRAIN_DATA_ROOT=data/DogsCatsKaggle/train/
    VAL_DATA_ROOT=data/DogsCatsKaggle/train/
    ...
    RESIZE=true
    ...
    GLOG_logtostderr=1 $TOOLS/convert_imageset \
    ...
        $EXAMPLE/dogscatskaggle_train_lmdb

    echo "Creating val lmdb..."

    GLOG_logtostderr=1 $TOOLS/convert_imageset \

    ...
        $DATA/val.txt \
        $EXAMPLE/dogscatskaggle_val_lmdb

    echo "Done."
    执行：
    ./examples/DogsCatsKaggle/create_imagenet.sh
  ```
  - 计算数据的均值。
  ```
    sudo cp examples/imagenet/make_imagenet_mean.sh examples/DogsCatsKaggle/
    修改之：
    EXAMPLE=examples/DogsCatsKaggle
    DATA=data/DogsCatsKaggle
    TOOLS=build/tools

    $TOOLS/compute_image_mean $EXAMPLE/dogscatskaggle_train_lmdb \
      $DATA/dogscatskaggle_mean.binaryproto
    执行：
   ./examples/DogsCatsKaggle/make_imagenet_mean.sh
  ```

2. 定义模型

  创建solver.prototxt(优化器配置文件)和train_val.prototxt（模型结构配置文件）。

3. 训练模型
```
 ./build/tools/caffe train --solver=models/dogscatskaggle_alexnet/solver.prototxt
```

> 公司要求用的caffe，太难用了，没有tensorflow,pytorch等方便。
