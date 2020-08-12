---
title: hexo使用
date: 2020-03-29 20:17:16
tags: hexo
categories: 学习记录
---



记录了我使用到hexo的一些问题（从3月29日起）。

前面使用到的后续再补充上来。

<!--more-->

- [1.markdown的原生TOC生成目录方式对github不支持](#1markdown---toc-------github---)
- [2.常用hexo命令](#2--hexo--)



## 1.markdown的原生TOC生成目录方式对github不支持

在线生成工具 [markdown-toc](https://ecotrust-canada.github.io/markdown-toc/)

## 2.常用hexo命令

hexo clean 清空缓存文件

hexo generate （或hexo g）

hexo deploy（或hexo d）d

hexo server （或hexo s）



## 3.hexo迁移

参考：

[hexo迁移1](https://www.jianshu.com/p/153490a029a5)

[hexo迁移2](https://blog.csdn.net/white_idiot/article/details/80685990)

原理：新建hexo分支，保存以下内容：

| 文件（夹）   | 说明                                            |
| ------------ | ----------------------------------------------- |
| scaffolds/   | 博客文章的模版                                  |
| source/      | 所有博客文章，以及about、tags、categories等page |
| themes/      | 网站的主题（备份时需删除内部.git）              |
| .gitignore   | 在push时需要忽略的文件和文件夹                  |
| _config.yml  | 站点配置文件                                    |
| package.json | 依赖包的名称和版本号                            |

推到远程仓库备份时，选择hexo分支为默认分支。

编辑 **_config.yml**站点配置文件，设置branch为master

下次更换电脑，直接clone代码后npm install即可。



## 4.hexo部署后样式丢失

查看本地文件发现错误生成了`css/style.scss`

运行`npm install hexo-renderer-scss --save`后再`Hexo g`问题解决。