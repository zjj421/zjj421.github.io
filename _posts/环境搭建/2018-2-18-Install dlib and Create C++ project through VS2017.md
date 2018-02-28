---
layout: post
title: 环境搭建
category: C++
tags: C++
keywords:
description:
---

## 1 [下载dlib](http://dlib.net/)
1. 下载dlib并解压
3. 在dlib根目录下创建空文件夹并重名为build

## 2 [下载cmake](https://cmake.org/download/)
进入cmake官网下载cmake-3.11.0-rc2-win64-x64.msi并安装

## 3 编译dlib
> **如电脑装有cuda则编译为gpu加速版本，否则编译为cpu版本**

1. 打开cmake-gui,指定source（如D:\dlib-19.9）和build目录（刚自己新建的build目录）
2. Configure --> Visual Studio 14 2015 Win64 --> Finish
3. 如有Warning则重新configure
4. Generate
5. Visual Studio打开build目录（D:\dlib-19.9\build\Project.sln）
6. 解决方案配置设置为Release,x64
7. 右击解决方案中的ALL_BUILD并选择生成（完成后D:\dlib-19.9\build\dlib\Release目录下会出现dlib_release_64bit_msv1900.lib文件）

## 4 配置工程目录
1. 新建一个空的工程目录
2. 设置工程目录属性(解决方案配置设置为Release， x64)
  - VC++目录 --> 包含目录 --> "D:\dlib-19.9"
  - C/C++ --> 预处理器定义 --> "DLIB_JPEG_SUPPORT"
  - 链接器 --> 输入 --> 附加依赖项 -->
2. 在解决方案中的资源文件下新建一个source.cpp文件
3. 复制dlib的C++例子(如dnn_face_recognition_ex.cpp)到source.cpp文件中，然后build
4. 下载一下两个文件并解压到http://dlib.net/files/shape_predictor_5_face_landmarks.dat.bz2
http://dlib.net/files/dlib_face_recognition_resnet_model_v1.dat.bz2
