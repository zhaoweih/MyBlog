---
title: 'Android:手机刷第三方ROM教程，旧手机重生之术'
date: 2017-05-05 10:00:00
tags: [Android,刷机,第三方ROM]
categories: 刷机
---
`与我联系`
```
-  Email:zhaoweihaochn@gmail.com
-  Blog:zhaoweihao.me
```
# 前言

我是一个大二学生，我有一台米4陪伴了我快两年了，我是从MIUI6到MIUI8过来的，看着MIUI一直的越来越差，广告越来越多，而且后台占用很多，空间也被自带软件占用了好多，可是自带软件又不能卸载，所以我就下定决心拯救一下我这台垂危的米4，经过昨天一下午的折腾把手机刷了lineageOS系统，Android7.1.2，然后想着把自己刷机的经验总结一下，因为我看网上一个完整的教程比较少，我都是零零散散地搜索和收集的
`注：如果大家对我的文章有误解请Email我修改`

## 更新(2017/08/31)
由于发现之前的版本有误导的地方，所以修改一下

## 方法

我这个文章主要介绍刷入第三方rec刷机的，如果需要一键刷机的可以移步到刷机精灵，虽然刷机精灵可以一键刷机，但是刷完后的系统有好多刷机精灵安装的APP，还不能删除，我是接受不了的，当然，如果你可以接受也是可以的
# 关于LineageOS

我在网上搜索第三方ROM时很多人推荐LineageOS，我一开始不知道这个是什么东西，经过搜索才知道是前CM团队成员开发的，之前一直久仰CM团队大名，于是我就毅然决然地动手了，但是LineageOS的官网要翻墙，所以我特地为大家整理了下载地址，留在下方
## 附上LineageOS的截图

![](http://op4e089f0.bkt.clouddn.com/Screenshot_20170505-101314.jpg)

![](http://op4e089f0.bkt.clouddn.com/Screenshot_20170505-101211.jpg)

![](http://op4e089f0.bkt.clouddn.com/Screenshot_20170505-101322.jpg)

![](http://op4e089f0.bkt.clouddn.com/Screenshot_20170505-101345.jpg)

## 安装后

安装后的系统十分纯净，自带的软件不超过17个，都是必要的应用，例如音乐，时钟，日历，浏览器，计算器之类的，而且lineageOS的自带应用都是根据Material design设计的，非常美观

# 需要下载的东西

TWRP recovery:http://pan.baidu.com/s/1hrPlhsw
LineageOS下载地址`需要翻墙`:https://download.lineageos.org/
我整理的LineageOS下载地址`不用翻墙`:[LineageOS下载地址-个人整理](http://zhaoweihao.me/2017/05/05/LineageOS%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80-%E4%B8%AA%E4%BA%BA%E6%95%B4%E7%90%86/)
找到适配自己机器的ROM，复制下载地址到迅雷即可下载
`注：如果百度云地址失效，请Email我更新`

# 请事先备份好要备份的数据

# 开始

## 下载TWRP
上文下载好的TWRP recovery解压好放着
进入下载地址：https://twrp.me/Devices/
找到自己机型的版本，在介绍页面找到Download Links，选择Primary(Americas)

![01.png](http://op4e089f0.bkt.clouddn.com/2017083101.png)
选择最新版本img文件下载

![02.png](http://op4e089f0.bkt.clouddn.com/2017083102.png)

将下载的img文件改名为recovery.img并放入上面解压好的TWRP recovery文件夹里,替换掉原来的recovery.img

![03.png](http://op4e089f0.bkt.clouddn.com/2017083103.png)

## 刷入第三方recovery

刷入第三方rec的方法很简单，首先手机关机，按住电源键+音量下键打开fastboot模式，将手机连接到电脑,在TWRP解压后的目录下按shift+右键

![](http://op4e089f0.bkt.clouddn.com/1.jpg)

选择在此处打开命令窗口，输入下面命令    

    fastboot flash recovery recovery.img

![](http://op4e089f0.bkt.clouddn.com/2.png)

过一会CMD会有finished提示就证明成功了
长按开机键等待手机重启即可
如果长按开机键后直接进入系统，可以关机后按住电源键+音量上键即可进入rec

- 问题
  如果出现waiting devices，请检查驱动
  如果不能刷入，请自行寻找适合自己机型的第三方rec，替换掉TWRP目录下的recovery.img再执行一次命令就可以了

## 刷入第三方ROM

`注：rec界面为英文`

- 第一次进入REC可能会问是否允许修改，选择允许修改（右滑）

下面进入最紧张最关键的步骤了，刷入lineageOS系统。首先上一步进入rec后连接电脑，将下载好的lineageOS的zip安装包放入手机download目录（放进你能找到的目录就可以了，注意不要放入系统目录，建议新建文件夹存放），然后rec里面点击Wipe，右滑确定双清，清理好后返回rec主界面，选择Install，然后在目录里寻找到你存放的zip安装包，右滑确定安装，然后等待安装完成重启就可以了（安装完rec会提示是否安装root，请根据需要自行选择）

# 最后

按照上面的步骤安装完成后重启会进入系统设置画面，设置好后就可以看到崭新的界面了，系统用起来非常流畅。

## 关于lineageos更新
- OTA升级
  官方升级和普通手机系统一样 在**设置-关于手机-LineageOS更新**（需翻墙），下载好后会重启更新
  **问题：**
  有部分人会出现重启后在recovery不启动更新也不进入系统，这是由于TWRP版本太旧的缘故，将TWRP版本更新到3.0.3以上最新版本即可启动更新
  [原文地址](https://www.reddit.com/r/LineageOS/comments/5riech/how_fix_twrp_recovery_boot_loop_after_lineageos/)

![04.png](http://op4e089f0.bkt.clouddn.com/2017083104.png)

- 卡刷升级
  在https://download.lineageos.org/ 下载最新适合自己机型的lineageos，和上面刷ROM的步骤一样，除了不用双清（lineageos升级lineageos不用双清，如果要刷第三方系统ROM需要双清）

## 优化

其实Android系统在外国的流畅度可以堪比ios的，如果问国内为什么运行如此的慢，追踪他的原因就是各位毒瘤应用，具体是哪个应用就不点名了，Android开发界都了解的，具体可以看这个文章：[安卓 & 卡顿 & APP](http://mp.weixin.qq.com/s?__biz=MzA4NTQwNDcyMA==&mid=2650662746&idx=1&sn=524e035c866762ae60bc65bafea98283&chksm=87d13a05b0a6b313cb740aabe29224b79ed5328148d1fb780d622cf49daee0526f6e380b966d&mpshare=1&scene=23&srcid=05057zswWCKtb9BiKdT2111v#rd)，好了言归正传，既然毒瘤应用我们不得不用，那就得进行优化了。

- 优化用到的应用：[绿色守护](http://www.wandoujia.com/apps/com.oasisfeng.greenify)

绿色守护可以在没有root的情况下监测加入列表的应用，并让它们休眠，如果root之后功能更为强大，我们要做的就是将平常不需要在后台保持的应用加入到列表，并让它们都休眠，可达到省电而且系统还流畅的目的

## 推荐

- 第三方应用市场：[豌豆荚](https://www.wandoujia.com/)
  刷了系统后系统内没有自带的应用市场，我们需要下载第三方应用市场，在对比了各个第三方应用市场后我选择了豌豆荚，因为它广告比较少，界面比较美观

## 捐赠

这篇博客我是总结自己刷机经验的，如果对大家有帮助，大家可以请我这个大学穷学生吃点零食，不要求多，1块五毛也行，你的支持是我最大的鼓励！谢谢！

微信支付码：

![](http://op4e089f0.bkt.clouddn.com/wechatcode.jpg)



