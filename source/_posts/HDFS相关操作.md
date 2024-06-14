---
title: HDFS相关操作
top_img: transparent
tags: 
  - hadoop
abbrlink: 34797
date: 2021-05-15 16:47:55
---

# `HDFS`

## `Hadoop`主要目录

- `bin`目录：存放对`Hadoop`相关服务（HDFS,YARN）进行操作的脚本
- `etc`目录：`Hadoop`的配置文件目录，存放`Hadoop`的配置文件
- `lib`目录：存放`Hadoop`的本地库（对数据进行压缩解压缩功能）
- `sbin`目录：存放启动或停止`Hadoop`相关服务的脚本
- `share`目录：存放`Hadoop`的依赖`jar`包，文档和官方案例

## `HDFS`

1.定义：`HDFS`是一个文件系统，用于存储文件，通过目录树来定位文件；其次，它是分布式的，由很多服务器联合起来实现其功能，集群中的服务器有各自的角色。

2.使用场景：适合一次写入，多次读出的场景，且不支持文件的修改。适合用来做数据分析，并不适合用来做网盘应用。

## `HDFS`常用命令

```shell
#启动Hadoop
cd /usr/local/hadoop
./sbin/start-all.sh
./sbin/start-dfs.sh
./sbin/start-yarn.sh

#jps查看进程
jps

#基本语法
bin/hadoop fs <具体命令>
bin/hdfs dfs <具体命令>

#查看hdfs支持哪些操作
hdfs dfs

# -help 输出该命令参数
hadoop fs -help rm
hdfs dfs -help rm

# -ls 显示目录信息
hadoop fs -ls /
hdfs dfs -ls /

# -mkdir 在hdfs上创建目录
hdfs dfs -mkdir -p /user/hadoop

# -moveFromLocal 从本地剪切粘贴到hdfs
hdfs dfs -moveFromLocal /home/abc.txt /user/hadoop

# -appendToFile 追加一个文件到已存在的文件末尾
hdfs dfs -appendToFile ./word.txt /user/hadoop/input/abc.txt

# -cat 显示文件内容
hdfs dfs -cat /user/hadoop/input/abc.txt

# -chgrp -chmod -chown 修改文件所属权限
hdfs dfs -chmod 666 /user/hadoop/input/abc.txt

# -copyFromLocal == -put从本地文件系统拷贝文件到hdfs路径去
hdfs dfs -copyFromLocal ./word.txt /user/hadoop/input
hdfs dfs -put./word.txt /user/hadoop/input

# -copyToLocal 从hdfs拷贝文件到本地  -get 从hdfs下载文件到本地  -getmerge 从hdfs合并下载多个文件到本地
hdfs dfs -copyToLocal /user/hadoop/input/abc.txt ./
hdfs dfs -get /user/hadoop/input/abc.txt ./
hdfs dfs -getmerge /user/hadoop/input/* ./abc.txt

# -cp 从hdfs的一个路径拷贝到hdfs的另一个路径
hdfs dfs -cp /input/test.txt /user/hadoop/input

# -mv 在hdfs目录中移动文件
hdfs dfs -mv /user/hadoop/input/abc.txt /input

# -tail 显示一个文件的末尾
hdfs dfs -tail /user/hadoop/input/abc.txt

# -rm 删除文件或文件夹
hdfs dfs -rm -r /user/hadoop/input/*

# -rmdir 删除空目录
hdfs dfs -rmdir /input

# -du 统计文件夹的大小信息
hdfs dfs -du -s -h /user/hadoop/input
hdfs dfs -du -h /user/hadoop/input

# -setrep 设置hdfs中文件的副本数量
hdfs dfs -setrep 10 /user/hadoop/input/abc.txt
```













