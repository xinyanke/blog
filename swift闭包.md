---
title: swift闭包
date: 2016-12-10 17:02:01
tags:
- swift 闭包
comments: true
categories:
- 学习路线
---

*生活已经很操蛋，你不能再抱怨*

---

>## 回顾嵌套函数

一门计算机语言要支持闭包有两个前提：
* 支持函数类型，能够将函数作为参数或返回值传递；
* 支持函数嵌套。

>## 闭包的概念

```
func calcul(opr: String)-> (Int,Int)->Int{
    var res: (Int,Int) ->Int
    switch (opr) {
    case "+":
        res = {(a: Int,b: Int) -> Int in   //闭包表达式
        return a + b
        }
    default:
        res = {(a: Int,b: Int) -> Int in  //闭包表达式
        return a - b
    }
}
return res
}
let f1:(Int,Int)->Int = calcul(opr: "+")
print(f1(10,1))
let f2:(Int,Int)->Int = calcul(opr: "-")
print(f2(10,1))

```
闭包是自包含的匿名函数代码块，可以作为表达式、函数参数和函数返回值，闭包表达式的运算结果是一种函数类型。
swift中的闭包可以捕获和存储其所在上下文环境中的常量和变量。这种引用事实上会引起比较麻烦的内存管理问题，好在swift不需要程序员管理内存。

>## 使用闭包表达式

标准语法格式：
```
{ (参数列表)->返回值类型 in
    语句组
}
```
参数列表与函数中的参数列表形式一样，返回值类型类似于函数中的返回值类型，但不同的是后面有in关键字。
swift提供了多种闭包简化写法：

>### 类型推断简化

类型推断是swift的强项，swift可以根据上下文环境推断出参数类型和返回值类型。
标准形式的闭包：
```
{ (a: Int, b: Int) -> Int in
  return a + b
}
```
swift能推断出参数a和b是Int类型，返回值也是Int类型。简化形式如下：
```
{ (a,b) in return a + b }
{ a,b in return a + b } //参数列表括号也可以省略
```
>### 隐藏return关键字

如果在闭包内部语句组只有一条语句，如`return a+b`等，那么这种语句都是返回语句。前面的关键字return可以省略，省略形式如下：
`{a,b in a+b}`
**注意：**省略的前提是闭包中只有一条return语句。下面这样有多条语句的情况下是不允许的：`{a,b in var c = 0, a + b}`

>### 省略参数名

swift的闭包还可以再进行简化。swift提供了参数名省略功能，可以用`$0、$1、$2...`来指定闭包中的参数：$0指代第一个参数，$1指代第二个参数，$2指代第三个参数，以此类推$n+1指代第n个参数。
使用参数名省略功能，在闭包中必须省略参数列表定义，swift能够推断出这些缩写参数的类型。参数列表省略了，in关键字也需要省略，参数名省略之后如下所示：
`{$0 + $1}`

简直太简洁了，爱死你了swift!

```
//闭包从标准写法简化到最后过程

res = {a: Int,b: Int} -> Int in
	return a + b
      } //标准写法

res = {a,b in return a + b}  //类型推断简化

res = {a,b in a + b}  //隐藏return关键字

res = {$0 + $1} //省略参数名
```
>### 使用闭包返回值

闭包表达本质上是函数类型，是有返回值的，可以直接在表达式中使用闭包的返回值。
```
let c: Int = {(a:Int,b:Int) -> Int in
		return a + b}(10,5)
print("10+5=\(c)")
```
**提示：** 理解闭包返回值窍门： 
将闭包部分看成一个函数`{(a:Int,b:Int) -> Int in return a + b}`
`(10,5)`后面的小括号就是调用函数时的参数列表。

>## 使用尾随闭包

闭包表达式可以作为函数的参数传递，如果闭包表达式很长，就会影响程序的可读性。尾随闭包是一个书写在函数括号之后的闭包表达式，函数支持将其作为最后一个参数调用。

```
func calu(opr: String,funN:(Int,Int)->Int) {
    switch (opr) {
    case "+":
        print("10+5=\(funN(10,5))")
    default:
        print("10-5=\(funN(10,5))")
    }
}
calu(opr: "+") { $0 + $1 }
calu(opr:"-"){ $0 - $1 }
```
函数calu最后一个参数funN是(Int,Int)->Int函数类型，funN可以接受闭包表达式。
闭包必须是参数列表的最后一个参数。
**提示：** 尾随闭包有时容易被误认为函数，闭包中往往有in关键字，还有缩写参数$0、$1...等，这些特征在函数中是没有的。

>## 捕获上下文中的变量和常量

嵌套函数或闭包可以访问它所在上下文的变量和常量，这个过程称为捕获值。即便是定义这些常量和变量的原始作用域已经不存在，嵌套函数或闭包仍然可以在函数体内或闭包体内引用和修改这些值。

```
func makeArray() -> (String) -> [String] {
    var ary: [String] = [String]()	//ary作用域是makeArray
    func addele(ele: String) -> [String] {   //定义了嵌套函数addele
        ary.append(ele)
        return ary
    }
    return addele
}

let f1 = makeArray()
print(f1("张三"))
print(f1("李四"))
print(f1("王五"))


let f2 = makeArray()
print(f2("刘备"))
print(f2("关羽"))
print(f2("张飞"))

/*
 输出结果：
 ["张三"]
 ["张三", "李四"]
 ["张三", "李四", "王五"]
 ["刘备"]
 ["刘备", "关羽"]
 ["刘备", "关羽", "张飞"]

 */
```

(完结)
//更新于2016年12月12日
