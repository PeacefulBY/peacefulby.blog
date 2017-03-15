---
title: Neo4j简介、版本说明与安装配置
tags:
  - graph database
  - neo4j
  - nosql
  - 图数据库
id: 141
categories:
  - 图数据库
date: 2014-04-07 21:46:18
---

[![neo4j](http://peacefulby.com/wp-content/uploads/2014/02/neo4j2.png)](http://peacefulby.com/wp-content/uploads/2014/02/neo4j2.png)

### Neo4j简介

<span style="line-height: 1.5em;">随着社交网站的不断发展，数据量越来越大，原来用传统RDBMS存储数据的应用面临新的挑战。一些典型的社交网站例如Facebook、Linkedin等，用户以及用户之间的关系可以用一张图来表示；在RDBMS中，如果要存储一张图来表示用户和用户之间的关系，一般会将用户（节点）和关系（边）分别存储为两张表，这样带来的问题就在于，当需要快速地在图中进行遍历（例如在Linkedin中回答“如何通过最少的人找到XX公司的HR”这类问题）或执行一些其他的图操作时，往往捉襟见肘：要么耗费大量时间在关系表上不断地做关联操作，要么耗费大量内存将整张图或部分图缓存起来。</span>

为了解决上面基于图数据存储、遍历等一系列问题，[Neo4j](http://www.neo4j.org)应运而生（类似的图数据库还有Infinite Graph等）。Neo4j是一个基于Java开发的、完全兼容ACID的开源图形数据库。与RDBMS不同，Neo4j针对图结构在存储等方面进行了专门的索引和优化。Neo4j中有五种主要的存储结构与概念:

1、Node：Neo4j中的基本结构，表示结点。

2、Relation：Neo4j中的基本结构，表示一条有向边，也即两个节点的关系。

3、Property：key-value键值对，表示Node和Relation的属性（一个Node或Relation可以有多个属性）

4、Index：Node或Relation的索引，可以通过索引建立key-value键值对，实现到Node或Relation的映射。

5、Traversal：根据一定条件对图进行遍历的过程。可以指定方向，深度，优先条件（深度优先、广度优先）等条件。

&nbsp;

### Neo4j版本说明

Neo4j目前一共有4个版本：社区版（免费）、个人版（登记后免费）、中小企业版（12K刀一年）、商业版（根据具体情况收费），其中后面三个功能基本一致，不同在于Email、电话等服务方面；社区版比后三者相比，主要是不支持集群和高性能Cache。详细见：[http://www.neotechnology.com/price-list/](http://www.neotechnology.com/price-list/)

版本号方面，需要注意的一点是Neo4j2.0不支持Java6，需要Java7（详见 [ChangeLog](http://www.neo4j.org/release-notes)）；1.9版本最新支持的发行版为1.9.6

&nbsp;

### Neo4j安装配置

在[这里](http://www.neo4j.org/download/other_versions)选择相应的操作系统和版本下载安装包并解压；Linux下在解压后的根目录，Neo4j2.0版本执行bin/neo4j-installer install，1.9以下版本执行bin/neo4j install进行安装

安装完成后，执行bin/neo4j start启动服务

一些常用配置项，更多可参考[官方文档](http://docs.neo4j.org/chunked/stable/configuration-jvm.html)：

内存：conf/neo4j-wrapper.conf

[cc lang='java' line_numbers='false']

wrapper.java.initmemory=4000  //初始化内存，单位MB

wrapper.java.maxmemory=8000  //最大占用内存，单位MB

[/cc]

Web访问：conf/neo4j-server.properties

[cc lang='java' line_numbers='false']org.neo4j.server.webserver.address=0.0.0.0  //开放Web管理页面，用于外部访问[/cc]

自动索引：conf/neo4j.properties

[cc lang='java' line_numbers='false']

node_auto_indexing=true

node_keys_indexable=  //节点自动索引字段

relationship_auto_indexing=true

relationship_keys_indexable=  //边自动索引字段

[/cc]