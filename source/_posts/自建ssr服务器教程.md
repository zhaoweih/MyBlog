---
title: 自建ssr服务器教程
date: 2017-11-04 00:33:50
tags: [ssr服务器]

---



- **原文地址：[自建ssr服务器教程](https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAss%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)**

**2017年10月31日对教程细节方面进行补充，方便新手。**

------

**自建ss/ssr教程很简单，整个教程分三步**：

第一步：购买VPS服务器

第二步：一键部署VPS服务器

第三步：一键加速VPS服务器 （谷歌BBR加速，推荐）

------

**第一步：购买VPS服务器**

VPS服务器需要选择国外的，首选国际知名的vultr，速度不错、稳定且性价比高。

vultr注册地址： http://www.vultr.com/?ref=7048874 （全球15个服务器位置可选，KVM框架） 

虽然是英文界面，但是现在的浏览器都有网页翻译功能，鼠标点击右键，选择网页翻译即可翻译成中文。

注册并邮件激活账号，充值后即可购买服务器。充值方式是paypal或支付宝(**2017年8月30日Vutrl支持支付宝付款，最低充值10美元即70元左右**），使用paypal有信用卡即可。paypal注册地址：https://www.paypal.com （paypal是国际知名的第三方支付服务商，相当于国内的支付宝。注册一下账号，绑定信用卡即可购买国外商品）

2.5美元/月的服务器配置信息：单核  512M内存  20G SSD硬盘   100M带宽   500G流量/月   

5美元/月的服务器配置信息：单核   1G内存   25G SSD硬盘   100M带宽    1000G流量/月  

10美元/月的服务器配置信息：单核  2G内存   40G SSD硬盘   100M带宽    2000G流量/月  

20美元/月的服务器配置信息：2cpu  4G内存   60G SSD硬盘   100M带宽    3000G流量/月  

40美元/月的服务器配置信息：4cpu  8G内存   100G SSD硬盘   100M带宽   4000G流量/月  

**vultr实际上是折算成小时来计费的，比如服务器是5美元1个月，那么每小时收费为5/30/24=0.0069美元 会自动从账号中扣费，只要保证账号有钱即可。如果你部署的服务器实测后不理想，你可以把它删掉（destroy），重新换个地区的服务器来部署，很方便。温馨提醒：同样的服务器位置，不同的宽带类型和地区所搭建的账号的翻墙速度会不同，所以最好亲测一下。**

**计费从你开通服务器开始算的，不管你有没有使用，即使服务器处于关机状态仍然会计费，如果你没有开通服务器就不算**。比如你今天早上开通了服务器，但你有事情，晚上才部署，那么这段时间是会计费的。同理，如果你早上删掉服务器，第二天才开通新的服务器，那么这段时间是不会计费的。

如图：

![](https://raw.githubusercontent.com/Alvin9999/pac2/master/pp100.png)

![](https://raw.githubusercontent.com/Alvin9999/pac2/master/pp101.png)

购买vps服务器时，服务器地址优先选择：美国硅谷（Silicon Valley）、美国达拉斯(Dallas)等，近期不推荐用洛杉矶和日本的服务器，因为这两个地区近期能够开到的好ip的可能性很低。**推荐选择CentOS 6.X64位的系统（系统版本不要选的太高，不要选centos7！centos7默认的防火墙可能会干扰ssr的正常连接！）**。完成购买后，找到系统的密码记下来，部署服务器时需要用到。如图：

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac教程01.png)

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac教程02.png)

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac教程04.png)

**默认是centos7系统，点击图中的CentOS几个字，会弹出centos6，然后选中它！vps操作系统不要选cento7，因为选它很可能会影响ssr的正常连接。**

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac教程05.png)

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac教程06.png)

------

**第二步：部署VPS服务器**

购买服务器后，需要部署一下。因为你买的是虚拟东西，而且又远在国外，我们需要一个叫Xshell的软件来远程部署。Xshell windows版下载地址：

[国外云盘下载](https://nofile.io/f/eb5dUzYMQK4/Xshell_setup_wm.exe) 提取密码：666

[百度软件中心](http://rj.baidu.com/soft/detail/15201.html?ald)

如果你是苹果电脑操作系统，请自行搜索并下载能远程连接vps服务器的软件的MAC版，关键词可以这样搜索“Mac OS X 平台有哪些好用的 SSH 客户端"

------

部署教程：

下载xshell软件并安装后，打开软件

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell11.png)

选择文件，新建

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell12.png)

随便取个名字，然后把你的服务器ip填上

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell13.png)

连接国外ip即服务器时，软件会先后提醒你输入用户名和密码，用户名linux系统默认都是root，密码是购买服务器后的cent系统的密码。

**如果开好了服务器，发现xshell死活连不上，多半是开的服务器ip被墙了，遇到这种情况，把服务器删掉，重新开个新的服务器即可，可以是同地区的也可以选择其它地区。**

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell14.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell15.png)

连接成功后，会出现如上图所示，之后就可以复制粘贴代码部署了。

**分享两个好用的代码，选择其中一个即可。建议两个脚本先大致都看一下功能,然后再选择。**

【第1个一键部署ssr代码】

yum -y install wget

wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh

chmod +x shadowsocksR.sh

./shadowsocksR.sh 2>&1 | tee shadowsocksR.log

———————————————————代码分割线————————————————

上面的代码总共有4行（显示5行），复制时要一起复制下来，以下脚本类似。如果要卸载直接输入命令：./shadowsocks-go.sh uninstall

**演示开始：复制代码粘贴到vps服务器里，按回车键，进入部署。**

按照如下提示，输入想设置的**密码**，按回车键进入下一步 (**密码建议用字母，图中的密码只是作为演示用**)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/1.png)

按照如下提示，输入想设置的**端口**（3～4位即可），按回车键进入下一步

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/2.png)

按照如下提示，选择想设置的**加密方式**，括号里面是默认的加密方式，想设置默认的话直接按回车键。这里选择数字2（和默认一样）的aes-256-cfb的加密方式

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/3.png)

按照如下提示，选择项设置的**协议插件**，默然的是origin（支持SS客户端，不推荐），我们选择SSR客户端的协议插件：3

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/4.png)

按照如下提示，选择项设置的**混淆插件**，默然的是plain（支持SS客户端，不推荐），我们选择SSR客户端的混淆插件：6

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/5.png)

按照如下提示，按任意键进行自动部署

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/6.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/7.png)

上图表示部署成功。从上往下依次为SSR帐号的IP、端口、密码、协议插件、混淆插件和加密方式。

最后可以重启服务器确保部署生效。重启需要在命令栏里输入reboot ，输入命令后稍微等待一会服务器就会自动重启，一般重启过程需要2～5分钟，重启过程中Xshell会自动断开连接，等VPS重启好后才可以用Xshell软件进行连接。如果部署过程中卡在某个位置超过10分钟，可以用xshell软件断开，然后重新连接你的ip，再复制代码进行部署。

这个脚本的图文演示就结束了，图中的IP仅作演示用，教程发布后会失效。有人想了，我以后有想修改密码或者端口的需求怎么办？这个脚本修改密码和端口不是很方便，需要把最初的部署代码重新输入一遍，即从头到尾部署一遍即可。

**下面再分享第二个脚本，这个脚本装一遍即可，方便以后想修改密码、端口什么的，而且功能更多。**

【第2个一键部署ssr代码】

CentOS/Debian/Ubuntu ShadowsocksR单/多端口一键管理脚本：

yum -y install wget

wget -N --no-check-certificate https://softs.fun/Bash/ssr.sh && chmod +x ssr.sh && bash ssr.sh

备用下载地址：

yum -y install wget

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh

———————————————————代码分割线————————————————

复制上面的代码到VPS服务器里，安装脚本后，以后只需要运行这个快捷命令就可以出现下图的界面进行设置，快捷管理命令为：bash ssr.sh

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/8.png)

如上图出现管理界面后，**输入数字1来安装SSR服务端**。如果输入1后不能进入下一步，那么请退出xshell，重新连接vps服务器，然后输入快捷管理命令bash ssr.sh 再尝试。

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/9.png)

根据上图提示，依次输入自己想设置的**端口和密码** (**密码建议用字母，图中的密码只是作为演示用**)，回车键用于确认

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/10.png)

如上图，选择想设置的**加密方式**，比如10，按回车键确认

接下来是选择**协议插件**，如下图：

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/11.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/12.png)

选择并确认后，会出现上图的界面，提示你是否选择兼容原版，这里的原版指的是SS客户端，可以根据需求进行选择，原则上不推荐使用SS客户端，演示选择n

之后进行混淆插件的设置，如下面

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/13.png)

进行混淆插件的设置后，会依次提示你对设备数、单线程限速和端口总限速进行设置，默认值是不进行限制，个人使用的话，选择默认即可，即直接敲回车键。

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/14.png)

之后代码就正式自动部署了，到下图所示的位置，提示你下载文件，输入：y

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/15.png)

耐心等待一会，出现下面的界面即部署完成：

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/16.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/17.png)

根据上图就可以看到自己设置的SSR账号信息，包括IP、端口、密码、加密方式、协议插件、混淆插件。如果之后想修改账号信息，直接输入快捷管理命令：bash ssr.sh 进入管理界面，选择相应的数字来进行一键修改。例如：

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/22.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/23.png)

**第2个脚本的演示结束。**

------

**第三步：一键加速VPS服务器**

此加速教程为谷歌BBR加速,Vultr的服务器框架可以装BBR加速，加速后对速度的提升很明显，所以推荐部署加速脚本。该加速方法是开机自动启动，部署一次就可以了。

按照第二步的步骤，连接服务器ip，登录成功后，在命令栏里粘贴以下代码：

【谷歌BBR加速教程】

yum -y install wget

wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

chmod +x bbr.sh

./bbr.sh

把上面整个代码复制后粘贴进去，不动的时候按回车，然后耐心等待，最后重启vps服务器即可。

演示开始，如图：

复制并粘贴代码后，按回车键确认

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/18.png)

如下图提示，按任意键继续部署

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/19.png)

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/20.png)

部署到上图这个位置的时候，等待3～6分钟

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/21.png)

最后输入y重启服务器或者手动输入代码reboot来确保加速生效。

------

【SSR客户端下载】

Windows SSR客户端 [下载地址](https://github.com/shadowsocksr-backup/shadowsocksr-csharp/releases) [备用下载地址](https://nofile.io/f/6Jm7WJCyOVv/ShadowsocksR-4.7.0-win.7z)

MAC SSR客户端 [下载地址](https://github.com/shadowsocksr-backup/ShadowsocksX-NG/releases) [备用下载地址](https://nofile.io/f/jgMWFwCBonU#ab0d3c3b6ac54482)

[Linux客户端一键安装配置使用脚本(使用方法见注释)](https://github.com/the0demiurge/CharlesScripts/blob/master/charles/bin/ssr) 或者采用图形界面的[linux ssr客户端](https://github.com/erguotou520/electron-ssr/releases)

安卓 SSR客户端 [下载地址](https://github.com/shadowsocksr-backup/shadowsocksr-android/releases) [备用下载地址](https://nofile.io/f/GRWw7PbADrc#1c6c32f969e7f5d9) 

苹果手机SSR客户端：Potatso Lite、Potatso、shadowrocket都可以作为SSR客户端，但这些软件目前已经在国内的app商店下架，请用美区的appid账号来下载，网络上有申请国外appid的教程或者淘宝购买。

**有了账号后，打开SSR客户端，填上信息，这里以windows版的SSR客户端为例子**：

![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/25.png)

在对应的位置，填上服务器ip、服务器端口、密码、加密方式、协议和混淆，最后将浏览器的代理设置为（http）127.0.0.1和1080即可。账号的端口号就是你自己设置的，而要上网的浏览器的端口号是1080，固定的，谷歌浏览器可以通过 SwitchyOmega 插件来设置。

启动SSR客户端后，右键SSR客户端图标，选择第一个“系统代理模式”，里面有3个子选项，选择"全局模式“，之后就可以用浏览器设置好了的代理模式（http）127.0.0.1和1080翻墙，此模式下所有的网站都会走SSR代理。（适合新手）

如果想国外网站走SSR代理，国内网站不走SSR代理，那么SSR客户端可以设置为”PAC模式“，但是此时浏览器要设置为系统代理才行。

![ssr9000](https://user-images.githubusercontent.com/12132898/32225069-cfe6195a-be7e-11e7-99e0-e2fa98f93b1f.png)

------

**常见问题参考解决方法**：

1、用了一段时间发现ssr账号用不了了？

多半是被墙了，即ip失效。首先ping一下自己的ip，看看能不能ping的通，ping不通那么就是ip被墙了，遇到这种情况重新部署一个新的服务器，新的服务器就是新的ip。关于怎么ping ip的方法，可以自行网上搜索，很简单。vultr服务商是折算成小时计费，且开通和删除服务器非常方便（新服务器即新ip。大多数vps服务商都没有这样的服务，一般的vps服务商可能会提供更换1次ip的服务，如果你买的是别家的vps，一定要了解是否能够更换ip，假如不能，那么万一你的ip不幸被墙，钱就打水漂了）。

2、刚搭建好的ssr账号，ip能ping通，但是还是用不了？

首选，排除杀毒软件的干扰，尤其是国产杀毒软件，包括但不限于360安全卫生、360杀毒软件、腾讯管家、金山卫生等。这些东西很容易干扰翻墙上网，如果你的电脑安装了这样的东西，建议至少翻墙时别用。其次，检查下SSR信息是否填写正确。浏览器的代理方式是否是ssr代理，即127.0.0.1 1080端口。如果以上条件都排除，还是用不了，那么可以更换端口、加密方式、协议、混淆，或者更换服务器位置。

3、vps的服务器操作系统不要用的太高，太高可能会因为系统的防火墙问题导致搭建的SSR账号连不上，如果你用的centos系统，建议用centos6，不要用centos7。如果你前面不小心装了centos7系统，那么只能重装系统或者重新部署新的vps服务器。

4、小知识：vultr服务商提供的vps服务器是单向流量计算，有的vps服务商是双向流量计算，单向流量计算对于用户来说更实惠。因为我们是在vps服务器上部署SSR服务端后，再用SSR客户端翻墙，所以SSR服务端就相当于中转，比如我们看一个视频，必然会产生流量，假如消耗流量80M，那么VPS服务器会产生上传80M和下载80M流量，vultr服务商只计算单向的80M流量。如果是双向计算流量，那么会计算为160M流量。

5、如果你想把搭建的账号给多人使用，不用额外设置端口，因为一个账号就可以多人使用。一般10美元的服务器可以同时支持100人在线使用。

> 鸣谢参考教程：[秋水逸冰](https://teddysun.com/392.html)  [91yun](https://www.91yun.co/archives/5174)  [doub.bid](https://doub.bid/ss-jc42/)

------

