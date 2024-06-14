---
title: PHP基础
top_img: transparent
tags: PHP
abbrlink: 42694
date: 2021-04-04 12:38:51
---



## 基础知识

1.PHP的主要目标是允许网络开发人员快速编写动态页面。

2.PHP可以用于收集表单数据，生成动态网页，字符串处理，动态输出图像，处理服务器端文件，与数据库交互，会话跟踪，处理XML文件，处理大量的网络协议，服务器端的相关操作。

3.PHP是脚本语言，不需要事先编译，在服务器端运行。

4.url地址

格式：http://host[:port][abs_path]

http://   表示要通过HTTP协议来定位网络资源

host     表示合法的Internet主机或者IP地址

port      指定一个端口号，可以省略默认为80

abs_path 被请求资源（文件）的位置(目录)

例：https://www.bilibili.com/video/BV1ct411S7nj

5.![image-20200810162458016](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200810162458016.png)

## PHP运行环境安装

1.需要安装的软件

（1）web服务器                                                                     apache

（2）PHP应用服务器----解释、执行我们编写的PHP程序      PHP

（3）数据库管理系统----数据库服务器                                   MySQL              

集成环境--wampserver

2.安装之后的访问方法

127.0.0.1 (ip)               localhost(域名)

3.被访问的界面放在哪里

C:\wamp64\www

http://localhost/           （ / 即被请求资源的位置，单独的一个 / 表示根目录）

站点根目录

http://localhost/         http://localhost/index.php  （同样的效果）

访问某个文件夹，默认会访问这个文件夹下面的index.php或者index.html，若没有，将所有文件列出来。

![image-20200810171616713](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200810171616713.png)

4.只有放在C:\wamp64\www目录下的文件才会被访问

## 编辑器安装

## 基本语法（1）初识PHP脚本程序

1.开始标记  <?php

   结束标记  ?>

（1）<?php  ?>之间就表示进入PHP模式，在开始和结束标记之外的内容都会被PHP解析器忽略。

（2）可以直接嵌入到html代码中，并且可以嵌入任意多个。

（3）文件末尾的PHP代码段结束标记可以不要，在一些情况下省略更好。

2.指令分隔符“分号”

（1）PHP语言分为两类：一种是在程序中使用结构定义语句，结尾不需要使用分号；另一种是在程序中使用功能执行语句，必需用分号结尾。

（2）结束标志 ?> 就隐含一个分号，所以PHP代码最后一行可以不用加分号。

3.注释

（1）/*多行注释*/

（2）//单行注释

（3）#

4.空白符包括空格、Tab制表符、换行都是无用的。

## 基础语法（2）变量

变量是用于临时（只有在程序运行过程中才存在）存储值（数据）的容器。

1.变量的声明：

PHP不要求在使用变量前声明变量，当第一次给一个变量赋值时，才创建了这个变量，变量用于存储数字、文本字符串或者数组。一旦设置了某个变量，就可以在脚本中重复地使用它。

PHP中变量必须使用$符号，后边跟着变量名，用赋值操作符（=）给变量赋值。

2.变量的释放：

unset($变量名称)

3.变量的命名规则：

（1）变量名是严格区分大小写的；

（2）变量名由字母或者下划线开头，后面可以跟上任意数量的字母、数字、下划线；

（3）最好不用关键字作为变量命名。

4.可变变量：

$abc="test";

$abc="小明";

echo $test;

5.变量引用赋值：

$b=$a;//把$a的值赋值一份给变量$b

$b=&$a;//给$a起了一个别名，共用关系，操作其中一个会影响另外一个变量的值

$a=100;

echo $b;

## 基础语法（3）变量的类型

使用var_dump(变量名)可以输出变量的类型。

1.变量的类型

（1）bool（布尔型）

![image-20200813103023901](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200813103023901.png)

（2）int（整型）

（3）float(浮点型，也称double)

（4）string(字符串)

（5）array(数组)

（6）object(对象)

（7）resource(资源)

（8）NULL

2.变量类型相互转换

（1）自动类型转换

![image-20200813104255411](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200813104255411.png)

（2）强制类型转换

![image-20200813104323808](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200813104323808.png)

$a='周四';

$b=(int)$a;（输出0）

## 基础语法（4）常量

1.常量是用于临时（只有在程序运行过程中才存在）存储值（数据）的容器。

2.常量的定义和使用

define('常量名称'，常量值)或者define("常量名称"，常量值)

常量的命名也遵循PHP标识符的命名规则（数字、字母、下划线），按照惯例常量标识符总是大写的。

define('MY_NAME','张三');

defined()函数检查是否定义了某个常量。

3.常量和变量的区别

（1）常量前面没有$符号

（2）常量只能用define()函数定义，不能通过赋值语句

（3）常量可以不用理会变量范围的规则而在任何地方被定义和使用

（4）常量一旦被定义就不能被重新定义或者取消

（5）常量的值只能是bool,int,float,string类型

4.预定义常量

PHP内核已经帮我们定义好了的常量（不区分大小写）

print_r(get_defined_constanta());

echo _FILE_;//输出文件的位置

## 基础语法（5）--- 运算符

1.算数运算符

![image-20200813112651859](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200813112651859.png)

2.字符串运算符

.    连接运算符

$a='123';

$b='456';

echo $a.$b;

3.赋值运算符

![image-20200813113551083](C:\Users\48755\AppData\Roaming\Typora\typora-user-images\image-20200813113551083.png)



















