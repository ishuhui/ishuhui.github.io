---
title: pip简介
top_img: transparent
tags:
  - pip
abbrlink: 10359
date: 2023-03-24 16:34:42
---

> `pip`是通用的`Python`包管理工具，提供了对`Python`包的查找、下载、安装、卸载功能。

# `pip`卸载

```shell
python -m pip uninstall pip
```

# `pip`安装

![](pip简介/1.jpg)

下载解压后，进入该路径下输入

![](pip简介/2.jpg)

```shell
python setup.py install
```

# 常用命令

```shell
# 显示版本和路径
pip --version

# 获取帮助
pip --help

# 升级pip
pip install -U pip

# 安装包
pip install SomePackage               # 最新版本
pip install SomePackage==1.0.4        # 指定版本
pip install ‘SomePackage>=1.0.4’      # 最小版本

# 升级包
pip install --upgrade SomePackage

# 卸载包
pip uninstall SomePackage

# 搜索包
pip search SomePackage

# 显示安装包信息
pip show SomePackage

# 列出已安装的包
pip list

# 查看指定包的详细信息
pip show -f SomePackage

```

