---
title: swift函数
date: 2016-12-08 09:21:57
tags:
- swift 函数
comments: true
categories:
- 学习路线
---

*每一个让你难堪的现在，都有一个不够努力的曾经*

---

将程序中反复执行的代码封装到一个代码块中，这个代码块模仿了数学中的函数，具有函数名、参数和返回值。
它可以独立存在，即全局函数；也可以存在于别的函数中，即函数嵌套；还可以存在于类、结构体和枚举中，即方法。

>## 使用函数

函数的语法格式如下：
```
func 函数名(参数列表) -> 返回值类型 {
    语句组
    return 返回值
}
```
func是定义函数的关键字，函数名需要符合标识符命名规范，多个参数列表之间可以用逗号（，）分隔，极端情况下可以没有参数。
参数语法：`(参数名: 类型)`

参数列表后使用箭头"->"指示返回值类型。返回值有单个值和多个值，多个值返回可以使用元组类型实现。如果函数没有返回值，则“->返回值类型”部分可以省略。
如果函数有返回值，就需要在函数体最后使用return语句将计算的值返回；如果没有返回值，则函数体中可以省略return语句。

示例代码：
```
func lirun(pifa: Double,lingshou: Doublie) -> Double {
	let jisuan = pifa - lingshou
	return jisuan
}
print("利润=\(lirun(pifa:200,lingshou:200))")

```
**提示：** 函数调用时，参数需要指定参数名。

>## 传递参数

swift中的函数很灵活，具体体现在传递参数有多种形式上。

### 使用外部参数名
如示例代码，pifa 和 lingshou 称为 “局部参数名”，只能在函数的内部使用。我们还可以为每个参数提供一个可以在函数外部使用的名称，称为“外部参数名”。可以修改lirun 函数如下：
```
func lirun(P pifa: Double, L lingshou:Double) -> Double {
	let jisuan = pifa - lingshou
	return jisuan
}
print("利润=\(lirun(P: 200,L: 100))")
```
如果使用外部参数名，则P 和L不能省略。

### 省略外部参数名

在定义函数时，使用下划线(_) 表示省略外部参数名，如`_ pifa: Double`

### 参数默认值
在定义函数的时候可以为参数设置一个默认值，当调用函数的时候可以忽略该参数。
```
func juanyan(pinpai: String = "中华") -> String {
return "给我拿条\(pinpai)烟。"
}
let yan = juanyan() //输出结果：给我拿条中华烟。
let yan1 = juanyan(pinpai:"芙蓉王") //输出结果：给我拿条芙蓉王。
```

### 可变参数
swift中函数的参数个数可以变化，它可以接受不确定数量的输入类型参数（这些参数具有相同的类型）,在参数类型名后面加入...的方式来表示这是可变参数。
示例：
```
func heji(xiaoshou:Double...) -> Double {
  var danpin: Double = 0
  for i in xiaoshou {
	danpin += i
    }
   return danpin  		
}

heji(xiaoshou:1,2,3) //结果6

```
### 参数的传递引用

参数传递方式有两种：

* 值类型
给函数传递的是参数的一个副本，这样在函数的调用过程中不会影响原始数据。
除了类，其他的数据类型如整型、浮点型、布尔型、字符、字符串、元组、集合、枚举和结构体全部是值类型。

* 引用类型
把数据本身引用（内存地址）传递过去，这样在函数的调用过程中会影响原始数据。
只有类是引用类型。

凡事都有例外，有的时候就是要将一个值类型参数以引用方式传递，swift提供的inout关键字就可以实现。
示例代码：
```
func inc(value: inout Double,amount: Double = 1.0 ){
value += amount
}
var value: Double = 10.0
inc(value: &value)
print(value)  //输出结果是11

inc(value: &value, amount:100.0)
print(value)  //输出结果是110.0
```
inout标识的参数称为输入输出参数，不能使用var或let标识。
&符号，取出value地址，是传递引用方式，参数标识与inout是相互对应的。

>## 函数返回值

3种形式：
1. 无返回值
2. 单一返回值
3. 多返回值

### 无返回值函数
有的函数只是为了处理某个过程，或者要返回的数据要通过inout类型参数传递出来，这时可以将函数设置为无返回值。所谓无返回值，事实上是void类型，即表示没有数据的类型。
无返回值函数的语法格式有如下3种形式：

```
//形式1：
func 函数名(参数列表){
	语句组
}

//形式2：
func 函数名(参数列表) ->(){
	语句组
}

//形式3：
func 函数名(参数列表) ->Void {
	语句组
}

```
### 多返回值函数

有时候需要函数返回多个值，可以通过两种方式来实现。

* 一种是在函数定义时将函数的多个参数声明为引用类型传递，这样当函数调用结束时，这些参数的值就变化了。

* 另一种是返回元组类型。

元组类型返回多值实现方式：

```
func pos(dt: Double, speed:(x:Int,y:Int)) -> (x:Int, y:Int) {
    let posx: Int = speed.x * Int(dt)
    let posy: Int = speed.y * Int(dt)

    return(posx,posy)
}

let move = pos(dt: 60.0, speed:(10,-5))
print("物体移动:\(move.x),\(move.y)") //物体移动:600,-300

```
参数speed:(x:Int,y:Int) 是元组类型

>### 函数类型

每个函数都有一个类型，使用函数的类型与使用其他数据类型一样，可以声明变量或常量，也可以作为其他函数的参数或者返回值使用。

#### 作为函数返回类型使用
可以把函数类型作为另一个函数的返回类型使用。

示例代码：

```

//计算 商品净利和毛利率  商品属性： 批发价和零售价
//净利 = 零售价-批发价；毛利率 = (零售价-批发价)/零售价*100%

func jingli(pifa:Double,lingshou:Double)->Double{
    let jisuan = lingshou - pifa
    return jisuan
}
func maolilv(pifa:Double,lingshou:Double)->Double{
    let jisuan = (lingshou - pifa)/lingshou * 100
    return jisuan
}
func shangpin(type: String)->(Double,Double)->Double{
    var jsxuanze:(Double,Double)->Double
        switch (type) {
        case "jl":
            jsxuanze = jingli
        case "ml":
            jsxuanze = maolilv
            
        default:
            jsxuanze = jingli
        }
        return jsxuanze
    }

var zhonghua:(Double,Double)->Double = shangpin(type: "jl")
print("中华批发价格381.6,零售450,利润:\(zhonghua(381.6,450))")
//输出：中华批发价格381.6,零售450,利润:68.4
```

### 作为参数类型使用

把函数类型作为另一个函数的参数类型使用，示例代码如下：

```
//计算 商品净利和毛利率  商品属性： 批发价和零售价
//净利 = 零售价-批发价；毛利率 = (零售价-批发价)/零售价*100%

func jingli(pifa:Double,lingshou:Double)->Double{
    let jisuan = lingshou - pifa
    return jisuan
}
func maolilv(pifa:Double,lingshou:Double)->Double{
    let jisuan = (lingshou - pifa)/lingshou * 100
    return jisuan
}
func juanyan(shangpin: (Double,Double)->Double,pifa:Double,lingshou:Double) ->Double{
    let jisuan = shangpin(pifa,lingshou)
    return jisuan
} //参数shangpin类型是函数类型（Double,Double）->Double

var zhonghua: Double = juanyan(shangpin: jingli,pifa:381.6,lingshou:450)
print("中华利润：\(zhonghua)") //输出结果：中华利润：68.4
zhonghua = juanyan(shangpin: maolilv, pifa: 381.6, lingshou: 450)
print("中华毛利:\(zhonghua)") //输出结果：中华毛利:15.2

```
 

>## 嵌套函数

把函数定义在另外的函数体中，称作“嵌套函数”
默认情况下，嵌套函数的作用域在外函数体内，但我们可以定义外函数的返回值类型为嵌套函数类型，从而将嵌套函数传递给外函数，被其他调用者使用。
示例代码如下：

```
func jsq(yunsuanfu: String)-> (Int,Int)->Int{
    
    func jia(a:Int,b:Int)->Int{
        return a + b
    }
    func jian(a:Int,b:Int)->Int{
        return a - b
    }
    var jisuan:(Int,Int)->Int
    switch yunsuanfu {
    case "+":
        jisuan = jia
    case "-":
        jisuan = jian
    default:
        jisuan = jia
    }
    return jisuan
    
}
let sz1:(Int,Int)->Int = jsq(yunsuanfu: "+")
print(sz1(1,1))
let sz2:(Int,Int)->Int = jsq(yunsuanfu: "-")
print(sz2(1,1))
```

//最后更新于2016.12.09 HiTao
(完)

