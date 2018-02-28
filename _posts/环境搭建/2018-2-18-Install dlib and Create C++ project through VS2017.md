---
layout: post
title: Install dlib and Create C++ project through VS 2017
category: 环境搭建
tags: 环境搭建
keywords:
description:
---

## 1 [下载dlib](http://dlib.net/)
1. 下载dlib并解压。
3. 在dlib根目录下创建空文件夹并重名为build。

## 2 [下载cmake](https://cmake.org/download/)
进入cmake官网下载cmake-3.11.0-rc2-win64-x64.msi并安装。

## 3 编译dlib
> **如电脑装有cuda则编译为gpu加速版本，否则编译为cpu版本**

1. 打开cmake-gui,指定source（如D:\dlib-19.9）和build目录（刚自己新建的build目录）。
2. Configure --> Visual Studio 14 2015 Win64 --> Finish。
3. 如有Warning则重新configure。
4. Generate。
5. Visual Studio打开build目录（D:\dlib-19.9\build\Project.sln）。
6. 解决方案配置设置为Release,x64。
7. 右击解决方案中的ALL_BUILD并选择生成（完成后D:\dlib-19.9\build\dlib\Release目录下会出现dlib_release_64bit_msv1900.lib文件）。

## 4 配置工程目录
1. 新建一个空的工程目录"D:\dlib_test"。
2. 设置工程目录属性(解决方案配置设置为Release， x64)：
  - VC++目录 --> 包含目录 --> "D:\dlib-19.9"。
  - C/C++ --> 预处理器定义 --> "DLIB_JPEG_SUPPORT"。
  - 链接器 --> 输入 --> 附加依赖项 --> D:\dlib-19.9\build\dlib\Release\dlib_release_64bit_msv1900.lib。
2. 在解决方案中的资源文件下新建一个source.cpp文件。
3. 复制dlib的C++例子(如dnn_face_recognition_ex.cpp)到source.cpp文件中，然后build。
4. 下载以下两个文件并解压到"D:\dlib_test\x64\Release"
http://dlib.net/files/shape_predictor_5_face_landmarks.dat.bz2
http://dlib.net/files/dlib_face_recognition_resnet_model_v1.dat.bz2
5. 把dlib中example里的faces文件夹也复制到"D:\dlib_test\x64\Release"。
6. cmd进入"D:\dlib_test\x64\Release"目录并输入'dlib_test face\bald_guys.jpg'。
7. 结果：弹出一张图片并聚类和输出提取到的特征
