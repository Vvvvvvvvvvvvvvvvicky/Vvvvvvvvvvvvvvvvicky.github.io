---
title: 突击webmagic  
date: 2018-03-27 10:45:27  
tags: [爬虫,webmagic]  
categories: 学习

---
Java爬虫框架
<!--more-->
# 主要包构成 #
## webmagic-core ##
核心包，包含爬虫基本模块和基本抽取器。  

## webmagic-extension ##
拓展模块，提供工具，包括注解格式定义爬虫、json、分布式支持。
注解方式：基于POJO增加注释

#### AfterExtractor
该接口是对注解方式抽取能力不足的补充。  
使用注解方式填充完字段后调用**afterProcess()**方法，在这个方法中可以直接访问已抽取的字段、补充需要抽取的字段，甚至做一些简单的输出和持久化操作(并不是很建议这么做)。

#### OOSpider
OOSpider是注解式爬虫的入口。  
这里调用**create()**方法将model类加入到爬虫的抽取中，这里是可以传入多个类的。
#### PageModelPipeline
定义该接口来选择结果的输出方式。  
PageModelPipeline目前包括ConsolePageModelPipeline、JsonFilePageModelPipeline、FilePageModelPipeline三个实现。


<br><br><br><br><br><br><br>
# 拓展包 #
## webmagic-saxon #
webmagic与saxon结合，saxon是xpath和xslt的解析工具。

## webmagic-selenium #
webmagic与selenium结合进行动态页面抓取，selenium可迷你浏览器进行页面渲染。



<br><br><br><br><br><br><br>
#模块划分#
<div style="width:50%;align:left" >  
<img src="http://code4craft.github.io/images/posts/webmagic.png"/>
</div>  
## DownLoader  
页面下载
### 实现
#### HttpClientDownloader
集成Apache HttpClient（Java http下载器，支持自定义http头（user-agent,cookie）、自动redirect、连接复用、cookie保留、设置代理等）
#### SeleniumDownloader
实现动态页面抓取



## PageProcessor - 链接提取和页面分析
实现PageProcessor可以**自定义**爬虫逻辑。  
### 核心方法  
#### public Page download(Request request, Task task)
task是包装了任务对应的Site信息的抽象接口。
#### public void setThread(int thread)
Downloader涉及连接池等。

### 核心方法  
#### public void process(Page page)  
| 方法 | 说明 |  
| ------: | :------- |  
| page.addTargetRequests() | 增加要抓取的URL |  
| page.putField() | 保存抽取结果 |   
| page.getHtml().xpath() | 按照某个规则对结果进行抽取|
| toString() | 返回单个String |  
| all() | 返回String列表 |  
#### public Site getSite()  
Site对象定义了爬虫的域名、起始地址、抓取间隔、编码等信息。

#### Selector 简化页面抽取
整合了cssSelector、xpath、正则表达式
SmartContentSelector 对于页面正文的自动抽取的类。
Xsoup对xpath的语法进行拓展，支持自定义函数（在xpath末尾加上/name-of-function
()）  
<table> <tr> <td width="100">函数</td> <td>说明</td> </tr> <tr> <td width="100">text(n)</td> <td>第n个文本节点(0表示取所有)</td> </tr> <tr> <td width="100">allText()</td> <td>包括子节点的所有文本</td> </tr> </tr> <tr> <td width="100">tidyText()</td> <td>包括子节点的所有文本，并进行智能换行</td> </tr> <tr> <td width="100">html()</td> <td>内部html(不包括当前标签本身)</td> </tr> <tr> <td width="100">outerHtml()</td> <td>外部html(包括当前标签本身)</td> </tr> <tr> <td width="100">regex(@attr,expr,group)</td> <td>正则表达式，@attr是抽取的属性(可省略)，expr是表达式内容，group为捕获组(可省略，默认为0)</td> </tr> </table>  



## Spider - 爬虫调度框架 #
爬虫入口（核心调度） 

<pre> Spider.create(blogProcessor)  
	.scheduler(new FileCacheQueueScheduler("/data/temp/webmagic/cache/"))  
	.pipeline(new FilePipeline())  
	.thread(10).run();  `
</pre>

核心处理流程

<pre>private void processRequest(Request request) {
        Page page = downloader.download(request, this);
        if (page == null) {
            sleep(site.getSleepTime());
            return;
        }
        pageProcessor.process(page);
        addRequest(page);
        for (Pipeline pipeline : pipelines) {
            pipeline.process(page, this);
        }
        sleep(site.getSleepTime());
    }
</pre>


## Scheduler - URL管理  
### 主要方法
#### public void push(Request request,Task task)
将待抓取的URL加入到Scheduler里面。request是对URL的一个封装，包括优先级、一个存储数据的Map

#### public Request poll(Task task)
从Scheduler中取出一条请求。

### 实现
#### QueueScheduler
#### FileCacheQueueScheduler
#### RedisScheduler




## Pipeline - 离线分析和持久化 #
结果输出和持久化。  
### 主要方法
public void process(ResultItems resultItems,Task task)
ResultItems是包含抽取结果的对象，通过ResultItems.get(key)可获取结果。
### 实现
#### ConsolePipeline 输出到控制台。
#### FilePipeline
#### JsonFilePipeline

### webmagic目前还不支持持久化到数据库。可以结合JFinal