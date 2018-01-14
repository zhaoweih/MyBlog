---
title: 'GenyMotion镜像下载慢解决方法(Get download links of GenyMotion virtual devices)'
date: 2018-01-14 15:36:32
tags: [Android,GenyMotion]
categories: 开发
---
#### 格式 Format
**中文**
 English
#### 正文 Body
**1.打开Genymotion点击'Add'按钮**
 Open Genymotion and click on 'Add' button.
**2.选择你想要的Android模拟器版本**
Select the device for which you want actual source url.
**3.点击'Next'然后再点击'Next'（在屏幕上会显示要给模拟器改名）**
Click 'Next' and then again 'Next' (on the screen that shows option to rename the device).
**4.等待一会儿直到Genymotion开始下载文件（下载进度条开始显示时）**
Wait for sometime until Genymotion starts downloading the file (i.e. some download progress is shown).
**5.取消下载并关掉Genymotion**
Abort the download process and close Genymotion.
**6.去到“C:\Users\<user_name>\AppData\Local\Genymobile\Genymotion\ova”这个目录，替换user_name为你的用户名，例如我的是：C:\Users\Administrator\AppData\Local\Genymobile\Genymotion\ova**
Go to this directory: C:\Users\<user_name>\AppData\Local\Genymobile\Genymotion\ova, replace <user_name> with your Windows account user name.
**7.在这个目录你可能会看到不止一个.ova文件，按照创建日期和修改日期排序，找到最新创建的那个文件并复制文件名（含扩展名），例如：genymotion_vbox86p_5.0_170928_172212.ova**
In this directory, you will see atleast one '.ova' file. Sort them according to the 'Date created' or 'Date modified' attribute and copy the name of the most recent file with extension e.g. genymotion_vbox86p_6.0_160825_141918.ova. Copy this file name as you'll need it in the next step.
**8.去到“C:\Users\<user_name>\AppData\Local\Genymobile”这个目录你会看到有一个'genymotion.log'文件.用记事本或者notepad++打开，搜索上一个步骤复制的文件名(快捷键是ctrl+F)，然后你会看到一条链接，例如： 08:11:28 [Genymotion] [debug] Downloading file http://dl.genymotion.com/dists/5.0.0/genymotion_vbox86p_5.0_170928_172212.ova**
Go to this path : C:\Users\<user_name>\AppData\Local\Genymobile and you must see a 'genymotion.log' file. Open the file and search the text for the filename copied earlier. You must see it as a part of a link.
e.g. 08:11:28 [Genymotion] [debug] Downloading file http://dl.genymotion.com/dists/7.0.0/ova/genymotion_vbox86p_7.0_161206_183248.ova
**9.复制链接然后粘贴到迅雷下载**
Now, copy the URL and paste it in your browser or in any download manager.
**10.下载完成后，复制下载后的文件到 "C:\Users\<user_name>\AppData\Local\Genymobile\Genymotion\ova"这个目录下面，请确保你下载的文件是'.ova'扩展名，如果是'.tar',重命名扩展名为'.ova'.**
After the file has been downloaded, move it to the directory from where you copied the file name. i.e. C:\Users\<user_name>\AppData\Local\Genymobile\Genymotion\ova
Make sure that the downloaded file has extension '.ova', if it has some other extension like '.tar' (in case of android 7.0), rename the extension to '.ova'.
**11.一切就绪后打开Genymotion，点击'Add'按钮然后选择之前选择相同的虚拟机，然后点击'Next','Next'.现在虚拟机会不用下载就可以部署了**
Now, open Genymotion, click 'Add' and then select the same device that you selected previously, and proceed, rename it if you want and then click 'Next'. Now, the device will be deployed without being downloaded.