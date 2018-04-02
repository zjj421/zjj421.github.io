---
layout: post
title: Anaconda多环境多python版本配置
category: 工具使用
tags: 工具使用
keywords:
description:
---

## 管理环境

### 创建并激活一个环境
`conda create --name env_name python=3.5`

`source activate env_name`
windows下去掉`source`

### 注销一个环境
`source deactivate`

### 列出所有环境
`conda info --envs`

### 复制一个环境
`conda create -n new_env --clone old_env`

### 删除一个环境
`conda remove -n env_name --all`

### 查找一个包
检查一个包是否可通过conda来安装
`conda search beautifulsoup4`
