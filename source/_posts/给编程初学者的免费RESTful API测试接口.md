---
title: '给编程初学者的免费RESTful API测试接口'
date: 2019-08-11 22:30:32
tags: [restful,api,免费,测试]
categories: 测试
---
原文地址：https://github.com/zhaoweih/Free-RESTful-API  

# 前言

受https://jsonplaceholder.typicode.com 项目启发，想要做一个免费的Restful API接口帮助编程初学者用来测试自己的程式，因为我当时刚开始学编程的时候就对没有免费的Restful API帮助深感苦恼，其实这个项目好几个星期前就想做了，苦于工作时间还有杂七杂八的事情导致一直搁置，所以现在打算一点一点来，先出一个小的版本，让大家试验，如果有任何问题可以发到我邮箱zhaoweihao.dev@gmail.com或者提issues。

# 域名

亚洲[新加坡服务器]: https://sg.zhaoweihao.icu/api   
例如请求连接是/zoos，完整请求连接应该是https://sg.zhaoweihao.icu/api/zoos


# 食用方法

## 1.GET方法
### 1.1列出所有动物园
请求连接：  
`/zoos`

可添加参数：  
`?limit=10`：指定返回记录的数量  
`?offset=10`：指定返回记录的开始位置。  
`?page=2&per_page=100`：指定第几页，以及每页的记录数。  
`?sortby=name&order=asc`：指定返回结果按照哪个属性排序，以及排序顺序。  

所有参数可以都添加，例如：  
`/zoos?page=2&per_page=2&limit=1&offset=1`

返回数据参考：
```json
{
    "code": 200,
    "msg": "查询所有动物园数据成功",
    "data": [
        {
            "_id": "5d32d3be52c99d0521292a40",
            "name": "Guangzhou zoos1",
            "location": "Guangzhou1"
        },
        {
            "_id": "5d32d5cfe7214e067497d33b",
            "name": "ShenZhen zoos1",
            "location": "ShenZhen1"
        },
        {
            "_id": "5d35c7e34c7fd837087d8a01",
            "name": "ShenZhen zoos2",
            "location": "ShenZhen2"
        },
        ...
        {
            "_id": "5d35c8154c7fd837087d8a09",
            "name": "ShenZhen zoos10",
            "location": "ShenZhen10"
        }
    ]
}
```

### 1.2获取某个指定动物园的信息
请求连接：  
`/zoos/ID`

请求成功返回例子：
```json
{
    "code": 200,
    "msg": "查询动物园成功",
    "data": [
        {
            "_id": "5d35c8154c7fd837087d8a09",
            "name": "ShenZhen zoos10",
            "location": "ShenZhen10"
        }
    ]
}
```

## 2.POST方法
### 2.1新建一个动物园
请求连接：  
`/zoos`

Body参数：  
name 动物园名字，例如ShenZhen zoo  
location 动物园位置, 例如ShenZhen

请求成功返回例子：
```json
{
    "code": 200,
    "msg": "添加动物园成功",
    "data": {
        "name": "ShenZhen zoos",
        "location": "ShenZhen",
        "_id": "5d500833225f965c0406bedc"
    }
}
```
## 3.PUT方法
### 3.1更新某个指定动物园的信息（提供该动物园的全部信息）
请求连接：  
`/zoos/ID`

Body参数：  
name 动物园名字，例如ShenZhen zoo11  
location 动物园位置, 例如ShenZhen11

请求成功返回示例：
```json
{
    "code": 200,
    "msg": "更新动物园成功",
    "data": {
        "name": "ShenZhen zoos11",
        "location": "ShenZhen11"
    }
}
```

## 4.PATCH方法
### 4.1更新某个指定动物园的信息（提供该动物园的部分信息）
请求连接：  
`/zoos/ID`

Body参数(可选，无需全部提供)：  
name 动物园名字，例如ShenZhen zoo12  
location 动物园位置, 例如ShenZhen12

请求成功返回示例：
```json
{
    "code": 200,
    "msg": "更新动物园成功",
    "data": {
        "name": "ShenZhen zoos12"
    }
}
```

## 5.DELETE方法
### 5.1删除某个动物园
请求连接：  
`/zoos/ID`

请求成功返回示例：
```json
{
    "code": 200,
    "msg": "删除数据成功",
    "data": [
        {
            "_id": "5d500833225f965c0406bedc",
            "name": "ShenZhen zoos12",
            "location": "ShenZhen11"
        }
    ]
}
```



# 参考

Restful API规范参考阮老师的文章：http://www.ruanyifeng.com/blog/2014/05/restful_api.html

# 程式架构
- Nginx
- Nodejs
- Express.js
- MongoDB

# 最后
这个只是第一个小版本，目前提供了常见的请求方法测试，后面会逐渐增加更多的功能并且把源代码开源。请期待！


# 联系
📮邮箱: zhaoweihao.dev@gmail.com





