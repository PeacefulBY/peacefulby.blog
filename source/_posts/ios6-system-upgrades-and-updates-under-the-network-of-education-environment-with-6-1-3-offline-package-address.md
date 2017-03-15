---
title: 教育网环境下iOS6系统的离线升级与更新（附6.1.3离线包地址）
tags:
  - iOS
  - iTunes
  - 教育网
id: 19
categories:
  - 未分类
date: 2013-04-05 19:03:31
---

最近想把刚买的Touch升级到刚发布的iOS6.1.3，期间遇到各种诸如教育网无法访问iTunes、C盘空间不足这样令人蛋碎的问题；尤其是要用教育网到公网的这条小水管穿越到大洋彼岸，下载一坨大到800MB的更新包，顿时觉得压力很大。好在iTunes提供了一种比较隐蔽的离线升级方式，可以先用P2P下载工具将苹果官方提供的更新包下载到本地，然后进行系统升级并联网验证。

以下记录一些期间遇到的问题和自己的解决方案： 

&nbsp;

<span style="font-size: large;">**1、教育网环境下iTunes访问**</span>

由于iTunes和apple大部分服务器地址都不在教育网免费地址以内，因此需要使用代理访问；iTunes在网络连接时使用的是IE代理，以下两个站点可以提供比较常用的教育网访问公网的代理及设置教程：

清华IPCN：[http://proxy.ipcn.org/](http://proxy.ipcn.org/ "清华IPCN")

代理服务器网：[http://www.cnproxy.com/proxyedu1.html](http://www.cnproxy.com/proxyedu1.html "代理服务器网")

上面提供的代理地址是临时地址，如果需要稳定的代理则推荐使用搜狗浏览器的某些过期版本的教育网加速代理功能，撸主使用的是2.2.0.2070版本，前后几个版本均可使用，开启搜狗的全网加速功能后将IE代理服务器地址设为“127.0.0.1”，端口设为“8081”（8080~8089好像都可以），可以支持https,http访问。

需要注意的是搜狗浏览器为了防止用户将该功能抽取出来的同时弃用搜狗浏览器，在新版本中教育网加速代理端口号是每次启动浏览器后随机绑定一个端口号，因此**使用时不建议升级搜狗浏览器**。

&nbsp;

<span style="font-size: large;">2、**确保C盘有足够的剩余空间**</span>

iTunes默认的下载并更新的过程是这样的：将更新包下载到C盘 —&gt; 将压缩包解压到C盘某临时目录 —&gt; 备份与升级系统 —&gt; 连接到官方服务器验证 —&gt; 删除之前下载的更新包

注：Windows XP环境下，iPhone/iPod默认的下载路径为C:\Documents and Settings\[用户名]\Application Data\Apple Computer\iTunes\iPod Software Updates，如果是更新iPad即为iPad Software Updates文件夹

需要注意的是，不管是下载途中因为C盘满提示空间不足，还是验证这一步因为连不上服务器出错，**无论升级成功还是失败，iTunes都会删除C盘中下载的更新包，没有断点续传功能**。 坑爹呢这是！不就是碰了下网线么？！劳资足足下一个小时，裤子都脱了就让我看这个？！

解决方案的话，除了 [更改iTunes备份路径释放C盘空间](http://www.google.com.hk/webhp?hl=zh-CN&amp;sourceid=cnhp#hl=zh-CN&amp;newwindow=1&amp;safe=strict&amp;site=webhp&amp;q=%E6%9B%B4%E6%94%B9iTunes%E5%A4%87%E4%BB%BD%E8%B7%AF%E5%BE%84%E9%87%8A%E6%94%BEC%E7%9B%98%E7%A9%BA%E9%97%B4&amp;oq=%E6%9B%B4%E6%94%B9iTunes%E5%A4%87%E4%BB%BD%E8%B7%AF%E5%BE%84%E9%87%8A%E6%94%BEC%E7%9B%98%E7%A9%BA%E9%97%B4&amp;gs_l=serp.3...208528.208528.0.208759.1.1.0.0.0.0.0.0..0.0...0.0...1c.1.5.serp.5Je_O3Mr-6g&amp;bav=on.2,or.r_gc.r_pw.&amp;bvm=bv.43148975,d.aGc&amp;fp=b16a1ddf6dc455fc&amp;biw=1280&amp;bih=642) 之外，也可以考虑使用下面的分区助手将其他盘符的空间搬到C盘来

官方下载地址：[http://www.disktool.cn/download.html](http://www.disktool.cn/download.html)

官方教程：[http://www.disktool.cn/jiaocheng/extend-c-drive.html](http://www.disktool.cn/jiaocheng/extend-c-drive.html)

[caption id="" align="aligncenter" width="444"][![](http://www.disktool.cn/jiaocheng/images/extend-c-drive/extend.gif "C盘分区助手")](http://www.disktool.cn/jiaocheng/extend-c-drive.html) C盘分区助手[/caption]

<span style="font-size: large;">**3、下载离线包并更新**</span>

下方是6.1.3的离线升级包官方下载链接，推荐用迅雷等P2P方式下载，开通会员风味更佳；

下载离线包后，在Windows系统下“**按住Shift+更新按钮**”，在Mac系统下“**Option+更新按钮**”，选择刚刚的离线包升级即可。

&nbsp;

iPhone 5 GSM+CDMA：

[http://appldnld.apple.com/iOS6.1/091-2516.20130319.7164R/iPhone5,2_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2516.20130319.7164R/iPhone5,2_6.1.3_10B329_Restore.ipsw)

iPhone 5 GSM：

[http://appldnld.apple.com/iOS6.1/091-2341.20130319.C24tg/iPhone5,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2341.20130319.C24tg/iPhone5,1_6.1.3_10B329_Restore.ipsw)

iPhone 4S：

[http://appldnld.apple.com/iOS6.1/091-2611.20130319.Fr54r/iPhone4,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2611.20130319.Fr54r/iPhone4,1_6.1.3_10B329_Restore.ipsw)

iPhone 4 (GSM)：

[http://appldnld.apple.com/iOS6.1/091-2610.20130319.Bedr4/iPhone3,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2610.20130319.Bedr4/iPhone3,1_6.1.3_10B329_Restore.ipsw)

iPhone 4(iPhone3,2)：

[http://appldnld.apple.com/iOS6.1/091-2444.20130319.exFqm/iPhone3,2_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2444.20130319.exFqm/iPhone3,2_6.1.3_10B329_Restore.ipsw)

iPhone 4 (CDMA)：

[http://appldnld.apple.com/iOS6.1/091-2351.20130319.Fe431/iPhone3,3_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2351.20130319.Fe431/iPhone3,3_6.1.3_10B329_Restore.ipsw)

iPhone 3GS：

[http://appldnld.apple.com/iOS6.1/091-2371.20130319.715gt/iPhone2,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2371.20130319.715gt/iPhone2,1_6.1.3_10B329_Restore.ipsw)

iPad mini WiFi：

[http://appldnld.apple.com/iOS6.1/091-2417.20130319.Nh23w/iPad2,5_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2417.20130319.Nh23w/iPad2,5_6.1.3_10B329_Restore.ipsw)

iPad mini (GSM)：

[http://appldnld.apple.com/iOS6.1/091-2461.20130319.Hgt54/iPad2,6_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2461.20130319.Hgt54/iPad2,6_6.1.3_10B329_Restore.ipsw)

iPad mini (CDMA)：

[http://appldnld.apple.com/iOS6.1/091-2356.20130319.54rGB/iPad2,7_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2356.20130319.54rGB/iPad2,7_6.1.3_10B329_Restore.ipsw)

iPad 4代WiFi：

[http://appldnld.apple.com/iOS6.1/091-2407.20130319.vs6yt/iPad3,4_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2407.20130319.vs6yt/iPad3,4_6.1.3_10B329_Restore.ipsw)

iPad 4代 (GSM)：

[http://appldnld.apple.com/iOS6.1/091-2560.20130319.ySu43/iPad3,5_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2560.20130319.ySu43/iPad3,5_6.1.3_10B329_Restore.ipsw)

iPad 4代 (CDMA)：

[http://appldnld.apple.com/iOS6.1/091-2347.20130319.Aqwe3/iPad3,6_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2347.20130319.Aqwe3/iPad3,6_6.1.3_10B329_Restore.ipsw)

iPad 3代WiFi：

[http://appldnld.apple.com/iOS6.1/091-2576.20130319.JeX43/iPad3,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2576.20130319.JeX43/iPad3,1_6.1.3_10B329_Restore.ipsw)

iPad 3代GSM：

[http://appldnld.apple.com/iOS6.1/091-2432.20130319.Be867/iPad3,2_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2432.20130319.Be867/iPad3,2_6.1.3_10B329_Restore.ipsw)

iPad 3代CDMA：

[http://appldnld.apple.com/iOS6.1/091-2592.20130319.64uy6/iPad3,3_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2592.20130319.64uy6/iPad3,3_6.1.3_10B329_Restore.ipsw)

iPad 2 WiFi：

[http://appldnld.apple.com/iOS6.1/091-2397.20130319.EEae9/iPad2,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2397.20130319.EEae9/iPad2,1_6.1.3_10B329_Restore.ipsw)

iPad 2 GSM：

[http://appldnld.apple.com/iOS6.1/091-2472.20130319.Ta4rt/iPad2,2_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2472.20130319.Ta4rt/iPad2,2_6.1.3_10B329_Restore.ipsw)

iPad 2 CDMA：

[http://appldnld.apple.com/iOS6.1/091-2464.20130319.KF6yt/iPad2,3_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2464.20130319.KF6yt/iPad2,3_6.1.3_10B329_Restore.ipsw)

iPad 2,4（32nm版本）：

[http://appldnld.apple.com/iOS6.1/091-2633.20130319.Xd54r/iPad2,4_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2633.20130319.Xd54r/iPad2,4_6.1.3_10B329_Restore.ipsw)

iPod touch第四代：

[http://appldnld.apple.com/iOS6.1/091-2655.20130319.Wyt54/iPod4,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2655.20130319.Wyt54/iPod4,1_6.1.3_10B329_Restore.ipsw)

iPod touch第五代：

[http://appldnld.apple.com/iOS6.1/091-2520.20130319.5gty7/iPod5,1_6.1.3_10B329_Restore.ipsw](http://appldnld.apple.com/iOS6.1/091-2520.20130319.5gty7/iPod5,1_6.1.3_10B329_Restore.ipsw)

&nbsp;

参考文献：

 1\. 雪花, 《苹果正式发布iOS 6.1.3！》, [http://news.mydrivers.com/1/257/257893.htm](http://news.mydrivers.com/1/257/257893.htm), 2013-03-20