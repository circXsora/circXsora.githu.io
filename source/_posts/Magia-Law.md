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

**公/私有字段名、属性**：下划线命名法（字段名一般不公有，属性一般不私有，考虑到字段和属性可能会相互转换，私有公有），字段属性一定是名词，并且用过去式和进行时来区分

``` c#
private int my_health = 1;
```

**公/私有函数名**：大骆驼峰命名，函数名务必是动词

```c#
public int Init() { MyHealth = 1; }
```

**临时变量/函数参数**：小骆驼峰命名

```c#
public int Excute(string actionName){
    var actionId = GetIdByName(actionName);
    Run(actionId);
    return actionId;
}
```

**常量**：全大写+下划线命名

```c#
const int MAX_HEALTH = 10;
```

**事件**：参考https://blog.csdn.net/FliesOfTime/article/details/100688367

事件始终是指某个操作，这个操作可能正在发生，也可能已经发生。 因此与方法一样，事件用谓词命名，谓词时态用于指示事件引发的时间。

**✓ 务必**使用谓词或谓词短语来命名事件。

示例：`Clicked`、`Painting`、`DroppedDown` 等。

**✓ 务必**通过使用现在时态和过去时态，让事件名称含有时间先后的概念。

例如，窗口关闭之前引发的事件称为 `Closing`，窗口关闭之后引发的事件称为 `Closed`。

X 请勿使用 “Before” 或 “After” 前缀和后缀来指示事件之前或之后。 应按前述使用现在时态和过去时态。

**✓ 请使用 “EventHandler” 后缀来命名事件处理程序（用作事件类型的委托）**，如以下示例所示：

```
public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);
```

**✓ 务必**在事件处理程序中使用两个名为 `sender` 和 `e` 的参数。

sender 参数表示引发事件的对象。 sender 参数的类型通常是 `object`，且可能会使用更具体的类型。

**✓ 务必**使用“EventArgs”后缀来命名事件参数类。

***个人建议：对于名称意义不明的事件可添加Event后缀，尽量少用后缀。***

官方参考：https://docs.microsoft.com/zh-cn/dotnet/standard/design-guidelines/names-of-type-members#names-of-events

#### 事件触发方法的名称

事件需要有一个事件触发方法，用于检测事件是否有绑定的方法，如果有就触发事件。直接触发事件在事件没有绑定方法时会引发空异常。

**✓ 务必**使用“On+事件名称”来命名事件触发方法。