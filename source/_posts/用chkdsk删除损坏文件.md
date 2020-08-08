---
title: 用chkdsk删除损坏文件
date: 2018-03-23 19:18:45  
comments: true  
categories: 踩坑  
tags: [windows,踩坑]  

---
**Q**:系统盘文件夹已损坏无法直接删除，提示需要调用系统命令chkdsk删除该文件。
<!--more-->
**A**：cmd运行“chkdsk E: /f”扫描指定盘（E盘），自动检查之后进行删除，自动关闭。  
系统会检查出已损坏文件，并删除，健康文件依旧保留。  

![chkdsk处理坏文件](https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1521814233947&di=3e111ac9cd31867c4a6b504398d78ec1&imgtype=jpg&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F7af40ad162d9f2d31b76dfe6a5ec8a136327cc50.jpg "chkdsk处理坏文件")

<div id="container"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
  id: '<%= page.date %>'
  owner: 'Vvvvvvvvvvvvvvvvicky',
  repo: 'comment.github.io',
  oauth: {
    client_id: 'da11ae3e133507a54c29',
    client_secret: '5ee4f2c6cf5943d8437c673222e48f249bee5cf9',
  },
})
gitment.render('container')
</script>