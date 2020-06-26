---
title: 关于C++全局重载符号计算的事
top: false
cover: false
toc: true
mathjax: true
date: 2020-06-26 19:35:56
password:
summary:
tags:
- C++
categories:
- 并不简单易懂的C++
---

# Case1

我定义了如下C++结构Point：

```C++
struct Point {
public:
	int x, y;
}
```

并重载了`+`运算符

```C++
// Global
inline const Point& operator +(const Point& lp, const Point& rp) {
	return { lp.x + rp.x, lp.y + rp.y };
}
```

当我这样使用时

```C++
//其中出现的类与函数定义
//......
std::vector<class Fire> m_FireSet;
//......
Fire::Fire(const Point& pos, Type type) :
	m_X(pos.x), m_Y(pos.y), m_Type(type)
{}
//......

m_FireSet.push_back(Fire((center + Point{ ins, 0 }), Fire::Type::Horizontal));
```

出现了一些难以理解的错误：

![](01.png)

我猜测引用的对象可能在何时被析构掉了，导致引用变成了空对象。于是不得不把重载返回的值改为拷贝：

```C++
// Global        not'&'
inline const Point operator +(const Point& lp, const Point& rp) {
	return { lp.x + rp.x, lp.y + rp.y };
}
```

C++，令人敬畏！