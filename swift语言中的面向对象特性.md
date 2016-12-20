---
title: swift语言中的面向对象特性
date: 2016-12-13 10:40:34
tags:
- swift 面向对象特性
comments: true
categories:
- 学习路线
---

*学如弓弩，才如箭镞*
***
>## 面向对象概念和基本特征

面向对象（oop）是现代流行的程序设计方法，是一种主流的程序设计规范。

**其基本思想是使用对象、类、继承、封装、属性、方法等基本概念来进行程序设计**，从现实世界中客观存在的事物出发来构造软件系统，并且在系统构造中尽可能运用人类的自然思维方式。

例如：在真实的学生管理系统中，张三同学和李四同学是现实世界中客观存在的实体，他们有学号、姓名、班级等属性，有学习、问问题、吃饭、走路等动作（或操作）。如果开发一个学生管理软件系统，那么张三同学和李四同学是对象，归纳总结他们共同的属性和方法（操作）后可得出一个抽象的描述，也就是类（class），即“学生类”。

**oop的基本特征包括：封装性、继承性和多态性。**
1. **封装性**。封装性就是尽可能隐蔽对象的内部细节，对外形成一个边界，只保留有限的对外接口使之与外部发生联系。
2. **继承性**。一些特殊类能够具有一般类的全部属性和方法，这称做特殊类对一般类的继承。*例如客轮和轮船，客轮是特殊类，轮船是一般类。通常我们称一般类为父类（或基类），称特殊类为子类（或派生类）。*
3. **多态性**。对象的多态性是指在父类中定义的属性或方法被子类继承之后，可以使用同一个属性或方法在父类及其各个子类中具有不同的含义，这称为多态性。*例如动物都有吃的方法，但是老鼠的吃饭和猫的吃法是截然不同的。*

>## swift中的面向对象类型

在c++和java等语言中面向对象的数据类型只有类，但在swift语言中类、结构体（struct）和枚举（enum）都是面向对象的数据类型，具有面向对象的特征。
**提示：** 在面向对象中类创建对象的过程称为“实例化”，实例化的结果称为“实例”，类的“实例”也称为“对象”。但是在swift中，结构体和枚举的实例一般不称为“对象”，这是因为结构体和枚举并不是彻底的面向对象类型，而只是包含了一些面向对象的特点。例如，在swift中继承只发生在类上，结构体和枚举不能继承。
在swift中，面向对象的概念还有属性、方法、扩展和协议等，这些概念对于枚举、类和结构体等不同类型有可能不同。
>## 枚举

在swift中，枚举的作用已经不仅仅是定义一组常量以及提高程序的可读性，还具有面向对象特性。
枚举声明：
```
enum 枚举名
{
	枚举的定义
}
```
"枚举名" 是该枚举类型的名称。它首先应该是有效的标识符，其次应该遵守面向对象的命名规范。它应该是一个名称，如果采用英文单词命名，首字母应该大写，且应尽量用一个英文单词。这个命名规范也适用于类和结构体的命名。“枚举的定义”是枚举的核心，它由一组成员值和一组相关值组成。

>### 成员值

在枚举类型中定义一组成员，默认情况下不是整数类型，声明枚举示例：
```
enum WeekDays {
	case Monday
	case Tuesday
	case Wednesday
	case Thursday
	case Friday
}
```
声明了weekDays枚举，表示一周中的每个工作日，其中定义了5个成员值Monday、Tuesday...，这些成员值并不是整数类型。
成员值前面还要加上case关键字，也可以将多个成员值放在同一行，用逗号隔开，如下所示：
```
enum WeekDays {
case Monday, Tuesday, Wednesday, Thursday, Friday
}
```
示例：
```
enum WeekDays {
case Mon,Tue,Wed,Thu,Fri
}
var day = WeekDays.Fri   //把WeekDays枚举的成员值赋值给变量
day = .Mon  //简写

func write(day: WeekDays) {
    switch day {
    case .Mon:
        print("周一好")
    case .Tue:
        print("周二好")
    case .Wed:
        print("周三好")
    case .Thu:
        print("周四好")
    case .Fri:
        print("周五好")
    }
}
write(day: day) //输出结果:周一好
```
**提示:** 使用枚举成员赋值时，可以采用完整的`枚举类型名.成员值`的形式，也可以省略枚举类型而采用`.成员值`的形式。省略形式能够访问的前提是，swift编译器能够根据上下文环境推断类型。

枚举类型与switch语句能够很好地配合使用。在swift语句中使用枚举类型可以没有default分支，这在使用其他类型时是不允许的。
**注意**：在swith中使用枚举类型时，switch语句中的case必须全面包含枚举中的所有成员，不能多也不能少，包括使用default的情况下，default也表示某个枚举成员。
>### 原始值

枚举类型提供原始值声明，这些原始值类型可以是字符、字符串、整数和浮点数等。
原始值枚举的语法格式如下：
```
enum 枚举名: 数据类型
{
	case 成员名 = 默认值
	...
}
```

示例代码：
```
enum WeekDays: Int {
	case Mon = 0
	case Tue = 1
	case Wed = 2
	case Thu = 3
	case Fri = 4
	}
```
也可以采用如下简便写法，给第一个成员赋值即可，后面的成员值会依次加1
```
enum WeekDays: Int {
	case Mon = 0, Tue, Wed, Thu, Fri
}
```

`let a = WeekDays.Fri.rawValue`  
`let b = WeekDays(rawValue: 4)`
rawValue属性是将成员值转换为原始值，相反WeekDays(rawValue: 3)是将原始值转换为成员值。

>### 相关值

在swift中除了可以定义一组成员值，还可以定义一组相关值。
```
enum Figure {
    case Rectangle(Int,Int)
    case Circle(Int)
}
```
枚举类型Figure 有两个相关值：Rectangle(矩形)和Circle(圆形)。Rectangle和Circle是与Figure关联的相关值，它们都是元组类型，对于一个特定的Figure实例只能是其中一个相关值。

示例代码：
```
enum Juanyan {             //声明枚举：juanyan
    case Jiage(Int,Int)    //相关值
    case jiaoyouhanliang(Int)  //相关值
}

func printJuanyan(juanyan: Juanyan){
    switch juanyan {
    case .Jiage(let pifa, let lingshou):
        print("批发价格：\(pifa) 零售价格:\(lingshou)")
    case .jiaoyouhanliang(let jyhl):
        print("焦油含量：\(jyhl)")
    }
}
var zh = Juanyan.Jiage(381,450)
printJuanyan(juanyan: zh)  //输出：批发价格：381 零售价格:450

zh = .jiaoyouhanliang(10)
printJuanyan(juanyan: zh)  //输出:焦油含量：10
```

如果某个相关值元组中字段类型一致，需要全部提取，可以将字段前面的let或var移动到相关值前面。例如
```
case .jiage(let pifa, let lingshou):  可以修改为:
case let .jiage(pifa,lingshou):
```

>## 结构体与类

swift语言非常重视结构体，把结构体作为实现面向对象的重要手段。swift中的结构体不仅可以定义成员变量（属性），还可以定义成员方法。因此，我们可以把结构体看作一种轻量级的类。
swift中的类和结构体非常类似，都具有定义和使用属性、方法、下标和构造函数等面向对象特性，但是结构体不具有继承性，也不具备运行时强制类型转换、使用析构函数和使用引用计等能力。

>### 类和结构体定义

使用class关键词定义类，使用struct关键词定义结构体，语法格式如下：
```
class 类名 {
    定义类的成员
}

struct 结构体名 {
    定义结构体的成员
}

```
类名、结构体名的命名规范与枚举类型的要求是一样的。
示例代码：
```
class Juanyan{			  //卷烟类
	var jybm: Int = 0     //卷烟编码属性
	var name: String = "" //卷烟名称属性
    var leibie: String？  //类别属性
	var zy: Zhongyan? 	  //所属中烟属性
}

struct Zhongyan {		 //中烟结构体
	var no: Int = 0 	 //中烟编码属性
	var name: String ="" //中烟名称属性
}
```
Juanyan和Zhongyan是有关联关系的，Juanyan所属中烟的属性zy与Zhongyan关联起来。

可通过下列语句实例化：
```
let jy = Juanyan()
let zy = Zhongyan()
```
**提示：** 实例化之后会开辟内存空间，jy和zy称为"实例"，但只有类实例化的"实例"才能称为“对象”。事实上，不仅仅是结构体和类可以实例化，枚举、函数类型和闭包开辟内存空间的过程也可以称为实例化，结果也可以叫“实例”，但不能叫“对象”。
类声明为let常量还是var变量呢？从编程过程讲类一般声明为let常量。由于类是引用数据类型，声明为let常量只是说明不能修改引用，但是引用指向的对象可以被修改。

>### 再谈值类型和引用类型

数据类型可以分为值类型和引用类型，这是由赋值或参数传递方式决定的。
* 值类型就是在赋值或给函数传递参数时创建一个副本，把副本传递过去，这样在函数的调用过程中不会影响原始数据。
* 引用类型就是在赋值或给函数传递参数的时候把本身引用传递过去，这样在函数的调用过程中会影响原始数据。
在众多的数据类型中，只有类是引用类型，其他类型全部是值类型。即便结构体与类非常相似，它也是值类型。值类型还包括整型、浮点型、布尔型、字符串、元组、集合和枚举。
```
class Juanyan{
    var no: Int = 0
    var name: String = ""
    var jiage: Double = 0
    var lb: String?
    var zy: Zhongyan?
}
struct Zhongyan{
    var no: Int = 0
    var name: String = ""
}

var zy = Zhongyan()
zy.no = 1010
zy.name = "黄金叶"


let jy = Juanyan()
jy.no = 410184
jy.name = "黄金叶(天叶)"
jy.jiage = 680
jy.lb = "一类"
jy.zy = zy

func updateZy( zy: inout Zhongyan){
    zy.name = "河南中烟"
}
print("中烟更新前:\(zy.name)")
updateZy(zy: &zy)  //中烟更新前:黄金叶
print("中烟更新后：\(zy.name)") //中烟更新后：河南中烟

func updateJy(jy: Juanyan){
    jy.jiage = 700
}
print("卷烟更新前\(jy.jiage)") //卷烟更新前680.0
updateJy(jy: jy)
print("卷烟更新后\(jy.jiage)")  //卷烟更新后700.0

```

>### 引用类型的比较

`===`用于比较两个引用是否为同一个实例，`!==`则恰恰相反，只能用于引用类型，也就是类的实例。

>### 运算符重载

运算符重载是通过定义函数来实现的。
示例代码：
```
struct Zy{
    var no: Int = 0
    var name: String = ""
}

var zy1 = Zy()
zy1.no = 10
zy1.name = "河南"

var zy2 = Zy()
zy2.no = 11
zy2.name = "上海"

func ==(a:Zy,b:Zy) -> Bool{
    return a.name == b.name && a.no == b.no
}
func !=(a:Zy,b:Zy) -> Bool{
    if(a.name != b.name || a.no != b.no){
        return true
    }
    return false
}

if zy1 == zy2{
    print("zy1==zy2")
}

if zy1 != zy2{
    print("zy1 != zy2")
}

```
>## 类型嵌套

swift语言中的类、结构体和枚举可以进行嵌套，即在某一类型的{}内部定义类。
类型嵌套的优点是支持访问它外部的成员（包括方法、属性和其他的嵌套类型），嵌套还可以有多个层次。


