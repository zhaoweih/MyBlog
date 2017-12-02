---
title: 用Kotlin开发，Android Studio配置Kotlin篇
date: 2017-08-13 11:35:23
tags: [Kotlin]
categories: Kotlin
---

- # 前言
如今J神加入了GOOGLE，并且专注在Kotlin领域，而且今年的I/O大会宣布Kotlin作为官方开发语言，所以以后的趋势可能要用Kotlin进行Android开发，对于初学者来说，现在学习使用Kotlin进行开发很有必要。即使现在Android还不是Kotlin天下，可是在以后谁都说不定对吧。

 # Android Studio配置Kotlin

## 第一步：安装Kotlin插件
*(Android Studio:以下简称AS)*
由于Kotlin插件只在[AS3.0](https://developer.android.com/studio/preview/index.html)自带。所以之前的版本都必须安装Kotlin插件，在AS中依次点击**File→Settings→Plugins→Install JetBrains plugin**，然后在搜索框填入Kotlin，找到Kotlin点击Install即可(由于我已经安装了，所以我这里没有Install按钮)
![TIM截图20170813102806.png](http://upload-images.jianshu.io/upload_images/5796527-ddaeb6cc097bdc24.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 第二步：创建项目
创建项目的步骤和之前一样，点击(如果在欢迎界面)Start a new Android Studio project 或者 File →New project，配置和之前一样就好
### 转换代码
建立好项目后打开`MainActivity.java`可以按快捷键**Ctrl+Shift+A**或者点击**Help→Find Action**，输入 **Convert Java File to Kotlin File**，又或者点击**Code→ Convert Java File to Kotlin File**都可以将当前java文件转换成kotlin文件

![TIM截图20170813104236.png](http://upload-images.jianshu.io/upload_images/5796527-e0ef520b6bf2ec3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

转换成功后就会发现.java后缀变成了.kt后缀，MainActivity也变成Kotlin语法

![TIM截图20170813104359.png](http://upload-images.jianshu.io/upload_images/5796527-49f3bb348d211230.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 在项目中配置Kotlin
在MainActivity里面随便输入一点东西，AS会在上方会出现一个Configure按钮，点击即可配置Kotlin，或者点击 **Tools→Kotlin→Configure Kotlin in Project**

![TIM截图20170813105024.png](http://upload-images.jianshu.io/upload_images/5796527-535dee76413d9e69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在弹出的窗口选择OK即可

![TIM截图20170813105251.png](http://upload-images.jianshu.io/upload_images/5796527-0f40b86db4bdef37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后会提示你更新项目，点击Sync Now即可

# Kotlin在AS中的扩展
## 添加依赖
在`build.gradle`文件里添加依赖

    apply plugin: 'kotlin-android-extensions'


![TIM截图20170813110211.png](http://upload-images.jianshu.io/upload_images/5796527-d77473662b893c22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 使用扩展
先在`activity_main.xml`中添加一个TextView

    <TextView
        android:id="@+id/hello"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="Hello World!"
       />

然后回到`MainAcitivity.kt`

    import kotlinx.android.synthetic.main.activity_main.*//记得添加这个import

    class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        hello.setText("Hello Kotlin!")//直接用id就可以控制，不用findviewById
    }
    }

运行在手机

![Screenshot_20170813-110806.png](http://upload-images.jianshu.io/upload_images/5796527-245d6eacbf61bb15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用Kotlin扩展将以前java代码简化好多，提高开发效率

更多关于kotlin扩展的解析可以查看[官方文档](http://kotlinlang.org/docs/tutorials/android-plugin.html)

# 其他
拓展阅读：[Android Frameworks Using Annotation Processing](http://kotlinlang.org/docs/tutorials/android-frameworks.html)

# 联系
[Github](https://github.com/zhaoweihaoChina)
[Blog](http://zhaoweihao.me/)
Email:zhaoweihaochn@foxmail.com

# 赞赏

![wechatcode.jpg](http://upload-images.jianshu.io/upload_images/5796527-43b1117577a374a8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)