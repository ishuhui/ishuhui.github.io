---
title: yarn冲突问题
top_img: transparent
tags:
  - node
abbrlink: 43558
date: 2023-03-26 00:16:49
---

# `node`中的`yarn`与`hadoop`的`yarn`冲突问题

安装`yarn`后，查看版本号`yarn -v`出现下面的问题

>'D:\Program' 不是内部或外部命令，也不是可运行的程序
>或批处理文件。
>No HADOOP_CONF_DIR set.
>Please specify it either in yarn-env.cmd or in the environment.

经过百度，是配置大数据环境`hadoop`时，里面的`yarn`与`node`中的`yarn`冲突了。

解决方法：

> 方法一：将`Hadoop`环境以及环境变量删除
>
> 方法二：把bin下的`yarn.cmd`改个名称，避免和`hadoop`的`yarn`冲突，配置好环境变量

最后再使用命令`yarn -v`，能正常显示版本号

