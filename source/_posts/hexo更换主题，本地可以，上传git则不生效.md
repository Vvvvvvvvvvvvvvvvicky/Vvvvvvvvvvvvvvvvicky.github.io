---
title: hexo更换主题，本地可以，上传git则不生效
date: 2018-03-23 21:40:54  
comments: true  
categories: 踩坑  
tags: [hexo,theme,踩坑]  

---
**Q**:运行原主题landscape正常，更换主题后，hexo g生成文件，hexo s使其在本地运行，运行正常，hexo d上传到github，访问出现空白无内容以及乱码。 
<!--more-->
**A**:查询了一些资料,得到这可能是hexo的缓存的问题，即根目录的db.json文件。所以在发布网站之前，先用hexo clean清除缓存，然后再部署网站。  

清除缓存的方法：  
1. 执行命令：hexo clean  
2. 然后可以生成静态博客并在本地预览：hexo g ; hexo s

**另**：在多次上传后，同一浏览器存在缓存，故导致改变不能立刻显示，利用Ctrl+F5强制刷新。