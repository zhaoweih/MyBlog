---
title: Git SSH Key 生成步骤
date: 2017-07-11 20:59:51
tags: [Git]
categories: 笔记
---
# 一 、设置Git的user name和email：

    $ git config --global user.name "ZhaoWeihao"
    $ git config --global user.email "zhaoweihaochn@foxmail.com"

# 二、生成SSH密钥过程：
## 1.查看是否已经有了ssh密钥：

    cd ~/.ssh

如果没有密钥则不会有此文件夹，有则备份删除
## 2.生存密钥：

    $ ssh-keygen -t rsa -C “zhaoweihaochn@foxmail.com”

按3个回车，密码为空。

Your identification has been saved in /home/tekkub/.ssh/id_rsa.
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.
The key fingerprint is:
………………

最后得到了两个文件：id_rsa和id_rsa.pub

## 3.添加密钥到ssh：

    ssh-add 文件名

需要之前输入密码。
## 4.在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。
打开https://github.com/ ，进入设置，然后添加ssh。

## 5.测试：

    ssh git@github.com

The authenticity of host ‘github.com (207.97.227.239)’ can’t be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added ‘github.com,207.97.227.239′ (RSA) to the list of known hosts.
ERROR: Hi tekkub! You’ve successfully authenticated, but GitHub does not provide shell access
Connection to github.com closed.