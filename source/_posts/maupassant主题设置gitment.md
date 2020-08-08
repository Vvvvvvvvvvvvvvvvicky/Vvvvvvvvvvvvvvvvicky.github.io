---
title: maupassant主题设置gitment
date: 2018-03-25 13:25:13
comments: true  
tags: [hexo,gitment,踩坑]  
categories: 踩坑  
---
maupassant主题设置gitment踩坑记录。
<!--more-->
1.在主题的配置文件_config.yml中更改配置如下：
<div style="width:70%;align:left" >
<img src="https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1521966153467&di=17a022292609fafdfa8aff705fb38d39&imgtype=jpg&src=http%3A%2F%2Fh.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F500fd9f9d72a605932b1f9162434349b033bba1c.jpg"/>
</div>  
* 注意大小写，写错会报“Error: Not Found”） 

2.修改文件Blog\themes\maupassant\layout\_partial\comments.pug，设置样式内容：
<div style="width:90%;align:left" >
<img src="https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1521966602824&di=23bc17b1564c7b55592c0d23aef66241&imgtype=jpg&src=http%3A%2F%2Ff.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2Fac6eddc451da81cba4a986c15e66d0160924316a.jpg"/>
</div>

<pre><code>
link(rel='stylesheet', href='https://imsun.github.io/gitment/style/default.css')  
script(src='https://imsun.github.io/gitment/dist/gitment.browser.js')</code>
</pre>
将划线部分复制粘贴，并补充将id值改为page.date（如不加，则默认传入文章url，超过50个字符报错“Error：validation failed”）

3.在每篇的开头部分补充  comments: true  
<div style="width:30%;align:left" >
<img src="https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1521967111606&di=0dede719fa62743754e6e7eeaf6c5777&imgtype=jpg&src=http%3A%2F%2Fa.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F8718367adab44aedfe61b8e8bf1c8701a18bfb8b.jpg"/>
</div>