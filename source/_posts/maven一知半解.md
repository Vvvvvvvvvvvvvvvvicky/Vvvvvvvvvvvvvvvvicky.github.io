---
title: maven一知半解
date: 2020-03-29 19:07:53
tags: maven
categories: 学习
---

maven操作的各种问题记录

<!--more-->

- [1.mvn clean install 和 mvn clean 区别](#1-mvn-clean-install---mvn-clean---)
- [2.mvn clean package -X 就能看到非常丰富的DEBUG信息](#2-mvn-clean-package--x----------debug--)



## 1.mvn clean install 和 mvn clean 区别

现象发生的场景：mvn install后，新改的内容不生效，一定要后来使用mvn clean install 才生效。

mvn install ：compile -> package -> test


org.codehaus.plexus.archiver.AbstractArchiver中的关键一段，用来判断是否强制新建jar
```java
protected boolean checkForced() throws ArchiverException
{
    if ( !isForced() && isSupportingForced() && isUptodate() )
    {
        getLogger().debug( "Archive " + getDestFile() + " is uptodate.");
        return false;
    }
    return true;
}
```

代码中提到有这么几个情况，会认为jar包不是最新的：
1. jar包不存在（其实就是mvn clean的效果）
2. 传入比较的文件资源不存在
3. Resource with unknown modification date found，资源的修改时间未知
4. Resource with newer modification date found，jar包的最后修改时间比资源的最后修改时间早

总结：
1. mvn clean 得到的jar包是最新的，除非其他方式修改jar包中的内容而不修改源代码。
2. 日常可以用mvn install，不进行chean，以节省时间；但最保险还是用 mvn clean install 生成最新的jar包或其他包
3. 不想用mvn clean又想保证jar包最新，建议添加 -Djar.forceCreation 参数



## 2.mvn clean package -X 就能看到非常丰富的DEBUG信息


