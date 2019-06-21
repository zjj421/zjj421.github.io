---
layout: post
title: ubuntu配置samba
category: 环境搭建
tags: 环境搭建
keywords:
description:
---

## [安装并配置Samba](https://tutorials.ubuntu.com/tutorial/install-and-configure-samba#0)
A samba file server enables file sharing across different operating systems over a network. It lets you access your desktop files from a laptop and share files with Windows and macOS users.

This guide covers the installation and configuration of Samba on Ubuntu.

### 安装Samba
```
sudo apt update
sudo apt install samba
```

### 配置Samba
1. 创建一个用来共享的目录，比如在用户目录下创建“sambashare”目录：
```
mkdir /home/<username>/sambashare
```
2. 在Samba配置文件中添加我们新建的共享目录：
```
sudo vim /etc/samba/smb.conf
在文件底部添加如下信息：
[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes
```
> [sambashare]: The name inside the brackets is the name of our share.

> comment: A brief description of the share.

> path: The directory of our share.

> read only: Permission to modify the contents of the share folder is only granted when the value of this directive is no.

> browsable: When set to yes, file managers such as Ubuntu's default file manager will list this share under "Network" (it could also appear as browseable).

3. 重启Samba服务：
```
sudo service smbd restart
```

### 为Samba设置用户账号并连接到Samba共享文件系统

1. 为ubuntu系统中已存在的用户设置密码：
```
sudo smbpasswd -a username
```
> username只能时系统中已存在的用户名

2. 连接共享文件系统
  - ubuntu：打开默认文件管理器 -> 连接到服务器 -> 输入`smb://ip-address/sambashare`
  - macOS: In the Finder menu, click GO > Connect to Server then enter: `smb://ip-address/sambashare`
  - Windows: 打开文件管理器 -> 地址栏输入`\\ip-address\sambashare`
> `ip-address`是Samba服务器的ip地址 sambashare时共享目录的别名。