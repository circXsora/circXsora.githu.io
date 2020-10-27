---
title: Magia Law
top: false
cover: false
toc: true
mathjax: true
date: 2020-08-30 12:46:17
password:
summary:
tags:
- Law
- 软件工程
categories:
- 软件工程
---

# 编程风格

因为自己的编程风格总是换，希望能有一个固定的编程风格，所以写了这篇文章来约束。

### C#

私有字段名：下划线命名法（字段名一般不公有）

``` c#
private int my_health = 1;
```

公/私有属性：大骆驼峰命名

```c#
public int MyHealth { get; set; }
```

公/私有函数名：大骆驼峰命名

```c#
public int Init() { MyHealth = 1; }
```

临时变量/函数参数：小骆驼峰命名

```c#
public int Excute(string actionName){
    var actionId = GetIdByName(actionName);
    Run(actionId);
    return actionId;
}
```

常量：全大写+下划线命名

```c#
const int MAX_HEALTH = 10;
```

