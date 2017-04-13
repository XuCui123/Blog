---
title: Ruby版本升级（Mac）版
date: 2017-04-05 11:40:03
tags: 安装
---
### 一. 安装RVM

RVM(Ruby Version Manager),Ruby版本管理器用来升级ruby，RVM包含了Ruby的版本管理和Gem库管理(gemset)。
> 1、  RVM安装

'''bash'
$ curl -L get.rvm.io | bash -s stable
'''
> 2、  之后就是等待一段时间之后，就可以安装成功了，使用以下命令来验证

'''bash'
$ source ~/.bashrc
$ source ~/.bash_profile
'''
> 3、 测试是否安装正常

'''bash'
$ rvm -v
'''
### 二. 使用RVM升级Ruby

> 1、查看当前ruby版本

'''bash'
$ ruby -v
'''
> 2、列出已知ruby的版本

'''bash'
$ rvm list known
如果出现下列问题：A RVM version 1.29.1 (latest) is installed yet 1.21.20 (stable) is loaded.
Please do one of the following:
* 'rvm reload'
* open a new shell
* 'echo rvm_auto_reload_flag=1 >> ~/.rvmrc' # for auto reload with msg.
* 'echo rvm_auto_reload_flag=2 >> ~/.rvmrc' # for silent auto reload.
执行rvm reload
再执行rvm list known
'''
> 3、安装ruby 2.4.0

'''bash'
$ rvm install 2.4.0
'''
> 4、安装完之后，可以ruby -v测试是否安装成功

'''bash'
ruby -v
ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-darwin16]
'''
> 5.将该版本设置为默认的ruby版本

'''bash'
rvm use 2.4.0 --default
Using /Users/******/.rvm/gems/ruby-2.4.0
'''
> 6.ruby -v

'''bash'
ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-darwin16]
'''
