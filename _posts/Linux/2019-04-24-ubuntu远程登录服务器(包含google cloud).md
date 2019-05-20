---
layout: post
title: ubuntu登录远程服务器（包含google cloud）
category: Linux
tags: Linux
keywords:
description:
---

## google cloud 终端ssh连接
参考自[这里](https://www.jianshu.com/p/57e85cf3e50b)

1. 网页端登录google cloud服务器

2. 设置当前用户和root用户的新密码
```
sudo passwd ${whoami}
sudo passwd root
```
3. 本地生成秘钥对
```
cd ~/.ssh
ssh-keygen -f googlecloudkey
```
4. 复制公钥并导入到谷歌云
```
#　进入谷歌云平台页面 -> 计算引擎 -> 元数据 -> SSH 密钥，粘贴保存
#　将公钥最后的内容改成google cloud当前用户名
```
5. 本地通过私钥登录google cloud
```
ssh -i myKey user@ip
```

## ubuntu免密登录远程服务器

下次配置时再写
