---
layout: post
title: Basic knowledge of Linux
category: Linux
tags: Linux
keywords:
description:
---

# Baseic knowledge of Linux
## 安装软件

* .deb
  * 安装软件：sudo dpkg -i ****.deb
  * 卸载软件：sudo dpkg -r ****.deb
  * 完全卸载软件：sudo dpkg -P ****.deb
* apt
  * 安装：sudo apt install <package_name>
  * 卸载：sudo apt --purge remove <package_name>

## 硬链接和软链接（符号链接）的区别

![hard_and_soft_link](assets/markdown-img-paste-20170807204239791.png)

１. 硬链接 (hard link)

    ln file1 file1_hardlink
    给file1创建了一个硬链接fiel1_hardlink，２个文件的内容是关联的，修改其中任何一个文件的内容，另一个文件也会跟着被修改，２个文件的大小一样。但是删除某一个文件并不会影响另一个文件。

２. 软链接（soft link）
    ln -s file2 file2_softlink
    同样２个文件是关联的，与硬链接不同的是，软链接文件的大小为０，删除或移动原文件会影响软链接文件。

３. 此处只做了简单区分，[参考自这里](https://askubuntu.com/questions/108771/what-is-the-difference-between-a-hard-link-and-a-symbolic-link)。
