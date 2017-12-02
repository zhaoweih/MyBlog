---
title: 'Android:2分钟创建一个好看的关于页面'
date: 2017-05-02 20:44:32
tags: [Android,about-page]
categories: Android
---
# 写在前面

通常关于页面是我们开发的时候最容易忽视的页面，一般我都是留在最后才去设计关于页面，但是虽然关于页面并不起眼但是也不能忽视它的作用，所以我就在想能不能在很短时间内创建一个蛮好看的关于页面呢，我在Github找到了这个开源库，介绍里号称可以在两分钟内创建一个好看的关于页面。

- Github原地址：https://github.com/medyo/android-about-page

![](http://op4e089f0.bkt.clouddn.com/cover.png)

# 用法

这个开源库的用法也很简单

首先在app/build.gradle文件中声明这个库的依赖：
```
dependencies {
    compile 'com.github.medyo:android-about-page:1.2'
}
```

然后再修改关于（例如是MainActivity）页面的代码：
```
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        View aboutPage = new AboutPage(this)
                .isRTL(false)
                .setImage(R.drawable.girl)//图片
                .setDescription("道理我都懂，可我就是不听啊")//介绍
                .addItem(new Element().setTitle("Version 1.0"))
                .addGroup("与我联系")
                .addEmail("zhaoweihaochn@foxmail.com")//邮箱
                .addWebsite("http://zhaoweihao.me")//网站
                .addPlayStore("com.example.abouttest")//应用商店
                .addGitHub("zhaoweihaoChina")//github
                .create();

        setContentView(aboutPage);
    }
}
        
```

运行到模拟器

![](http://op4e089f0.bkt.clouddn.com/image/blogimage/20170502QQ%E5%9B%BE%E7%89%8720170502213648.png)

这样一个比较好看的关于页面就创建完毕了

这个开源库让我们建立关于页面的速度快了不是一点

# 更多

我们一般不会这样添加一个关于页面，因为现在要用到Toolbar而不是默认的Actionbar

先修改values/style 换成NoActionBar主题
```
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
       ......
    </style>

</resources>

```

所以我们先在app/res/layout里面新建一个about_layout.xml

```

<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <android.support.design.widget.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="?attr/colorPrimary"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
        app:popupTheme="@style/ThemeOverlay.AppCompat.Light"
        ></android.support.v7.widget.Toolbar>

    </android.support.design.widget.AppBarLayout>
    
    <RelativeLayout
        android:id="@+id/relativeLayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior"
        >
        
        
    </RelativeLayout>

</android.support.design.widget.CoordinatorLayout>


```


然后在包下创建AboutActivity

```

package com.example.abouttest;

import android.os.Bundle;
......

/**
 * Created by Administrator on 2017/5/2.
 */

public class AboutActivity extends AppCompatActivity{

    private RelativeLayout relativeLayout;
    
    private Toolbar toolbar;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.about_layout);
        
        initViews();

        View aboutPage = new AboutPage(this)
                .isRTL(false)
                .setImage(R.drawable.girl)//图片
                .setDescription("道理我都懂，可我就是不听啊")//介绍
                .addItem(new Element().setTitle("Version 1.0"))
                .addGroup("与我联系")
                .addEmail("zhaoweihaochn@foxmail.com")//邮箱
                .addWebsite("http://zhaoweihao.me")//网站
                .addPlayStore("com.example.abouttest")//应用商店
                .addGitHub("zhaoweihaoChina")//github
                .create();

        relativeLayout.addView(aboutPage);
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()){
            case android.R.id.home:
                finish();
                break;
            default:

        }
        return true;
    }
    
    private void initViews(){
        relativeLayout= (RelativeLayout) findViewById(R.id.relativeLayout);
        toolbar= (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        ActionBar actionBar=getSupportActionBar();
        if(actionBar!=null){
            actionBar.setDisplayHomeAsUpEnabled(true);
        }
    }


}



```

最后别忘了在AndroidManifest.xml中声明AboutActivity
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.abouttest">

    <application
       ......
        <activity android:name=".AboutActivity"
        android:label="关于"
        >
        </activity>
    </application>

</manifest>

```

运行到手机，查看

![](http://op4e089f0.bkt.clouddn.com/Screenshot_2017-05-02-22-13-03-092_com.example.ab.png)


虽然效果看上去和上面没有区别，但是我们的aboutpage是在relativelayout里面的，ActionBar也改为Toolbar

# 添加自定义Element

以APP版本为例子 :
```
Element versionElement = new Element();
versionElement.setTitle("Version 6.2");
addItem(versionElement)

```
当前可用的Element类型
```
setTitle(String)	//设置element的标题
setIconTint(Int)	//设置element的颜色
setIconDrawable(Int)	//设置element的图标
setValue(String)	//Set Element value like Facebook ID
setIntent(Intent)	//Set intent to be called on onClickListener
setGravity(Gravity)	//Set a Gravity for the element
setOnClickListener(View.OnClickListener)	//如果Intent不是你想要的，可以在这里重写
```


# 写在最后

如果你阅读本文后受益匪浅，可以不妨请我喝杯咖啡[微信扫描下发二维码向我转账]

![](http://op4e089f0.bkt.clouddn.com/wechatcode.jpg)

# 联系方式
- 邮箱:zhaoweihaochn@foxmail.com
- 博客:[zhaoweihao.me](http://zhaoweihao.me)
- Github:https://github.com/zhaoweihaoChina


