---
title: 'java.lang.NoSuchMethodError: No virtual method getContext()'
date: 2018-01-14 15:51:32
tags: [Android]
categories: 开发
---

Caused by: `val conMgr = connectivityManager(context)`

**java:`getContext()`或kotlin:`context `是出现在API23以后才有的，所以改为使用java:`getActivity()`或kotlin:`activity `就可以解决。**

java:`getContext()`or kotlin:`context `Only available after API 23，so we can solved it by java:`getActivity()`or kotlin:`activity `



After: `val conMgr = connectivityManager(activity)` It works fine.