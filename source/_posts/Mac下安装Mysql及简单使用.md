---
title: Mac下安装Mysql
date: 2017-05-06 19:14:59
tags: 安装
---
## 一.官网下载

### 1.官网下载地址： https://www.mysql.com/downloads/

### 2.在 https://dev.mysql.com/downloads/ 下找到MySQL Community Server进入下载页，选择合适的版本进行下载。下载页会显示登录和注册，直接选择“No thanks, just start my download.”


## 二.安装

### 1.下载完成后，点击安装，一直next，直到最后会出现一个初始密码，记下密码。

### 2.进入系统偏好设置，找到Mysql打开

### 3.在终端中运行下面指令，方便直接打开终端就可以运行Mysql
```bash
alias mysql=/usr/local/mysql/bin/mysql
alias mysqladmin=/usr/local/mysql/bin/mysqladmin
```
### 4.重置密码
```bash
mysqladmin -u root -p password newpass
```
newpass 是新密码，此时会需要输入安装第一步中留存的初始密码

### 5.用新密码登录
```bash
mysql -u root -p
```


## 三.简单使用

### 1.登录Mysql
```bash
mysql -u root -p
```
### 2.创建用户
```bash
创建用户
insert into mysql.user(Host,User,Password) values("localhost","user1",password("123456"));

刷新系统权限
flush privileges;

退出当前用户
exit

用新用户登录
mysql -u user1 -p
```

### 3.为用户授权
```bash
root用户登录
mysql -u root -p

赋予任何主机访问数据的权限
grant all privileges on . to 'user1'@'%' with grant option ;
grant all privileges on . to 'user1'@'%' identified by '123456';
flush privileges;

或只在localhost下访问数据
grant all privileges on . to 'user1'@'localhost' with grant option;
grant all privileges on . to 'user1'@'localhost' identified by '123456′;
flush privileges;

允许用户从某IP地址的主机连接到Mysql服务器
grant all privileges on . to 'user1'@'123.123.1.1' with grant option ;
grant all privileges on . to 'user1'@'%' identified by '123456';
flush privileges;
```

### 4.为用户创建数据库
```bash
root用户登录
mysql -u root -p

创建数据库
create database user1DB;
grant all privileges on user1DB.* to user1@localhost identified by '123456';
flush privileges;

或指定部分权限分给某用户
grant select,update on user1DB.* to user1@localhost identified by '123456';
flush privileges;
```

### 5.数据库操作
```bash
显示Mysql中所有数据库
show databases;

打开一个数据库
use user1DB;

显示数据库中所有表
show tables;

创建一个表
CREATE TABLE Persons
(
Id_P int primary key,
LastName varchar(255) not null,
FirstName varchar(255) not null,
Address varchar(255),
City varchar(255)
)

添加记录
insert into 表名 （字段1，字段2，...） values('值1'，‘值2’，...);
或者指定所要插入数据的列
insert into table_name (列1, 列2,...) VALUES (值1, 值2,....)

删除记录
delete from 表名称 where 列名称 = 值；

更新记录
update 表名称 set 列名称 = 新值 where 列名称 = 某值
```
### 6.删除用户
```bash
root用户登录
mysql -u root -p

删除用户
DELETE FROM user WHERE User="user1" and Host="localhost";

刷新系统权限
flush privileges;

删除用户数据库
drop database user1DB;

### 7.修改指定用户密码
```bash
root用户登录
mysql -u root -p

修改密码
update mysql.user set password=password('新密码') where User="user1" and Host="localhost";
刷新系统权限
flush privileges;
```

Mac下的Mysql安装及使用
