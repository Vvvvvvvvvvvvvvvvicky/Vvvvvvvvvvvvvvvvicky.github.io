title: Redis学习记录
date: 2020-11-22 21:22:28
tags: redis
categories: 学习

redis学习使用、问题记录。

<!--more-->

# redis 

## 安装

在终端进入下载后的目录，然后：

- 解压：tar zxvf redis-X.X.X.tar.gz
- 移动到：sudo mv redis-X.X.X /usr/local
- 切换到：cd /usr/local/redis-X.X.X/
- 编译测试：make test
- 编译安装：make install

完成安装。



## 使用

1.先开启redis服务端

终端录入redis-server

看到Port：6379，启动成功

2.再打开一个终端（前一个不要关）

终端录入redis-cli

即可测试验证

3.关闭

关闭客户端：shutdown

