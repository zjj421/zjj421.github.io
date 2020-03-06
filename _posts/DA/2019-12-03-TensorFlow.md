---
layout: post
title: TensorFlow
category: DA
tags: DA
keywords:
description:
---

## 服务器使用tensorboard
参考自[这里](https://stackoverflow.com/questions/38513333/is-it-possible-to-see-tensorboard-over-ssh)

1. 本地连接服务器: `ssh -L 16006:127.0.0.1:6006 account@server.address`
2. `tensorboard --logdir  your_log_dir`
3.  本地浏览器输入: `http://127.0.0.1:16006/`