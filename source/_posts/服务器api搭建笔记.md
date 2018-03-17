---
title: 服务器api搭建笔记
date: 2018-03-17 01:38:05
tags: [api,笔记]
categories: 笔记
---
### yum安装jdk：
在linux上使用yum安装是非常粗暴无脑的，但仍然有需要注意的点，不然会掉坑里。这里说一下步骤。

1.执行命令yum -y list java*查看可安装java版本。执行成功后可以看见如下的结果
Paste_Image.png

2.选择一个java版本进行安装，这里我们希望安装java1.8，因为我们的机器是64位的，所以选择安装java-1.8.0-openjdk-devel.x86_64。
这里有个地方要注意，上图中我用红框圈起来的两个java版本，要选择-devel的安装，因为这个安装的是jdk，而那个不带-devel的安装完了其实是jre。

3.执行命令yum install -y java-1.8.0-openjdk-devel.x86_64。执行完后会看见控制台刷出很多输出。
耐心等待至自动安装完成

4.输入java --version查看已安装的jdk版本，当出现如下输出表示安装成功。

5.你可能好奇，yum安装的jdk，被安装到哪里去了？你可以在/usr/lib/jvm目录下找到他们。
至此，yum安装jdk完成。

### yum安装mysql：

1.新开的云服务器，需要检测系统是否自带安装mysql

`# yum list installed | grep mysql`

2.如果发现有系统自带mysql，果断这么干

`# yum -y remove mysql-libs.x86_64`

3.随便在你存放文件的目录下执行，这里解释一下，由于这个mysql的yum源服务器在国外，所以下载速度会比较慢，还好mysql5.6只有79M大，而mysql5.7就有182M了，所以这是我不想安装mysql5.7的原因

`# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm`

4.接着执行这句,解释一下，这个rpm还不是mysql的安装文件，只是两个yum源文件，执行后，在/etc/yum.repos.d/ 这个目录下多出mysql-community-source.repo和mysql-community.repo

`# rpm -ivh mysql-community-release-el6-5.noarch.rpm`

5.这个时候，可以用yum repolist mysql这个命令查看一下是否已经有mysql可安装文件

`#yum repolist all | grep mysql`

6.安装mysql 服务器命令（一路yes）：

`# yum install mysql-community-server`

7.安装成功后

`# service mysqld start`

8.由于mysql刚刚安装完的时候，mysql的root用户的密码默认是空的，所以我们需要及时用mysql的root用户登录（第一次回车键，不用输入密码），并修改密码

`# mysql -u root`

`# use mysql;`

`# update user set password=PASSWORD("这里输入root用户密码") where User='root';`
 
9.授权（自动创建）一个mysql的非root的aaa用户，能访问localhost上的testdb数据库，密码是xxxx，最后刷新权限

`# grant all privileges on testdb.* to aaa@localhost identified by 'xxxx';`

`# flush privileges;`

10.创建一个utf8的表(如果你有需要的话)之后退出

`# CREATE DATABASE `database` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci; `

`# exit;`

11.查看mysql是否自启动,并且设置开启自启动命令

`# chkconfig --list | grep mysqld`

`# chkconfig mysqld on`

12.mysql安全设置(系统会一路问你几个问题，看不懂复制之后翻译，基本上一路yes)：

`# mysql_secure_installation`

13.晚安

`# exit`


### MySQL修改root密码的多种方法
方法1： 用SET PASSWORD命令

`mysql -u root`

`mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');`

### Linux-SSH传输文件
在linux下一般用scp这个命令来通过ssh传输文件。

从服务器上下载文件
把192.168.0.101上的/var/www/test.txt 的文件下载到/var/www/local_dir（本地目录）

`scp root@192.168.0.101:/var/www/test.txt /var/www/local_dir `

上传本地文件到服务器

`把本机/var/www/目录下的test.php文件上传到192.168.0.101这台服务器上的/var/www
scp /var/www/test.php  root@192.168.0.101:/var/www/`

从服务器下载整个目录

`scp -r root@192.168.0.101:/var/www/test  /var/www/ `

上传目录到服务器

`scp  -r local_dir username@servername:remote_dir`

注：** 目标服务器要开启写入权限。**

### 运行jar文件:

`java -jar upload.jar`

### linux下利用nohup后台运行jar文件包程序：

`nohup java -jar XXX.jar & ` 

nohup 意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行

当用 nohup 命令执行作业时，缺省情况下该作业的所有输出被重定向到nohup.out的文件中，除非另外指定了输出文件。

原文地址：
https://www.jianshu.com/p/10949f44ce9c
https://www.jianshu.com/p/b70089f4c187
https://segmentfault.com/a/1190000007667534
https://www.jianshu.com/p/8fed013cc592
http://blog.csdn.net/tang9140/article/details/38899345