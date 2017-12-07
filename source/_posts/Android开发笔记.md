---
title: Android开发笔记
date: 2017-12-07 15:19:09
tags:
---
我最近在学校期末作业使用Kotlin语言做一个校园社区Android APP，仍然在制作中。。。

Github项目地址：https://github.com/zhaoweihaoChina/hnuplus

这是我用记录一些我在做的时候需要记录的东西，用来以后翻看。也给需要的同学做个参考。

##### Activity 调用 Fragment的公共方法

首先创建一个接口

```java
public interface MyInterface
{
    void myAction() ;
}
```

你的fragment必须声明这个接口

```java
public MyFragment extends Fragment implements MyInterface
```

在你的Activity中，定义一个MyInterface类型的字段

```java
  private MyInterface listener ;

  public void setListener(MyInterface listener)
  {
     this.listener = listener ;
  }
```

当创建你的fragment时添加它

```java
setListener(myFragment);
```

最后，当你想要在activity中调用fragment的方法时可以：

```java
listener.myAction() ; // 这将调用MyFragment类中的方法
```

##### Fragment 调用 Activity的公共方法

```
((YourActivityClassName)getActivity()).yourPublicMethod();
```

##### 保存List<Object>到SharedPreferences中

`Kotlin`

```kotlin
//保存
//这是在Fragment里保存的代码
val postList: List<Post> = ... //你需要保存的list
val appSharedPrefs = PreferenceManager
        .getDefaultSharedPreferences(activity.applicationContext)
val prefsEditor = appSharedPrefs.edit()
val gson = Gson()
val json = gson.toJson(postList)
prefsEditor.putString("MyObject", json)
prefsEditor.commit()
//读取
//这是在Fragment里读取的代码
val appSharedPrefs = PreferenceManager
                        .getDefaultSharedPreferences(activity.getApplicationContext())
val gson = Gson()
val json = appSharedPrefs.getString("MyObject", "")
val type = object : TypeToken<List<Post>>() {
}.type
val postList: List<Post> = gson.fromJson(json,type)
```

##### Uri 转换成Path

`Kotlin`

```kotlin
//uri to path
var path: String? = null
val uri = Matisse.obtainResult(data)[0]//你需要转换的uri
listener!!.showImage(uri)
val filePathColumn = arrayOf(MediaStore.Images.Media.DATA)
val cursor = contentResolver.query(uri, filePathColumn, null, null, null)
if (cursor!!.moveToFirst()) {
    val columnIndex = cursor.getColumnIndex(filePathColumn[0])
    path = cursor.getString(columnIndex)//输出的path
    Log.d("PA",path)
} else {
    //boooo, cursor doesn't have rows ...
}
cursor.close()
```

##### 在Fragment中使用Kotlin-android-extensions

`Kotlin`

```kotlin
override fun onViewCreated(view: View?, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
    btn_pic!!.setOnClickListener {//btn_pic是我在布局定义的按钮id名字
      //逻辑代码
    }
}
```

### 联系我
zhaoweihaochn@foxmail.com