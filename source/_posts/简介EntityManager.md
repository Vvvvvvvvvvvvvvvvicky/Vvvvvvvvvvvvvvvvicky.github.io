---
title: EntityManager相关
date: 2017-10-05 23:37:54  
comments: true  
tags: Java  
categories: 学习  

---
EntityManager的含义及用法
<!--more-->
### EntityManager介绍
EntityManager是JPA操作基础，获取到EntityManager实例后，才能通过JPA对数据库进行操作，类似于Connection实例和JDBC的关系。
### 什么是JPA
**JPA —— Java Persistence API  Java持久化API**  
定义了 对象-关系映射+实体对象持久化标准接口  
JPA在持久化上下文中维护实体生命周期：  
&nbsp;&nbsp;1. ORM元数据（支持annotation和xml）  
&nbsp;&nbsp;2. 实体CRUD操作  
&nbsp;&nbsp;2. 查询JPQL  

### 实体的生命周期
1. new ——新创建的实体对象，未分配主键值  
2. managed ——被EntityManager管理，处于Persistence Context  
3. detached ——处于Application Domain，在Persistance Context之外  
4. removed ——对象被删除  

#### 方法：
1. persist ——持久化（将新建或已删除的实体变为managed状态，存库）  
2. remove ——删除实体  
3. merge ——游离实体变为managed，存库  
<div style="width:60%;align:center" >  
<img src="https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1507292305525&di=5c933128fa51ab422023b3310969573d&imgtype=jpg&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2Fa9d3fd1f4134970a2c76ab5b9ecad1c8a7865db8.jpg"/>
</div>  

### 实体关系映射 ORM
#### 基本映射  
| 对象 | 数据库 | annotation | 可选annotation |  
| :------ | :------- | :--------- | :------ |  
| Class | Table | @Entity | @Table(name="tableName") |  
| property | colum | @Id | @GeneratedValue |  
| property | primary key | @Entity | @Table(name="tableName") |  
| property | NONE | @Transient |     |  

#### ID生成策略
1. GeneratorType.AUTO JPA自动生成
2. GenerationType.IDENTITY 数据库自增长
3. GenerationType.SEQUENCE 数据库序列号
4. GenerationType.TABLE 数据库表记录ID的增长（需定义一个TableGenarator）

#### 关联关系
| 关系类型 | Owning-Side | Inverse-Side |  
| :------ | :------- | :--------- |  
| one-to-one | @OneToOne | @OneToOne(mappedBy="othersideName") |  
| one-to-many / @ManyToOne | colum | @OneToMany(mappedBy="xxx") |  
| many-to-many | @ManyToMany | @ManyToMany(mappedBy ="xxx") |  

### 查询语言
1. 根据主键查询，EntityManager的find方法：T find(Class entityClass, Object primaryKey)  
2. 使用JPQL查询语言（完全面向对象，类似hibernate HQL），使用EntityManager的createQuery方法：Query createQuery(String qlString)  
##### EntityManager的各个方法
![EntityManager方法](https://timgsa.baidu.com/timg?image&quality=80%20&size=b10000_10000&sec=1507467896237&di=7ce1661ed3e030471ba1624402867d55&imgtype=jpg&src=http%3A%2F%2Fb.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F91529822720e0cf30e1627830146f21fbf09aae1.jpg)
