---
title: Android初学者：用知乎Matisse开源项目制作更换应用背景图片功能
date: 2017-08-25 17:41:23
tags: [Android,Matisse]
---

# Android初学者：用知乎Matisse开源项目制作更换应用背景图片功能

## 前言

我搜索了下关于知乎Matisse的使用教程甚少，于是我就想着来做一个教程，这个教程是针对初学者的，因为我自己也是一个初学者，希望对各位刚刚接触Android开发的小伙伴有帮助！

## 关于Matisse

Github页面：https://github.com/zhihu/Matisse

A well-designed local image and video selector for Android

意思既是一个本地图片和视频选择器，well-designed的，效果看起来很棒

预览图：

![](http://op4e089f0.bkt.clouddn.com/2017082501.png)

## 效果

这次我想到了我一个半年前做的项目（我第一个项目），一个倒数日记录器，可以给它增加更换背景图片功能的效果，效果如下，项目地址：https://github.com/zhaoweihaoChina/BigDays (欢迎star和fork)

![](http://op4e089f0.bkt.clouddn.com/2017082502.gif)

## 原理

使用Matisse选择图片后会返回一个图片Uri值，将它显示在ImageView上并保存在Sharedpreferences里头，下次打开这个Activity就从Sharedpreferences里头拿出Uri值并显示在ImageView上，Let's do it！

## 步骤

### 配置Matisse

- 添加依赖

  Gradle:

  ```
  repositories {
      jcenter()
  }

  dependencies {
      compile 'com.zhihu.android:matisse:0.4.3'
  }
  ```

  ​

- 添加Permission

  ``android.permission.READ_EXTERNAL_STORAGE``

  `android.permission.WRITE_EXTERNAL_STORAGE`

  如果是Android 6.0+以上要添加运行时权限获取

  **权限获取代码**

  按钮点击事件（将ZoomActivity替换成你当前Activity的名字）

  ```java
  ...setOnClickListener{
  if(ContextCompat.checkSelfPermission(ZoomActivity.this, Manifest.permission.READ_EXTERNAL_STORAGE)!= PackageManager.PERMISSION_GRANTED){
      ActivityCompat.requestPermissions(ZoomActivity.this,new String[]{Manifest.permission.READ_EXTERNAL_STORAGE},1);
  }else{
      //执行逻辑
  }
  }
  ```

  重写方法

  ```java
  @Override

  public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
      switch(requestCode){
          case 1:
              if(grantResults.length>0&&grantResults[0]==PackageManager.PERMISSION_GRANTED){
                  //执行逻辑
              }else{
                  Toast.makeText(this, "You denied the permission", Toast.LENGTH_SHORT).show();
              }

              break;
          default:
      }
  ```

  ​

- 添加Proguard

  打开proguard-rules.pro，添加下面代码，同步

  ```
  -dontwarn com.squareup.picasso.**
  ```

### 使用Matisse



- 在上方**//执行逻辑**的地方添加如下代码

```java
Matisse.from(ZoomActivity.this)
        .choose(MimeType.allOf())
        .countable(true)
        .maxSelectable(1)//由于这里我只需要一张照片，所以最多选择设置为1
        .gridExpectedSize(getResources().getDimensionPixelSize(R.dimen.grid_expected_size))
        .restrictOrientation(ActivityInfo.SCREEN_ORIENTATION_UNSPECIFIED)
        .thumbnailScale(0.85f)
        .imageEngine(new GlideEngine())
        .forResult(REQUEST_CODE_CHOOSE);
```



- 在头部声明

  `private final int REQUEST_CODE_CHOOSE=0;`



- 重写方法

  ```java
  //这里方法是选择图片后返回的Uri数组
  //返回的Uri数组
  List<Uri> mSelected;
  @Override
  protected void onActivityResult(int requestCode, int resultCode, Intent data) {
      super.onActivityResult(requestCode, resultCode, data);
      if (requestCode == REQUEST_CODE_CHOOSE && resultCode == RESULT_OK) {
          mSelected = Matisse.obtainResult(data);
        //用setImageURI将Uri数组第一个Uri显示在ImageView上
          mImageView.setImageURI(mSelected.get(0));
        //将Uri转换为String保存在SharedPreferences中    
          SharedPreferences.Editor editor=getSharedPreferences("data",MODE_PRIVATE).edit();
          editor.putString("imageUri",mSelected.get(0).toString());
          editor.apply();

          Toast.makeText(this, "Set up successfully", Toast.LENGTH_SHORT).show();

      }else if(requestCode!=RESULT_OK&&requestCode!=RESULT_CANCELED){
        //设置失败提示
          Toast.makeText(this, "Error", Toast.LENGTH_SHORT).show();
      }
  }
  ```



到这里已经将图片显示在ImageView上并保存起来

接下来在每次打开这个Activity时将Uri读取出来并显示在ImageView上

- 在OnCreate方法中添加如下代码

```java
//从SharedPreferences中读取之前保存好的Uri(String)
SharedPreferences preferences=getSharedPreferences("data",MODE_PRIVATE);

String imageUriString=preferences.getString("imageUri",null);
//这里设定用户第一次打开没有保存任何Uri，就显示默认的图片(保存在drawable中)
if(imageUriString!=null){
  //非第一次打开，既有保存Uri
  //String转换为Uri
    Uri imageUri=Uri.parse(imageUriString);
    mImageView.setImageURI(imageUri);
}else{
  //没有保存Uri，显示默认图片
    mImageView.setImageDrawable(getResources().getDrawable(R.drawable.image));
}
```

到这里效果就做好了,Have fun!

## 联系

如果对这篇文章有任何疑问可以联系我

Email:zhaoweihaochn@gmail.com

Blog:http://zhaoweihao.me

## 赞赏

如果喜欢我的文章并对你有帮助，可以给我打赏

![](http://op4e089f0.bkt.clouddn.com/wechatcode.jpg)