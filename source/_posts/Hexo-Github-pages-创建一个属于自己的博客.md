---
title: Hexo+Github pages 创建一个属于自己的博客
date: 2017-04-29 13:13:33
tags: [Hexo,Github,博客]
categories: 博客
---
# 写在前面
## 什么是Hexo？
>Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 `Markdown`（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。[Hexo官方文档中文版](https://hexo.io/zh-cn/docs/index.html)



## 适合人群
 * 喜欢写博客
 * 有MarkDown语法基础
 * 会使用版本控制Git
 * 了解使用Github

## 预览效果
我的博客也是用Hexo+Github搭建的，主题用的是Next<br>
[前往我的博客](https://zhaoweihaochina.github.io/)

# 环境准备
## 安装Git
下载[Git](https://git-scm.com/download/win)并执行安装就好了
>由于众所周知的原因，国内下载很慢，Hexo官方文档很体贴的给出了[这个页面](https://github.com/waylau/git-for-win)，里面有收录百度云下载地址。**我的做法是将下载地址复制到迅雷**


## 安装Node.js
在windows下安装[Node.js](https://nodejs.org/en/)十分简单，只需要下载并安装就好了
## 安装Hexo
利用npm命令即可安装

     npm install -g hexo-cli
`注意`
建议挂上代理
`问题`

* 一些旧的文章使用
    npm install -g hexo
会出现错误，最新指令请参考[Hexo官方文档](https://hexo.io/zh-cn/docs/index.html)
* npm ERR! registry error parsing json 错误
可能需要设置npm代理,执行命令
    npm config set registry http://registry.cnpmjs.org
* hexo:command not found
删除刚刚安装的npm目录，重新执行命令npm install -g hexo-cli安装hexo

## 创建hexo文件夹
安装完成后，在自己喜欢的目录下（例如：E:\Myblog\Hexo）执行如下命令(在E:\Myblog\Hexo目录空白处右键选择Git Bash),Hexo就会自动生成所需要的文件

    hexo init
## 安装依赖包

    npm install
`此步建议挂代理`

## 本地预览
现在已经在本地搭建了Hexo博客了，执行如下命令(在E:\Myblog\Hexo)，然后到浏览器输入localhost:4000即可查看

    hexo generate
    hexo server
    
到现在为止，本地hexo博客已经搭建完成，接下来就是部署到Github
`问题`

* 执行hexo server提示找不到该指令
解决办法：
在Hexo 3.0 后server被单独出来了，需要安装server，安装的命令如下：


    npm install hexo -server --save
## github创建博客
* 注册账号
地址:https://github.com/
输入账号、邮箱和密码点击Sign up for Github

![github.jpg](http://op4e089f0.bkt.clouddn.com/image/blogimage/20170429github_page.jpg)

* 创建github pages仓库
这个仓库的名字需要和你的账号对应，格式: yourname.github.io
输入基本信息，然后点击创建仓库.
`帮助`
例如我的github名字是zhaoweihaoChina,那么我的仓库名字就是zhaoweihaoChina.github.io

![create repository.jpg](http://op4e089f0.bkt.clouddn.com/image/blogimage/20170429github_page_2.jpg)

## 生成SSH密钥

ssh-keygen -t rsa -C "你的邮箱地址"，按3个回车，密码为空。

在C:\Users\Administrator.ssh下，得到两个文件id_rsa和id_rsa.pub。

## 在GitHub上添加SSH密钥
打开id_rsa.pub，复制全文。打开 https://github.com/settings/ssh ，Add SSH key，粘贴进去。

# Hexo使用
## 目录结构

    .
    ├── _config.yml#网站配置信息
    ├── package.json#应用程序信息
    ├── scaffolds#模板
    ├── source
    |   ├── _drafts#草稿
    |   └── _posts#文章
    └── themes#主题

更详细说明：[Hexo官方文档-建站篇](https://hexo.io/zh-cn/docs/setup.html)

## 全局配置 _config.yml

    # Hexo Configuration
    ## Docs: http://hexo.io/docs/configuration.html
    ## Source: https://github.com/hexojs/hexo/
    # Site #站点信息
    title:  #标题
    subtitle:  #副标题
    description:  #站点描述，给搜索引擎看的
    author:  #作者
    email:  #电子邮箱
    language: zh-CN #语言
    timezone: Asia/Shanghai#时区
    # URL #链接格式
    url:  #网址
    root: / #根目录
    permalink: :year/:month/:day/:title/ #文章的链接格式
    permalink_defaults:
    # Directory #目录
    tag_dir: tags #标签目录
    archive_dir: archives #存档目录
    category_dir: categories #分类目录
    code_dir: downloads/code
    source_dir: source #源文件目录
    public_dir: public #生成的网页文件目录
    # Writing #写作
    new_post_name: :title.md #新文章标题
    default_layout: post #默认的模板，包括     post、page、photo、draft（文章、页面、照片、草稿）
    titlecase: false #标题转换成大写
    external_link: true #在新选项卡中打开连接
    filename_case: 0
    render_drafts: false
    post_asset_folder: false
    relative_link: false
    highlight: #语法高亮
      enable: true #是否启用
      line_number: true #显示行号
      tab_replace:
    # Category & Tag #分类和标签
    default_category: uncategorized #默认分类
    category_map:
    tag_map:
    # Archives
    2: 开启分页
    1: 禁用分页
    0: 全部禁用
    archive: 2
    category: 2
    tag: 2
    # Server #本地服务器
    port: 4000 #端口号
    server_ip: localhost #IP 地址
    logger: false
    logger_format: dev
    # Date / Time format #日期时间格式
    date_format: YYYY-MM-DD     #参考http://momentjs.com/docs/#/displaying/format/
    time_format: H:mm:ss
    # Pagination #分页
    per_page: 10 #每页文章数，设置成 0 禁用分页
    pagination_dir: page
    # Disqus #Disqus评论，替换为多说
    disqus_shortname:
    # Extensions #拓展插件
    theme: landscape-plus #主题
    exclude_generator:
    plugins: #插件，例如生成 RSS 和站点地图的
    - hexo-generator-feed
    - hexo-generator-sitemap
    # Deployment #部署
    deploy:
      type: git
      repo: 刚刚github创库地址.git
      branch: master
      
更详细说明:[Hexo官方文档-配置篇](https://hexo.io/zh-cn/docs/configuration.html)

`注意`

* 这里的格式很重要！很重要！很重要！（重要的事情说三遍）
* 每个":"冒号后面都有一个空格
* repo: 刚刚github创库地址.git

## Hexo命令的使用
常用命令:

    hexo help #查看帮助
    hexo init #初始化一个目录
    hexo new "postName" #新建文章
    hexo new page "pageName" #新建页面
    hexo generate #生成网页，可以在 public 目录查看整个网站的文件
    hexo server #本地预览，'Ctrl+C'关闭
    hexo deploy #部署.deploy目录
    hexo clean #清除缓存，**强烈建议每次执行命令前先清理缓存，每次部署前先删除 .deploy 文件夹**
    
简写：

    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy
    
更详细的命令:[Hexo官方文档-命令篇](https://hexo.io/zh-cn/docs/commands.html)

## 写文章

新建文章

    hexo new "标题"

在 _posts 目录下会生成文件标题.md

    title: 标题
    date: 2017-04-29 07:56:29 #发表日期，一般不改动
    categories: hexo #文章文类
    tags: [hexo,github] #文章标签，多于一项时用这种格式
    ---
    正文，使用Markdown语法书写

Markdown编辑器推荐：[Cmd Markdown](https://www.zybuluo.com/mdeditor)
Markdown基础语法：[Cmd Markdown 简明语法手册](https://www.zybuluo.com/mdeditor?url=https%3A%2F%2Fwww.zybuluo.com%2Fstatic%2Feditor%2Fmd-help.markdown)

编辑完后保存,hexo server预览

## Hexo部署
执行下列指令即可完成部署。

    hexo generate
    hexo deploy

以下提示说明部署成功

    [info] Deploy done: git
    
打开https://yourname.github.io就可以看到你的博客了



## Hexo主题

这里以配置next主题为例

###### 1. 打开[Hexo官方主题](https://hexo.io/themes/)

###### 2. 找到next主题
  ![next.jpg](http://op4e089f0.bkt.clouddn.com/image/blogimage/20170429github_page_3.jpg)

###### 3. 点击NexT蓝色字体进入进入next的github界面，在介绍里可以找到[next使用文档](http://theme-next.iissnan.com/getting-started.html)
###### 4. 下载主题
  执行如下命令(在E:\Myblog\Hexo)


      git clone https://github.com/iissnan/hexo-theme-next themes/next 
###### 5. 启用主题

   打开_config.yml，找到`theme`字段，，并将其值更改为`next`。


    theme: next
  现在next主题已经配置完成了，执行如下命令(在E:\Myblog\Hexo)

    hexo clean
    hexo server
    
  然后到浏览器输入localhost:4000即可查看

   更加详细的next主题配置请到[next开始使用](http://theme-next.iissnan.com/getting-started.html)和[next主题配置](http://theme-next.iissnan.com/theme-settings.html)查看
   
   
###### 6. 部署到github
设置满意后，执行


    hero generate
    hero deploy

  然后到yourname.github.io即可查看效果（会有一点延迟）
  
  # 写在最后
  
  昨天折腾了一晚上得出来的经验，汇总给大家
  
  如果大家觉得本文对你有帮助，不妨微信扫描以下二维码，请我喝杯咖啡
  
  ![](http://op4e089f0.bkt.clouddn.com/wechatcode.jpg)