---
title: Mac下安装MongoDB
date: 2017-05-21 20:40:30
tags: 安装
---
### 1. 使用homebrew安装，升级brew版本库

```bash
brew update
```
### 2. 安装mongodb

```bash
brew install mongodb
```

查看安装信息
```bash
brew info mongodb
```

查看mongodb的版本
```bash
mongo --version
```
### 3. 运行mongodb

创建一个数据库存储目录 /data/db：
```bash
sudo mkdir -p /data/db
```

启动 mongodb，默认数据库目录即为 /data/db：
```bash
sudo mongod
```
