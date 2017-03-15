---
title: Python第三方库-网络包-requests
tags:
  - http
  - json
  - python
  - requests
  - urllib
  - urllib2
id: 82
categories:
  - Python
date: 2014-03-04 14:39:40
---

正如 python 第三方库-requests 库[官方主页](http://docs.python-requests.org/en/latest/index.html "requests")标题所说：It's HTTP for Humans! 言下之意是说其他HTTP库都不是给Humans用的…… 尽管 python 下的 urllib 和 urllib2 比起 Java 的 HttpURLConnection 已经足够简单易用，相比之下 requests 库依然人性化到逆天。 以访问百度首页为例，urllib2 方式访问：
<pre>[cc lang='python' escaped='true']
&gt;&gt;&gt; import urllib2
&gt;&gt;&gt; r = urllib2.Request('http://www.baidu.com') 
&gt;&gt;&gt; response = urllib2.urlopen(r)
&gt;&gt;&gt; print response.read()
&lt;!DOCTYPE html&gt;&lt;!--STATUS OK--&gt;&lt;html&gt;&lt;head...
[/cc]</pre>
而requests只需要：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; import requests
&gt;&gt;&gt; r = requests.get('http://www.baidu.com')
&gt;&gt;&gt; print r.text
&lt;!DOCTYPE html&gt;&lt;!--STATUS OK--&gt;&lt;html&gt;&lt;head...
[/cc]</pre>
requests有官方[中文文档](http://cn.python-requests.org/en/latest/ "requests中文文档")（目前更新到1.1.0版）和[英文文档](http://docs.python-requests.org/en/latest/ "requests文档")（更新到最新版），大部分特性和示例都可以在文档中找到。以下记录一些requests的安装、基本应用和常用特性，其他的想到或用到再往上补充吧

### 1、安装

Windows环境下在 [这里](https://github.com/kennethreitz/requests/tarball/master "requests安装包") 下载安装包并解压后，执行 **python setup.py install** 安装 Linux环境下直接执行 **easy_install requests** 或 **pip install requests** 即可

### 2、基本应用-访问

requests支持所有访问http访问方式，常用的Get和Post方式使用方式如下： Get方式下，参数的提交可以采用直接拼接URL的方式，也可以采用params参数传递：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; r = requests.get('http://www.baidu.com/s?wd=测试')
&gt;&gt;&gt; r = requests.get('http://www.baidu.com/s?',params={'wd':'测试'})
[/cc]</pre>
Post方式下，提交参数的方式和上面第二种方式类似：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; r = requests.post('http://www.baidu.com/s?',data={'wd':'测试'})
[/cc]</pre>

### 3、基本应用-返回

我们可以通过r.text直接获取返回的html网页，或者通过r.content获取网页的字节内容：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; r = requests.get('http://www.baidu.com')
&gt;&gt;&gt; r.text
u'&lt;!DOCTYPE html&gt;&lt;!--STATUS OK--&gt;&lt;html&gt;&lt;head...'
&gt;&gt;&gt; r.content
b'&lt;!DOCTYPE html&gt;&lt;!--STATUS OK--&gt;&lt;html&gt;&lt;head...' 
[/cc]</pre>
值得一提的一点是，requests包本身还自带了json解析方法，在现在大量API支持json格式数据的时代，无疑是快速开发一个第三方应用的利器：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; r = requests.get('https://github.com/timeline.json')
&gt;&gt;&gt; r.json()
[{u'repository': {u'open_issues': 0, u'url': 'https://github.com/...
[/cc]</pre>
除此以外，我们还可以获取其他返回的相关信息：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; r = requests.get('http://www.baidu.com')
&gt;&gt;&gt; r.status_code  #状态码
200
&gt;&gt;&gt; r.headers['content-type']  #响应头
'text/html'
&gt;&gt;&gt; r.encoding  #网页编码
'ISO-8859-1'
&gt;&gt;&gt; r.url
u'http://www.baidu.com/'
[/cc]</pre>

### 4、Basic Auth

在一些大型平台提供的第三方API中，不少API提供了Basic Auth方式登录获取信息，以便开发者进行快速开发与调试，例如[新浪微博API](http://open.weibo.com/wiki/2/statuses/home_timeline)；以下一段代码展示了如何获取用户所关注的用户的最新微博：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; url = 'https://api.weibo.com/2/statuses/home_timeline.json?source=XXXXXXXXXX'  #source为AppKey
&gt;&gt;&gt; username = 'user@example.com'  #新浪微博用户名
&gt;&gt;&gt; password = 'password'  #密码
&gt;&gt;&gt; r = requests.get(url,auth=(username, password))
&gt;&gt;&gt; r.json()
{u'total_number': 1111, u'previous_cursor': 0, u'hasvisible': False ...
[/cc]</pre>

### 5、代理

如果是编写爬虫或一些其他网络抓取脚本，有时需要采用代理避免被封IP，在requests中可以直接使用proxies属性配置
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; proxies = {"http": "http://0.0.0.0:80/"}
&gt;&gt;&gt; requests.get("http://www.baidu.com", proxies=proxies)
[/cc]</pre>
如果代理需要用户名和密码验证，可以用HTTP Basic Auth方式配置如下：
<pre>[cc lang='python' escaped="true"]
&gt;&gt;&gt; proxies = {"http": "http://user:pass@0.0.0.0:80/"} 
[/cc]</pre>