---
title: 使用Hexo搭建博客（Mac版）
date: 2017-04-05 11:13:24
tags: 安装
---

官方文档：https://hexo.io/zh-cn/


> 安装前提：在安装前，您必须检查电脑中是否已安装下列应用程序：

- Node.js
- Git


### 安装 Hexo

```bash
$ npm install -g hexo-cli
```


### 建站

> 安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```


### 测试 Hexo

在整个配置完成后，打开终端，输入以下指令即可运行本地服务测试

```bash
$ hexo server
$ # 输入http://localhost:4000/即可打开默认页面
```


hexo文件夹目录结构

- `source`：博客资源文件夹
- `source/_drafts`：草稿文件夹
- `source/_posts`：文章文件夹
- `themes`：存放主题的文件夹
- `themes/landscape`：默认的主题
- `_config.yml`：全局配置文件


### 部署到 Github Pages

博客发布到Github Pages上，供外网访问，当然你也可以部署到其他服务器上，Github Pages服务的使用步骤：

1. 开通Github账号
2. 创建一个repository，名称开头必须和账号名一样，然后以.github.io结尾


修改配置文件：_config.yml，整个站点的配置都在这里，打开_config.yml文件，修改你的信息

```bash
deploy:
  type: git
  repo: https://github.com/YourName/YourName.github.io.git
  branch: master
```

> 如果要修改主题，只需要将主题文件clone到themes目录下，并修改_config.yml配置文件即可



### 新建博客

两种方式，一种通过命令生成一个博客样板，另一种是直接把Markdown文档拿来使用

1. 命令行生成
```bash
$ hexo new HelloWord
```
> 新生成的文章都会保存在 `source/_posts` 目录下，打开生成的模板,在分割线下面，就可以按照正常的Markdown格式进行写作
2. 文档拷贝：也可以将 Markdown 拷贝到 `source/_posts` 目录下


### 生成博客

新增了博客文章后，需要提交到服务器上，输入以下指令完成将博客生成静态Html文件

```bash
$ hexo generate
```

生成静态文件选项:

- `-d, --deploy`	文件生成后立即部署网站
- `-w, --watch`	监视文件变动

该命令可以简写为:

```bash
$ hexo g
```

### 发布博客到服务器

安装 hexo-deployer-git 工具:

```bash
$ npm install hexo-deployer-git --save
$ hexo deploy
```

部署网站参数	:
- `-g, --generate`	部署之前预先生成静态文件

> `hexo deploy` 命令可以简写为 `hexo d`
