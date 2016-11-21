---
title: swift原生字符串
date: 2016-11-20 17:54:49
tags:
- swift 原生字符串
comments: true
categories:
- 学习路线
---

简单的事情重复做，做到极致。

>## 字符

字符串的组成单位是字符。

* Unicode编码：可以有单字节编码、双字节编码和四字节编码，它们的表现形式是`\u{n}`,其中n为1~8个十六进制数
**提示：** 在swift语言中，不能使用单引号方式，必须使用双引号（“”）把字符括起来。字符串也是使用双引号（“”）把字符括起来。字符类型是:Character，如果省略，编译器自动推断出的类型不是字符类型，而是字符串类型。
* 转义符
```
\t : 水平制表符tab
\n : 换行
\r : 回车
\" : 双引号
\' : 单引号
\\ : 反斜线

```

* 创建字符串
swift字符串类型是String
可通过加号（+）把多个字符拼接成一个字符串。

* 可变字符串
在swift中通过let声明的字符串常量是不可变字符串，var声明的字符串变量是可变字符串。

* 字符串拼接
swift中String字符串之间的拼接可以使用+和+=运算符，String字符串与字符拼接可以使用String的append(_:Character)方法。

**提示：** `\()`语句非常强大，可以将任何数据类型拼接起来。

* 字符串插入、删除和替换
	* 在索引位置插入字符
```
func insert(_ newElement: Character,atIndex i：Index) 

示例代码：在a后面增加"."
var a = "你好，祖国"
a.insert(".",atIndex: a.endIndex)
```
***
	* 在索引位置删除字符
```
func removeAtIndex(_ i: Index) -> Character
示例代码：删除"."字符
a.removeAtIndex(a.endIndex.predecessor())

```
	* 删除指定范围内的字符串
```
func removeRange(_ subRange: Range<Index>)
示例代码：
var aIndex = a.startIndex
var aendIndex = aIndex.advancedBy(9)
var range = aIndex...aendIndex
a.removeRange(range)
```
	* 使用字符串或字符替换指定范围内的字符串
```
func replaceRange(_ subRange: Range<Index>,with newElements: String)
```

* 字符串比较
比较的是Unicode编码
后缀：hasSuffix(_:)方法
前缀: hasPrefix(_:)方法

（完）

