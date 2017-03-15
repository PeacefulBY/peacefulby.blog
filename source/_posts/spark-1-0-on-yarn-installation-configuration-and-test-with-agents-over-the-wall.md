---
title: Spark 1.0 on Yarn安装配置与测试（附翻墙代理）
tags:
  - apache
  - hadoop
  - spark
  - yarn
id: 169
categories:
  - Spark
date: 2014-05-03 23:51:36
---

Spark 1.0应该很快要发布了，等不急于是手痒下载源码编译安装了一下，记录一下过程；由于目前公司已有Hadoop 2.2.0集群，因此主要试用了一下Spark on Yarn模式

**集群环境**：Hadoop-2.2.0

**客户端环境**：CentOS 6.2、Java 6

**客户端待安装**：Scala 2.10.4、Spark 1.0.0（SNAPSHOT）

&nbsp;

### 1、安装scala 2.10.4

根据Spark 源码里的文档，Spark 1.0.0依赖于scala 2.10.4，不过应该2.10.x版的都可以

下载[scala 2.10.4](http://www.scala-lang.org/files/archive/scala-2.10.4.tgz) 并解压，同时设置好SCALA_HOME和PATH：
<pre>[cc lang='bash' escaped='true']
$ wget http://www.scala-lang.org/files/archive/scala-2.10.4.tgz
$ tar -zxvf scala-2.10.4.tgz
$ sudo mv scala-2.10.4 /usr/local
$ sudo vim /etc/profile #或 vim ~/.bash_profile 设置个人环境变量，下同
# 设置环境变量，将以下行加入到文件末尾
export SCALA_HOME=/usr/local/scala-2.10.4
export PATH=$PATH:$SCALA_HOME/bin
# 保存退出
$ source /etc/profile # 导入刚刚设置的环境变量
$ scala -version # 测试是否安装成功
Scala code runner version 2.10.4 -- Copyright 2002-2013, LAMP/EPFL
[/cc]</pre>

### 2、下载Spark源码并编译

#### 2.1、下载源码

如果Spark官方提供了prebuilt版，那么建议直接下载prebuilt版（[最新的0.9.1-Hadoop 2.2.0的prebuilt版](http://d3kbcqa49mib13.cloudfront.net/spark-0.9.1-bin-hadoop2.tgz)）解压即可立即上手使用，无需编译；

但如果像我这样想试用一下最新的Feature或功能，那么还是得从github下载Spark源码编译（目前是1.0.0-SNAPSHOT版本）：
<pre>[cc lang='bash' escaped='true']
$ cd /usr/local
$ sudo git clone https://github.com/apache/spark.git spark_source
$ sudo vim /etc/profile # 设置spark目录位置，将以下行加入到文件末尾
export SPARK_HOME=/usr/local/spark_source
export PATH=$PATH:$SPARK_HOME/bin 
# 保存退出 
[/cc]</pre>

#### 2.2、配置翻墙代理

由于有一个依赖的twitter4j的库被伟大的G♂F♂W墙了，如果有VPN最好，否则需要先架设和配置一下翻墙代理，建议使用GAE上的[goagent](https://code.google.com/p/goagent/)自行架设一个；如果服务器端已架设，下载客户端的并配置运行（spark-build是我配置用来编译spark的代理，如果无法架设成功可以直接使用这个，不过不要滥用:P）：
<pre>[cc lang='bash' escaped='true']
$ cd local
$ vim proxy.ini
...
[gae]
appid = spark-build #你的APPID 
password = 
...
#保存退出
$ sudo python proxy.py &amp; 
[/cc]</pre>
然后配置代理的环境变量（[@连城](http://weibo.com/lianchengzju) 在知乎[这篇回答](http://www.zhihu.com/question/23245141)提到的SBT_OPTS设置项不一定生效，建议配置为JAVA_OPTS）：
<pre>[cc lang='bash' escaped='true']
$ sudo vim /etc/profile # 设置环境变量，将以下行加入到文件末尾
#export SBT_OPTS="$SBT_OPTS -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=8087"
export JAVA_OPTS="$JAVA_OPTS -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=8087"
# 保存退出
$ source /etc/profile # 导入刚刚设置的环境变量
[/cc]</pre>

#### 2.3、编译源码

代理配置完成之后，根据集群版本编译Spark源码，根据网速不同大约20~30分钟编译完成：
<pre>[cc lang='bash' escaped='true']
$ cd $SPARK_HOME
$ SPARK_HADOOP_VERSION=2.2.0 SPARK_YARN=true sbt/sbt assembly
...
[info] Done packaging.
[success] Total time: 1152 s, completed May 3, 2014 6:21:09 PM
[/cc]</pre>
编译完成后，会在$SPARK_HOME/assembly/target/scala-2.10目录下生成spark-assembly-1.0.0-SNAPSHOT-hadoop2.2.0.jar文件，也就是spark的核心jar文件。

&nbsp;

### 3、本地与Yarn模式测试

#### 3.1、配置spark属性

将spark核心文件地址设置到环境变量中：
<pre>[cc lang='bash' escaped='true']
$ sudo vim /etc/profile # 设置环境变量，将以下行加入到文件末尾
export SPARK_JAR=$SPARK_HOME/assembly/target/scala-2.10/spark-assembly-1.0.0-SNAPSHOT-hadoop2.2.0.jar
# 保存退出
$ source /etc/profile # 导入刚刚设置的环境变量
[/cc]</pre>
同时设置spark运行时的一些属性：
<pre>[cc lang='bash' escaped='true']
$ cd $SPARK_HOME/conf
$ sudo cp spark-env.sh.template spark-env.sh
$ sudo vim spark-env.sh # 文件里有各项的详细解释就不多列举了，如果要On Yarn运行的话下面这项是必选的
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop # HADOOP_HOME为Hadoop安装的目录
[/cc]</pre>

#### 3.2、本地模式测试

<pre>[cc lang='bash' escaped='true']
$ run-example org.apache.spark.examples.SparkPi local # 本地单线程模式
...
14/05/03 23:35:23 INFO SparkContext: Job finished: reduce at SparkPi.scala:39, took 1.223735661 s
Pi is roughly 3.14228
$ run-example org.apache.spark.examples.SparkPi local[4] # 本地多线程模式
...
14/05/03 23:37:01 INFO SparkContext: Job finished: reduce at SparkPi.scala:39, took 1.060589206 s
Pi is roughly 3.14226
[/cc]</pre>

#### 3.3、Yarn模式测试

<pre>[cc lang='bash' escaped='true']
$ run-example org.apache.spark.examples.SparkPi yarn-client # 提交SparkPi Job
...
14/05/03 23:38:37 INFO YarnClientSchedulerBackend: Application report from ASM:
 appMasterRpcPort: 0
 appStartTime: 1399131517104
 yarnAppState: ACCEPTED
...
14/05/03 23:38:47 INFO SparkContext: Job finished: reduce at SparkPi.scala:39, took 4.383655572 s
Pi is roughly 3.1414

$ MASTER=yarn-client spark-shell # spark-shell模式
...
14/05/03 23:40:01 INFO YarnClientSchedulerBackend: Application report from ASM:
 appMasterRpcPort: 0
 appStartTime: 1399131601515
 yarnAppState: ACCEPTED
...
14/05/03 23:40:07 INFO SparkILoop: Created spark context..
Spark context available as sc.

scala&gt; val file = sc.textFile("hdfs://ip:8020/file") // 读取hdfs文件
file: org.apache.spark.rdd.RDD[String] = MappedRDD[3] at textFile at &lt;console&gt;:12
scala&gt; file.count()
...
14/05/03 23:41:01 INFO SparkContext: Job finished: count at &lt;console&gt;:15, took 18.676700057 s
res0: Long = 13347
[/cc]</pre>
至此，Spark 1.0 on Yarn安装完毕

&nbsp;

参考文档：

1、Apache Spark官方网站：[https://spark.incubator.apache.org
](https://spark.incubator.apache.org)

2、Spark最新文档：[http://www.cs.berkeley.edu/~marmbrus/sparkdocs/_site/running-on-yarn.html](http://www.cs.berkeley.edu/~marmbrus/sparkdocs/_site/running-on-yarn.html)

3、Spark文档 in Code：[https://github.com/apache/spark/blob/master/docs/running-on-yarn.md](https://github.com/apache/spark/blob/master/docs/running-on-yarn.md)