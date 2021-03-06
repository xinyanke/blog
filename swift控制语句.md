---
title: swift控制语句
date: 2016-11-21 13:51:29
tags:
- swift 控制语句
comments: true
categories:
- 学习路线
---

李克强总理连续三次督促宽带提速，单位虽然装的是光纤，却被限制到变态级别，还不如拨号的网速，最可气的是连技术类网站也开始限制访问了。

>## 分支语句

分支语句又称条件语句

* if 语句
	1. if结构
	```
	if 条件表达式 {
	    语句组
	}
	```
	2. if-else结构
	```
	if 条件表达式 {
	    语句组1
	} else {
	    语句组2
	}
	```
	3. else-if结构
	```
	if 条件表达式1 {
	    语句组1
	} else if 条件表达式2 {
	    语句组2
	} else if 条件表达式3 {
	...
	} else if 条件表达式n {
	    语句组n
	} else {
	    语句组n + 1
	}
	```
* switch 语句
switch语句也称开关语句，它提供多分支程序结构。swift中的switch语句可以使用整数、浮点数、字符、字符串和元组等类型，而且它的数值可以是离散的也可以是连续的范围。swift中的switch语句case分支不需要显式地添加break语句，分支执行完成就会跳出switch语句。
```
switch 条件表达式{
	case 值1:
	  语句组1
	case 值2，值3
	  语句组2
	case 值3：语句组3
	...
	case 判断值n:
	  语句组n
	default:
	  语句组n+1
}

```
每个case后面可以跟一个或多个值，多个值之间用逗号分隔。每个switch必须有一个default语句，它放在所有分支后面。每个case中至少要有一条语句。

* guard语句
guard语句是swift2.x新添加的关键字，与if语句非常类似，可以判断一个条件为true情况下执行某语句，否则终止或跳过执行某语句。它设计目的是替换复杂if-else语句的嵌套，提高程序的可读性。guard语句必须带有else语句。
```
guard 条件表达式 else {
     跳转语句
}
语句组
```
当条件表达式为true时跳过else语句中的内容，执行语句组内容，条件表达式为false时执行else语句中的内容。跳转语句一般是return、break、continue和throw，return和throw关键字用于guard语句中

>## 循环语句
循环语句能够使程序代码重复执行。swift编程语言支持4种循环构造类型：while、repeat-while、for和for-in。
for和while循环是在执行循环体之前测试循环条件，而repeat-while是在执行循环体之后测试循环条件，for-in是for循环的变形，它是专门为集合遍历而设计的。

* while语句
while语句是一种先判断的循环结构
```
while 循环条件 {
   语句组
}
```
while循环没有初始化语句，循环次数是不可知的，只要循环条件满足，循环就会一直进行下去。while循环条件语句中只能写一个表达式，而且是一个布尔型表达式，如果循环体中需要循环变量，就必须在while语句之前对循环体变量进行初始化。

* repeat-while语句
repeat-while语句是事后判断循环条件结构
```
repeat {
    语句组
} while 循环条件
```
repeat-while循环没有初始化语句，循环次数是不可知的，不管循环条件是否满足，都会先执行一次循环体，然后再判断循环条件。如果条件满足则执行循环体，不满足则停止循环。

**提示:** repeat-while是为了替换do-while循环，do关键字在swift2.x中被用于错误处理语句了。

* for语句
```
for 初始化; 循环条件; 迭代 {
    语句组
}
```
先执行初始化语句（其作用是初始化循环变量和其他变量），然后程序会查看循环条件是否满足，如果满足，则继续执行循环体并计算迭代语句，之后再判断循环条件，如此反复，直到判断循环条件不满足时跳出循环。
**提示：** 初始化、循环条件以及迭代部分都可以为空语句（但分号不能省略），三者均为空的时候，相当于一个无限循环。

* for-in 语句
专门用于遍历集合的for循环： for-in循环。

for 循环示例：
```

let numbers = [1,2,3,4,5,6,7,8,9,10]
for var i = 0; i < numbers.count; i++ {
print(i)
}
```

for - in 循环示例：
```

let numbers = [1,2,3,4,5,6,7,8,9,10]
for a in numbers {
print(a)
}
```
如果需要循环变量，可以使用集合enumerate()方法。

```
let numbers = [1,2,3,4,5]
for (index,element) in numbers.enumerate() {
print("\(index):\(element)")
}
```

>## 跳转语句

跳转语句能够改变程序的执行顺序，可以实现程序的跳转。swift有5种跳转语句：break、continue、fallthrough、throw和return。

* break 语句
强行退出循环结构，不执行循环结构中剩余的语句。
在循环体中使用break语句有两种方式：可以带标签，也可以不带标签。语句格式如下：
Break  //不带标签
break label //带标签，label是标签名
定义标签的时候后面需要跟一个冒号。不带标签的break语句使程序跳出所在层的循环体，而带标签的break语句使程序跳出标签指示的循环体。

* continue 语句
用来结束本次循环，跳过循环体中尚未执行的语句，接着进行终止条件的判断，以决定是否继续循环。
continue	//不带标签
continue label  //带标签

* fallthrough 语句
fallthrough是贯通语句，只能使用在switch语句中。

* 范围与区间运算符
闭区间(...) : 包含上下临界值
下临界值 ≤ 范围 ≤ 上临界值
半开区间（..<）包含下临界值，但不包含上临界值
下临界值 ≤ 范围 < 上临界值
**注意：** 在编程之后区间运算符与上下临界值之间不能有空格，例如`80...90`不能写成`80 ... 90`

* 值绑定
在一些控制语句中可以将表达式的值临时赋给一个常量或变量，这些常量或变量能够在该控制语句中使用，这称为“值绑定”
值绑定可以应用于if、guard和switch等控制语句中。

* where 语句
在一些控制语句中使用where语句，进行条件过滤，类似sql语句中的where语句，能够使用where语句的控制语句有switch、for-in和guard等。


