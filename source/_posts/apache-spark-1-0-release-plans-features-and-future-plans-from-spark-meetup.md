---
title: Spark 1.0 发布计划、版本特性与未来计划（From Spark Meetup）
tags:
  - spark
id: 192
categories:
  - Spark
date: 2014-04-28 15:10:40
---

上周由<span style="color: rgba(0, 0, 0, 0.670588);">Patrick Wendell（Databricks创始人之一）主讲的[Spark Meetup](http://www.meetup.com/spark-users/)透露了Spark 1.0的发布计划、版本特性以及未来的一些发展计划</span>

<span style="color: rgba(0, 0, 0, 0.670588);">演讲视频见：[http://www.youtube.com/watch?v=NUQ-8to2XAk](http://www.youtube.com/watch?v=NUQ-8to2XAk)</span>

演讲ppt如下：

<iframe src="https://onedrive.live.com/embed?cid=FF5D4889707A3D16&amp;resid=FF5D4889707A3D16%21107&amp;authkey=AJrQinIrJBLnFko&amp;em=2" width="602" height="407" frameborder="0" scrolling="no"></iframe>

&nbsp;

**结合Meetup和之前Spark中国峰会的消息<span style="color: rgba(0, 0, 0, 0.670588);">，Spark 1.0会在最近的两周发布，目前代码已冻结，也不会再进行Feature的增加，在进行最后的测试和bug fix中；Spark计划以三个月为周期迭代，因此Spark 1.1预计在8月份到来</span>**

ppt中比较有意思的是下面这张Slide，展示了近30天Spark与MapReduce、Storm、Yarn代码更新情况的对比，从对比中可以看到，Spark在近期的活跃度要远远高于其他三个项目（btw，我觉得一部分原因是因为Spark 1.0即将发布，各种Pacth和Bug fix等也会较为频繁，如果能增加一张Active Contributor数量对比图会更有说服力一些）

[![Spark 1.0 Meetup](http://peacefulby.com/wp-content/uploads/2014/04/Spark-1.0-Meetup-600x450.png)](http://peacefulby.com/wp-content/uploads/2014/04/Spark-1.0-Meetup.png)

从演讲视频与ppt来看，Spark 1.0以下几点新特性是我比较关注的：

1、基于<span style="color: #222222;">Catalyst的Spark SQL支持</span>

由于多数企业对于大数据的应用场景停留在统计分析层面，这一新特性或者说新功能可以说这是最令人期待的。相比于目前Spark给出的解决方案Shark构建在Hive的SQL优化引擎之上，Spark SQL将采用内置的<span style="color: #222222;">Catalyst引擎用于SQL计划生成和优化；对于Spark SQL的优势我的理解是采用内置引擎一方面给后续的持续优化和改进提供可能，另一方面内置类型SchemaRDD可以向前接入其他RDD如TextRDD等，向后可以直接导出到机器学习库MLlib等作为输入，使用上更为灵活。更多Shark与Spark SQL的区别可以参见[@连城](http://weibo.com/lianchengzju) 老师在知乎上的这篇回答：[http://www.zhihu.com/question/23182567](http://www.zhihu.com/question/23182567)</span>

2、Java8支持

对于大部分没有接触过Scala的程序员来说，上手Scala还是有一定难度的，或者需要一定时间的学习；为了让更多人接触Spark，Spark 1.0对Java8进行了支持，同时对原有的Python接口进行了进一步的覆盖与扩展。以Java8为例，原来的函数需要在外部定义：
<pre>[cc lang='java' escaped='true']
class Split extends FlatMapFunction&lt;String, String&gt; {
  public Iterable&lt;String&gt; call(String s) {
    return Arrays.asList(s.split(" "));
  }
);
JavaRDD&lt;String&gt; words = lines.flatMap(new Split());
[/cc]</pre>
在Java8引入了Lambda表达式后，代码将更为简洁，也更贴近Scala/Python的语法：
<pre>[cc lang='java' escaped='true']
JavaRDD&lt;String&gt; words = lines.flatMap(s -&gt; Arrays.asList(s.split(" ")));
[/cc]</pre>
3、MLlib扩展

作为一个基于内存的分布式计算框架，Spark在迭代式计算方面有很大的优势，也是许多机器学习算法发挥的地方，因此在过去6个月内，有多达35位Contributor在Spark的机器学习库MLlib上贡献，尽可能大地发挥Spark的长处。结合Meetup与峰会上[@尹绪森](http://weibo.com/yinxusen) 老师的演讲来看，MLlib至少会加入以下一些新的API或算法：

（1）Vector/Matrix（dense or sparse）RDD的引入，方便开发者实现自己的ML算法

（2）决策树算法

（3）评估方法，包括AUC、ROC、Precision-Recall、F-measure等

（4）SVD、PCA

（5）Gibbs Sampling和LDA（[@尹绪森](http://weibo.com/yinxusen) 实现）

除了以上三点，Spark 1.0还在WebUI方面增加了一些支持，可以查看更详细的eventLog和支持取消Job的操作；开发文档方面也更加完善，可见：[http://www.cs.berkeley.edu/~marmbrus/sparkdocs/_site/api/core/index.html](http://www.cs.berkeley.edu/~marmbrus/sparkdocs/_site/api/core/index.html)

在未来的Spark 1.1以及以后的版本，预计会继续完善Catalyst引擎并推广应用到Shark等产品当中，同时继续优化现有框架的性能和可用性，例如提供External Shuffle等，Streaming方面与Flume和Kafka的对接也在不断完善