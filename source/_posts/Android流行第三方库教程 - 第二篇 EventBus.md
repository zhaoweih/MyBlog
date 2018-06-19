---
title: 'Android流行第三方库教程 - 第二篇 EventBus'
date: 2018-06-16 18:11:32
tags: [Android]
categories: Android
---


这是系列的第二篇，这次主要介绍EventBus的配置和简单使用

先来看看官方的介绍：

>EventBus is an open-source library for Android and Java using the publisher/subscriber pattern for loose coupling. EventBus enables central communication to decoupled classes with just a few lines of code – simplifying the code, removing dependencies, and speeding up app development.

>翻译：EventBus 是一个为了解耦而生的开源的Android和Java库，使用发布者和订阅者模式。EventBus用几行代码来实现中央通讯去解耦各个类 - 简化代码，去除依赖，还加快APP开发效率。

好了，官方说明好像说的挺厉害的，那到底对于初学者来说EventBus能用在些什么地方呢？现在先来假设一种情况，你的某一个Activity中的Fragment中的Fragment想去执行另外一个Activity中Fragment的方法，这时候该怎么办，该是用Fragment和Activity通信去干吗？唔，也许可以，但是你得想想，这时候就要Fragment和Activity通信，然后Activity再和Acitivyt通信，最后Acitivy和Fragment通信，似乎有些复杂。。。，或许可以使用接口，或许可以使用广播，但是代码都不会少，而且都会有些复杂。

这时候EventBus就可以横空出世了，接下来就来看看用EventBus怎么做吧，当然EventBus的用武之地肯定不止这些，靠大家自己去想象吧。
## 配置
先在 app/build.gradle中添加
```
compile 'org.greenrobot:eventbus:3.1.1'
```
## EventBus 三部曲
### 1.定义事件：
```java
public static class MessageEvent { /* Additional fields if needed */ }
```
### 2.准备订阅者：
声明和注释你的订阅方法，另外还可以指定进程模式：
```java
@Subscribe(threadMode = ThreadMode.MAIN)  
public void onMessageEvent(MessageEvent event) {/* Do something */};
```

注册和注销你的订阅者。在Android中的例子，Activity和Fragment应该通常根据他们生命周期注册：
```java
 @Override
 public void onStart() {
     super.onStart();
     EventBus.getDefault().register(this);
 }

 @Override
 public void onStop() {
     super.onStop();
     EventBus.getDefault().unregister(this);
 }

```


### 3.发布事件：

```java
 EventBus.getDefault().post(new MessageEvent());
```

## 实际例子
例如我在登录成功后需要更新某些页面

### 1.先定义事件：
```java
public static class MessageEvent { /* Additional fields if needed */ }
```
### 2.发送事件

在登录完成后发送事件：

```java
  EventBus.getDefault().post(new MessageEvent());
```

### 3.接受事件：

在需要更新的页面也注册EventBus，这里是在onCreate方法和onDestroy方法是因为当登录成功发送事件那时候需要更新的页面先前是执行过onStop方法的，如果放在onStart和onStop的话就不能捕获到事件。

```java

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 注册EventBus
        EventBus.getDefault().register(this);
    }


    @Override
    public void onDestroy() {
        // 注销EventBus
        EventBus.getDefault().unregister(this);
        super.onDestroy();

    }

```
接着当接受到事件的时候在主进程更新UI
```java
    @Subscribe(threadMode = ThreadMode.MAIN)
    public void onMessageEvent(LoginActivity.MessageEvent event) {
    	// 在这里更新UI的操作
        requestTecOrStu();
    }
```

## 更多

更详细的使用教程可以参考官方文档：http://greenrobot.org/eventbus/documentation/

## Contact 
zhaoweihao.dev@gmail.com