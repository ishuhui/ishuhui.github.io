---
title: 使用Mybatis进行简单的查询
top_img: transparent
tags: JavaWeb
abbrlink: 34221
date: 2021-04-20 20:55:43
---

# Mybatis三层架构的基本概念

- 持久层：主要完成与数据库相关的操作，即数据库的增删改查。

  因为数据库访问的对象一般称为Data Access Object，所以持久层又叫DAO层。

- 业务层：主要根据功能需求完成业务逻辑的定义和实现。

  主要为上层提供服务，所以又叫Service层或Business层。

- 表现层：主要完成与最终软件使用用户的交互，需要有交互界面（UI）。

  又称表现层为Web层或View层。

三层架构之间的调用关系为：表现层调用业务层，业务层调用持久层。

各层之间需要进行数据交互，一般使用java实体对象来传递参数。

# ORM思想

ORM（Object Relational Mapping）对象关系映射

- O（对象模型）：实体对象，即我们在程序中根据数据库表结构建立的一个个实体javaBean

- R（关系型数据库的数据结构）：关系数据领域的Relational（建立的数据库表）

- M（映射）：


从R（数据库）到O（对象模型）的映射，可以通过XML文件映射。

| O    | User实体                   |
| ---- | -------------------------- |
| R    | user表                     |
| M    | 建立User实体和user表的映射 |

实现：

（1）让实体类和数据库表进行一一对应关系

先让实体类和数据库表对应

再让实体类属性和表里面的字段对应

（2）不需要直接操作数据库表，直接操作表对应的实体类对象

# 案例

## 案例需求：

通过mybatis查询数据库user表的所有记录，封装到User对象中，打印到控制台上。

## 步骤分析：

1. 创建数据库及user表

2. 创建maven工程，导入依赖（MySQL驱动、mybatis、junit）

3. 编写User实体类

4. 编写UserMapper.xml映射配置文件（ORM）思想

5. 编写SqlMapConfig.xml核心配置文件

   数据库环境配置

   映射关系配置的引入（引入映射配置文件的路径）

6. 编写测试代码

   1.加载核心配置文件

   2.获取sqlSessionFactory工厂对象

   3.获取sqlSession会话对象

   4.执行sql

   5.打印结果

   6.释放资源

## 代码实现：

### 1.创建user数据表

```mysql
#创建数据库
CREATE DATABASE mybatis_db;
#使用这个数据库
USE mybatis_db;

#创建表
CREATE TABLE USER (
	`id` INT ( 11 ) NOT NULL auto_increment,
	`username` VARCHAR ( 32 ) NOT NULL COMMENT '用户名',
	`birthday` datetime DEFAULT NULL COMMENT '生日',
	`sex` CHAR ( 1 ) DEFAULT NULL COMMENT '性别',
	`address` VARCHAR ( 256 ) DEFAULT NULL COMMENT '地址',
PRIMARY KEY ( `id` ) 
) ENGINE = INNODB DEFAULT CHARSET = utf8;

#向表中添加数据
INSERT INTO USER ( `id`, `username`, `birthday`, `sex`, `address` )
VALUES
	( 1, '张三', '2020-1-12 00:25:45', '男', '北京' ),
	( 2, '小红', '2020-5-11 12:50:22', '女', '上海' );
```

### 2.创建maven工程，导入依赖（MySQL驱动、mybatis、junit）



```xml
<dependencies>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.6</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.6</version>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        
 </dependencies>
```

### 3.编写User实体类

```java
package com.luoshi.demo.entity;

import java.util.Date;

public class User {
    private int id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", birthday=" + birthday +
                ", sex='" + sex + '\'' +
                ", address='" + address + '\'' +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public Date getBirthday() {
        return birthday;
    }

    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
```

```java
package com.luoshi.demo.dao;

import com.luoshi.demo.entity.User;

import java.util.List;

public interface UserMapper {
    //查询所有
    List<User> findAll();
}

```

### 4.编写UserMapper.xml映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.luoshi.demo.dao.UserMapper">
    <select id="findAll" resultType="com.luoshi.demo.entity.User">
        select * from user
    </select>
</mapper>
```

### 5.编写SqlMapConfig.xml核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://8.136.206.177:3306/mybatis_db"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="UserMapper.xml"/>
    </mappers>
</configuration>
```

### 6.编写测试代码

```java
import com.luoshi.demo.dao.UserMapper;
import com.luoshi.demo.entity.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import javax.imageio.IIOException;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class mybatisTest {
    @Test
    public void test(){

        try {
            //加载核心配置文件
            InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");

            //获取SqlSessionFactory工厂对象
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);

            //获取SqlSession会话对象
            SqlSession sqlSession = sqlSessionFactory.openSession();

            //获取映射
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);

            //执行sql
            List<User> all=mapper.findAll();
            for(User user:all){
                //打印结果
                System.out.println(user);
            }

            //释放资源
            sqlSession.close();

        }catch (IOException e){
            e.printStackTrace();
        }

    }
}
```





