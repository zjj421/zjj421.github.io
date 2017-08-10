---
layout: post
title: Basic knowledge of Linux
category: Linux
tags: Linux
keywords:
description:
---

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

## 设置程序开机自启

方法有很多，这里只记录其中一种：

    1. sudo vim /etc/rc.local
    2. 在exit 0之前添加想在开机时运行的命令
    3. 如果想以指定用户运行某个命令: sudo -u username <cmd>

## 终端使用socks5代理

### 配置：

1. sudo apt install polipo
2. sudo vim /etc/polipo/config
3. config内容设置如下：
```
    logSyslog = true
    logFile = /var/log/polipo/polipo.log
    socksParentProxy = "localhost:1080"
    socksProxyType = socks5
    logLevel=4
```
4. 关闭软件，让设置生效: sudo service polipo stop
5. sudo service polipo start

### 使用：

1. vim ~/.bashrc
2. 最后一行写入：
```
    alias ss="http_proxy=http://localhost:8123"
```
alias命令是设置别名用的，这里ss就代表"http_proxy=http://localhost:8123".
3. 以代理方式运行某条命令，只需在其前面加上ss就可以了。
```
    例如：ss curl ip.gs　(显示当前ip的详细信息。)
```
### git需要重新配置代理

1. socks5代理：
```
    git config --global http.proxy 'socks5://127.0.0.1:1080'
    git config --global https.proxy 'socks5://127.0.0.1:1080'
```
2. http代理：
```
    git config --global http.proxy https://127.0.0.1:1080
    git config --global https.proxy https://127.0.0.1:1080
```
3. 取消：
```
    git config --global --unset http.proxy
    git config --global --unset https.proxy
```
### pip配置代理

1. vim ~/.bashrc
2. 最后一行加上：
```
    alias pip="pip --proxy 127.0.0.1:8123"
```
3. source ~/.bashrc

### ubuntu和windows共享文件系统（永久）

1. sudo fdisk -l 查看想要挂载的分区的设备号，如/dev/sdb1
2. sudo vim /etc/fstab 在最后一行添加自己想要挂载的设备号，如：
```
    dev/sdb1       /home/zj/dataShare      ntfs    defaults        0       0
```    
3. 保存重启。注意，挂载点不能为用户根目录，否则后果很严重。　　





未完待续
