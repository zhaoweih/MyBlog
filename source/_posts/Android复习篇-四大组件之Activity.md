---
title: 'Android复习篇-四大组件之Activity'
date: 2018-06-17 18:11:32
tags: [Android]
categories: Android
---


今天花点时间重新看了下郭大的《第一行代码第二版》中四大组件，复习了下四大组件的基础知识，顺便做做笔记

## 四大组件之Activity
活动其实最基础的就是生命周期（Life Cycle），一开始学习时感受不到生命周期的意义，后面做的项目越来越多的时候就体会到生命周期的意义了，
也借这个篇幅说说Activity生命周期和最佳实践，说生命周期最好就是实践得真知了，具体什么时候什么方法被回调，最好亲身体验一遍。

### 生命周期

#### 完全遮挡

1. 当第一个Activity第一次启动会依次执行 onCreate()、onStart()、onResume()。

2. 启动第二个Activity时完全遮挡第一个，第一个会执行onPause()、onStop()。

3. 按下Back键回到第一个，第一个会执行onRestart()、onStart()、onResume()。

#### 未完全遮挡

1. 第一个Activity启动后，弹出一个对话框，第一个会执行onPause()。

2. 对话框消失后，第一个会执行onResume()。

#### 退出

1. 第一个Activity点击返回键退出程序，会执行onPause()、onStop()、onDestroy()。


具体代码可看这里：https://github.com/zhaoweih/booksource/tree/master/chapter2/ActivityLifeCycleTest

### 活动被回收前保存数据
onSaveInstanceState()方法可以保证在活动被回收前一定会被调用
```java
@Override
protected void onSaveInstanceState(Bundle outState) {
	super.onSaveInstanceState(outState);
	String tempData = "Something you just typed";
	outState.putString("data_key", tempData);
}
```

修改MainActivity的onCreate()方法

```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        ...
        if (savedInstanceState != null) {
        	// 获取Activity被回收前的数据
        	String tempData = savedInstanceState.getString("data_key");

        }
    }
```

### 活动的启动模式

#### standard模式

```java
Intent intent = new Intent(FirstActivity.this, FirstActivity.class);
startActivity(intent);
```

FirstActivity -> FirstActivity -> FirstActivity 

每次点击会创建新的FirstActivity实例。

#### singleTop模式

##### 处于栈顶

修改AndroidManifest.xml

```xml
<activity
            android:name=".FirstActivity"
            android:label="This is FirstActivity"
            android:launchMode="singleTop">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```

FirstActivity

当FirstActivity处于栈顶，每次点击都只会有一个FirstActivity实例。

##### 处于非栈顶

FirstActivity.java

```java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
startActivity(intent);
```

SecondActivity.java

```java
Intent intent = new Intent(SecondActivity.this, FirstActivity.class);
startActivity(intent);
```

整个流程 FirstActivity -> SecondActivity -> FirstActivity。

当FirstActivity不是处于栈顶，点击会创建一个新的实例。


#### singleTask模式

修改AndroidManifest.xml

```xml
<activity
           ...
            android:launchMode="singleTask">
           ...
        </activity>
```

FirstActivity -> SecondActivity 

当SecondActivity要启动FirstActivity会发现栈中存在FirstActivity实例，所以会导致SecondActivity出栈，FirstActivity重新回到栈顶

#### singleInstance模式

此时有FirstActivity 、 SecondActivity和ThirdActivity三个Activity。

修改AndroidManifest.xml

```xml
<activity
            android:name=".SecondActivity"
            android:launchMode="singleInstance">
           ...
        </activity>
```

Acitivity启动时打印各个Activity的栈ID。

FirstActivity -> SecondActivity -> ThirdActivity

FirstActivity ID 和 ThirdActivity ID相同，而SecondActivity ID不同。

这时候按返回键退出栈

ThirdActivity -> FirstActivity -> SecondActivity

正常应该是第三个会回到第二个再回到第一个，这里是第三个到第一个，再到第二个。

是因为第三个和第一个栈ID相同，第三个退出了第一个到栈顶，而第二个属于另外的栈，所以第一个推出后再到另外的栈第二个到栈顶，再按退出就会退出程序。


-- 待更新(先睡觉了)
