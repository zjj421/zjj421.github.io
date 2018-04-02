---
layout: post
title: MobileNetV2论文笔记
category: DA
tags: DA
keywords:
description:
---

> 论文[链接](https://arxiv.org/pdf/1801.04381.pdf)

## 论文核心：

- Inverted residual structure
  1. 1x1 conv2d, relu6. 增加通道数: (h, w, k) --> (h, w, tk)


  2. 3x3 dwise_conv, relu6. depth-wise convolution: (h, w, tk) --> (h/s, w/s, (tk))
  3. linear 1x1 conv2d. point-wise convolution后没有非线性激活函数：(h/s, w/s, (tk)) --> ()  (h/s, w/s, (k'))

![Bottleneck residual block](assets/markdown-img-paste-20180328130608566.png)
![invered residual block](assets/markdown-img-paste-20180328125039419.png)
![invered residual block](assets/markdown-img-paste-20180328130939769.png)
![model structure](assets/markdown-img-paste-20180328132432858.png)

$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$
