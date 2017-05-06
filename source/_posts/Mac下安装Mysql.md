---
title: Mac下安装Mysql
date: 2017-05-06 19:14:59
tags: 安装
---
## 一.官网下载

### 1.官网下载地址： https://www.mysql.com/downloads/

### 2.在 https://dev.mysql.com/downloads/ 下找到MySQL Community Server进入下载页，选择合适的版本进行下载。下载页会显示登录和注册，直接选择“No thanks, just start my download.”

## 二.安装

### 1.下载完成后，点击安装，一直next，知道最后会出现一个初始密码，记下密码。

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
