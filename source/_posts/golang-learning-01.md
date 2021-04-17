---
title: golang learning 01
date: 2019-05-26 22:09:52
tags: golang
---

今天开始，深入学习golang语言，记录下来以备后用。

## 变量
### 变量定义
* var用于定义变量，类型放在变量名后面，变脸定义之后会被初始化为零值。
 ```golang
 var x int
 var y = false
 ```
* 可以一次定义多个变量，包括不同初始值定义不同类型
 ```golang
 var x, y int
 var a, s = 100, "abc"
 ```
<!--more-->

### 简短模式
```golang
func main() {
  x := 100
  a, s := 1, "abc"
}
```
如上段代码，简短模式的限制条件
* 定义变量的同时显式初始化；
* 不能提供数据类型；
* **只能在韩式内部使用**；

**简短模式的退化赋值**： 最少有一个新变量被定义，且必须在同一个作用域
```golang
  func main() {
    x := 12
    x, y := 20, 15 // x为退化赋值，y是新定义
  }
```

### 多变量赋值
```golang
func main() {
  x, y := 1, 2
  x, y = y + 3, x + 2
}
```
多变量赋值时，首先计算等号右侧的值，在对左侧变量赋值；

### 空标识符
_ 是空标识符，用作忽略占位符。

## 常量
golang常量用const关键字定义

```golang
const x, y int = 123, 0x22
const s = "hello world"

const {
  i, f = 1, 0.123
  b = false
}
```
此外，也可以在函数内部定义常量，不被使用的常量不会再编译期报错；

在常量组中，如果没有指定类型和初始化值，则与上一行非空常量右值相同
```golang
func main() {
  const {
    x uint16 = 120
    y
    s = "abc"
    z
  }
}
```

## 枚举
golang中没有enum的定义，不过可以借助iota标识符实现一组自增常量值实现枚举；
```golang
  const {
    x = iota // 0
    y        // 1
    z        // 2
  }
```

## 引用类型
特指 slice、map和channel三种类型，引用类型必须通过make函数创建。
