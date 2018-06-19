---
title: 'Android流行第三方库教程 - 第一篇 ButterKnife'
date: 2018-06-15 18:11:32
tags: [Android]
categories: Android
---


这个系列会将我平时使用的Android一些流行第三方库拿出来简单讲解一些使用方法和应该在什么时候使用

希望能帮助到更多处在Android初学阶段的朋友们

第一篇先来讲解一个很常用也很好用的View注入框架--黄油刀，这是由著名的大神JakeWharton创作的。虽然现在Kotlin语言在Android端对View绑定的优化使得黄油刀没有在Kotlin中应用的必要（属于后话了），但是在仍在使用Java语言开发的项目中加入这个框架开发效率可谓是如鱼得水啊，非常重要一点是这个框架的加入对性能上是不会有影响的。

ButterKnife项目地址：https://github.com/JakeWharton/butterknife

## 简单使用

- 第一步 在app/build.gradle中 添加依赖 
```
dependencies {
  implementation 'com.jakewharton:butterknife:8.8.1'
  annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
}
```

配置ButterKnife很简单，下面先来简单尝试下ButterKnife的简便吧

- 第二步 使用

首先先来回顾一下在之前我们如何使用按钮的：

在Activity onCreate()方法中：
```java
  Button button = findViewById(R.id.submit);

  button.setOnClickListener(v -> {
            // 这里是点击按钮后的操作
        });
```

现在我们按钮点击事件可以简化成
```java
  @OnClick(R.id.submit) void submit() {
    // 这里是点击按钮后的操作
  }
```

然后所有的View绑定都能简化为
```java
  @BindView(R.id.user) EditText username;
  @BindView(R.id.pass) EditText password;
```

最后别忘了在onCreate()中加入
```java
  ButterKnife.bind(this);
```

整体示例代码：
```java
class ExampleActivity extends Activity {
  @BindView(R.id.user) EditText username;
  @BindView(R.id.pass) EditText password;

  @BindString(R.string.login_error) String loginErrorMessage;

  @OnClick(R.id.submit) void submit() {
    // TODO call server...
  }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.simple_activity);
    ButterKnife.bind(this);
    // TODO Use fields...
  }
}
```
# 更多
## 资源绑定
绑定已经预先定义好的资源
```java
class ExampleActivity extends Activity {
  @BindString(R.string.title) String title;
  @BindDrawable(R.drawable.graphic) Drawable graphic;
  @BindColor(R.color.red) int red; // int or ColorStateList field
  @BindDimen(R.dimen.spacer) Float spacer; // int (for pixel size) or float (for exact value) field
  // ...
}
```

## Fragment绑定
你也能通过提供你的view来绑定任意的对象
```java
public class FancyFragment extends Fragment {
  @BindView(R.id.button1) Button button1;
  @BindView(R.id.button2) Button button2;

  @Override public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.fancy_fragment, container, false);
    ButterKnife.bind(this, view);
    // TODO Use fields...
    return view;
  }
}
```
## Adapter绑定
另一个用途是简化list adapter内部的view holder模式
```java
public class MyAdapter extends BaseAdapter {
  @Override public View getView(int position, View view, ViewGroup parent) {
    ViewHolder holder;
    if (view != null) {
      holder = (ViewHolder) view.getTag();
    } else {
      view = inflater.inflate(R.layout.whatever, parent, false);
      holder = new ViewHolder(view);
      view.setTag(holder);
    }

    holder.name.setText("John Doe");
    // etc...

    return view;
  }

  static class ViewHolder {
    @BindView(R.id.title) TextView name;
    @BindView(R.id.job_title) TextView jobTitle;

    public ViewHolder(View view) {
      ButterKnife.bind(this, view);
    }
  }
}
```

## View列表
你可以将多个view放入List或者array
```java
@BindViews({ R.id.first_name, R.id.middle_name, R.id.last_name })
List<EditText> nameViews;
```
apply方法可以允许你一次绑定所有view
```java
ButterKnife.apply(nameViews, DISABLE);
ButterKnife.apply(nameViews, ENABLED, false);
```
Action 和 Setter接口允许执行一些比较简单的行为
```java
static final ButterKnife.Action<View> DISABLE = new ButterKnife.Action<View>() {
  @Override public void apply(View view, int index) {
    view.setEnabled(false);
  }
};
static final ButterKnife.Setter<View, Boolean> ENABLED = new ButterKnife.Setter<View, Boolean>() {
  @Override public void set(View view, Boolean value, int index) {
    view.setEnabled(value);
  }
};
```

## 解除绑定
Fragment和activity有不同的生命周期。所以当我们在onCreateView方法中绑定一个fragment，要在onDestroyView方法中设置views为null。当执行bind方法时，ButterKnife会返回一个Unbinder实例给你。在适当的生命周期回调方法里执行unbind方法。
```java
public class FancyFragment extends Fragment {
  @BindView(R.id.button1) Button button1;
  @BindView(R.id.button2) Button button2;
  private Unbinder unbinder;

  @Override public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.fancy_fragment, container, false);
    unbinder = ButterKnife.bind(this, view);
    // TODO Use fields...
    return view;
  }

  @Override public void onDestroyView() {
    super.onDestroyView();
    unbinder.unbind();
  }
}
```

## 额外的绑定
默认情况下，所有@Bind和listener绑定都是需要的。当目标view没有找到时会抛出异常。
为了避免这种状况，添加一个@Nullable注解到变量，或者@Optiona注解到方法。
注：所有@Nullable注解都可以用在变量上。
```java
@Nullable @BindView(R.id.might_not_be_there) TextView mightNotBeThere;

@Optional @OnClick(R.id.maybe_missing) void onMaybeMissingClicked() {
  // TODO ...
}
```

##监听器绑定
监听器也可以自动配置在方法上
```java
@OnClick(R.id.submit)
public void submit(View view) {
  // TODO submit data to server...
}
```
所有监听器的参数都是可选的
```java
@OnClick(R.id.submit)
public void submit() {
  // TODO submit data to server...
}
```
定义一个特定类型然后会自动强转型
```java
@OnClick(R.id.submit)
public void sayHi(Button button) {
  button.setText("Hello!");
}
```

通过不提供ID，自定义View能绑定到她们自己的监听器
```java
public class FancyButton extends Button {
  @OnClick
  public void onClick() {
    // TODO do something!
  }
}
```

# 联系方式
zhaoweihao.dev@gmail.com