# Swift初窥

<!-- TOC -->

- [Swift初窥](#swift初窥)
    - [基本内容](#基本内容)
        - [常量和变量](#常量和变量)
        - [类型标注](#类型标注)
        - [类型安全和类型推断](#类型安全和类型推断)
        - [类型别名](#类型别名)
        - [元组](#元组)
        - [可选型](#可选型)
        - [断言和先决条件](#断言和先决条件)
    - [基本运算符](#基本运算符)
        - [赋值运算符](#赋值运算符)
        - [算术运算符](#算术运算符)
        - [比较运算符](#比较运算符)
        - [合并空值运算符(`a ?? b`)](#合并空值运算符a--b)
        - [区间运算符](#区间运算符)
        - [逻辑运算符](#逻辑运算符)
    - [字符串和字符](#字符串和字符)
    - [集合类型](#集合类型)
    - [控制流](#控制流)
        - [循环遍历](#循环遍历)
        - [条件语句](#条件语句)
        - [控制转移语句](#控制转移语句)
    - [函数](#函数)
        - [函数类型](#函数类型)
        - [参数列表](#参数列表)
        - [返回值](#返回值)
    - [闭包](#闭包)
        - [闭包表达式](#闭包表达式)
        - [尾随闭包](#尾随闭包)
        - [捕获值](#捕获值)
        - [逃逸闭包](#逃逸闭包)
        - [自动闭包](#自动闭包)
    - [枚举](#枚举)
        - [枚举值](#枚举值)
        - [关联值](#关联值)
        - [原始值](#原始值)
        - [递归枚举](#递归枚举)
    - [类和结构体](#类和结构体)
    - [属性](#属性)
        - [存储属性](#存储属性)
        - [延迟存储属性](#延迟存储属性)
        - [计算属性](#计算属性)
        - [只读计算属性](#只读计算属性)
        - [属性观察器](#属性观察器)
        - [类型属性](#类型属性)
    - [方法](#方法)
        - [实例方法](#实例方法)
        - [类型方法](#类型方法)
    - [下标](#下标)
    - [继承](#继承)
    - [构造过程](#构造过程)
        - [存储属性初始赋值](#存储属性初始赋值)
        - [构造器](#构造器)
        - [两段式构造过程](#两段式构造过程)
        - [构造器的继承和重写](#构造器的继承和重写)
        - [构造器的自动继承](#构造器的自动继承)
        - [可失败构造器](#可失败构造器)
        - [必要构造器](#必要构造器)
    - [析构过程](#析构过程)
    - [自动引用计数](#自动引用计数)
        - [`循环强引用`](#循环强引用)
        - [弱引用](#弱引用)
        - [无主引用](#无主引用)
        - [闭包引起的循环强引用](#闭包引起的循环强引用)
    - [可选链式调用](#可选链式调用)
    - [错误处理](#错误处理)
        - [使用`throwing`函数传递参数](#使用throwing函数传递参数)
        - [使用`Do-Catch`处理错误](#使用do-catch处理错误)
        - [将错误转换为可选值](#将错误转换为可选值)
        - [禁用错误传递](#禁用错误传递)
        - [指定清理操作](#指定清理操作)
    - [常见的类型处理](#常见的类型处理)
        - [类型转换](#类型转换)
        - [嵌套类型](#嵌套类型)
    - [扩展](#扩展)
    - [协议](#协议)
    - [泛型](#泛型)
        - [类型形式参数](#类型形式参数)
        - [泛型类型](#泛型类型)
        - [类型约束](#类型约束)
        - [关联类型](#关联类型)
        - [泛型下标](#泛型下标)
    - [访问控制](#访问控制)
        - [访问级别](#访问级别)
        - [各种类型的访问控制](#各种类型的访问控制)
    - [高级运算符](#高级运算符)
        - [位运算符](#位运算符)
        - [溢出运算符](#溢出运算符)
        - [优先级和结合性](#优先级和结合性)
        - [运算符函数](#运算符函数)
    - [语法结构](#语法结构)
    - [类型](#类型)
        - [常见的几种类型](#常见的几种类型)
    - [表达式](#表达式)
        - [前缀/后缀表达式](#前缀后缀表达式)
        - [二元表达式](#二元表达式)
        - [三元条件运算符](#三元条件运算符)
        - [类型转换运算符](#类型转换运算符)
        - [字面量表达式](#字面量表达式)
        - [Self表达式和父类表达式](#self表达式和父类表达式)
        - [闭包表达式](#闭包表达式-1)
        - [可选链表表达式和强制取值表达式](#可选链表表达式和强制取值表达式)
    - [语句](#语句)
        - [常见的几种语句](#常见的几种语句)
        - [编译器控制语句](#编译器控制语句)
    - [声明](#声明)
        - [常见的声明关键词](#常见的声明关键词)
    - [特性](#特性)
        - [声明特性](#声明特性)
        - [类型特性](#类型特性)
    - [模式](#模式)
        - [通配符模式](#通配符模式)
        - [标识符模式](#标识符模式)
        - [值绑定模式](#值绑定模式)
        - [元组模式](#元组模式)
        - [枚举用例模式](#枚举用例模式)
        - [可选模式](#可选模式)
        - [表达式模式](#表达式模式)
        - [类型转换模式](#类型转换模式)
    - [Swift 使用 Tips](#swift-使用-tips)
        - [Swift 中的良好编程风格](#swift-中的良好编程风格)
        - [Swift 中的宏定义](#swift-中的宏定义)
        - [NSRange 和 Range 的互转](#nsrange-和-range-的互转)
        - [`substring` 方法/求子串的使用](#substring-方法求子串的使用)
    - [Swift和Objective-C对比](#swift和objective-c对比)
        - [两种语言的区别](#两种语言的区别)
        - [两种语言的混编](#两种语言的混编)

<!-- /TOC -->

## 基本内容

### 常量和变量

使用关键字`let`声明常量,使用关键字`var`声明变量.  
在一行中声明多个变量或者常量时,其间用逗号分隔.

> 使用`let`定义的变量具有不变性。  
针对值类型具有值的不变性，而对于引用类型值保证引用的不变性（不能给引用赋新值，但是引用可以所指的对象是可变的）。

### 类型标注

在声明变量或者常量是在名字后加冒号,空格最后加上使用的类型名称,用来确定变量或者常量能够存储值的类型.  
如果在定义常量或者变量时未设置类型标注,其会在设置初始值时进行[类型推断](#%E5%B8%B8%E8%A7%81%E7%9A%84%E5%87%A0%E7%A7%8D%E7%B1%BB%E5%9E%8B).

### 类型安全和类型推断

Swift会在编译阶段进行类型检查,任何不匹配的类型都会报错.  
如果没有为所需要的值进行类型声明,Swift会使用类型推断功能推断出合适的类型.

### 类型别名

可以使用`typealias`关键字为类型定义别名.

### 元组

元组把多个值合并成单一的复合型的值.  
元组内的值可以是任何类型,而且不必是同一类型.

元组分解时,不需要的数据可以使用`_`代替.还可以使用索引值去除对应的元素值.

### 可选型

某个类型可以有值,也可以根本没有值的特殊类型(`nil`).

> Swift中的`nil`和Objective-C 中的`nil`不同.  
后者是一个指向不存在对象的指针.  
前者不是指针,是值缺失的一种特殊类型.

**强制展开**:如果确定可选型中包含值,可以在名字后使用`!`强制展开来获取值.

**可选型绑定**:使用可选型绑定来判断可选型是否包含值,如果包含就把值赋给一个临时的常量或者变量.

```Swift
if let constantName = someOptional {
    statements
}
```

**隐式展开可选型**:如果确定类型会一直有值,可以在其声明后加上`!`来表示隐式展开可选型.

扩展:[可选类型完美解决占位问题](http://wiki.jikexueyuan.com/project/swift/chapter4/07_Optional_Case_Study.html)

### 断言和先决条件

使用全局函数`assert(_:_:)`来写断言,来断定一个条件为真.  
使用`recondition(_:_:file:line:)`函数来写先决条件.

使用`fatalError(_:file:line:)`函数用来表示致命错误的断言,且该断言在`Release`环境下也会生效.  
该函数还可以用来加在方法中表示不希望别人随意调用,但是又不得不实现的方法.

```swift
required init?(coder aDecoder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
}
```

## 基本运算符

### 赋值运算符

赋值运算符可以跟其他操作符结合组成组合赋值运算符.(`+=`等)

### 算术运算符

常见的四则运算符.

> Swift中算术运算符默认不允许值溢出.(详见[溢出运算符](#%E6%BA%A2%E5%87%BA%E8%BF%90%E7%AE%97%E7%AC%A6))

### 比较运算符

> 相等运算符(`==`)用来判断两个对象的值是否相等或相同.  
等价运算符(`===`和`!==`)用来判断两个对象的引用是否一致.

### 合并空值运算符(`a ?? b`)

```Swift
// a ?? b
// 如果a有值则展开,如果没有值则是nil,返回b
a != nil ? a! : b
```

### 区间运算符

* 闭区间运算符(`a...b`)

  只有闭合区间能够表达元素类型的最大值。

* 半开区间运算符(`a..<b`)

  只有半开范围能够表达空区间的概念（当范围的上下边界相等时）。

* 单侧区间
  使区间尽量超一个方向发展.比如`names[2...]`和`names[...2]`.

### 逻辑运算符

* 逻辑非(`!a`)
* 逻辑与(`a && b`)
* 逻辑或(`a || b`)

在复杂的混合逻辑运算中,可以使用显示括号改变逻辑运算优先级.

## 字符串和字符

字符串是值类型,进行赋值等操作传递的是拷贝份.

## 集合类型

数组(`Array<Element>`),集合(`Set<Element>`)和字典(`Dictionary<Key, Value>`).

集合中存储值必须都是可哈希的.
> 集合是通过判断hash值是否相等去除重复值。
>
> 需要将自定义类型存储在集合类型中时，类型需要遵循`Hashable`协议、还需要对`==`运算符进行重载。  
自定义类型的内容改变后，其hash值就会发生改变。

```swift
// 自定义结构体Person
struct Person {
    var name: String
    var zipCode: Int
    var birthDay: Date
}

// 重载运算符==
extension Person: Equatable {
    static func ==(lhs: Person, rhs: Person) -> Bool {
        return lhs.name == rhs.name && lhs.zipCode == rhs.zipCode && lhs.birthDay == rhs.birthDay
    }
}

// 保证对象可哈希
extension Person: Hashable {
    var hashValue: Int {
        // 使用异或计算hash值
        // 自定义类型的内容改变后，其hash值就会发生改变
        return name.hashValue ^ zipCode.hashValue ^ birthDay.hashValue
    }
}
```

常见的集合操作:
* 使用`intersection(_:)`（交集）方法来创建一个只包含两个集合共有值的新集合.
* 使用`symmetricDifference(_:)`方法来创建一个只包含两个集合各自有的非共有值的新集合.
* 使用`union(_:)`（并集）方法来创建一个包含两个集合所有值的新集合.
* 使用`subtracting(_:)`（补集）方法来创建一个两个集合当中不包含某个集合值的新集合.
* 使用`==`判断两个集合是否包含有相同的值.
* 使用`isSubset(of:)`方法来确定一个集合的所有值是被某集合所包含.
* 使用`isSuperset(of:)`方法来确定一个集合是否包含某个集合的所有值.
* 使用`isStrictSubset(of:)`或者`isStrictSuperset(of:)`方法来确定集合是否为某一个集合的子集或者超集,但两者并不相等.
* 使用`isDisjoint(with:)`方法来判断两个集合是否拥有完全不同的值.

## 控制流

常见的流程控制语句包括:`while`循环和`for-in`循环,分支选择`if`,`guard`和`switch`语句,和流程跳转`break`和`continue`语句.

可以使用`??`运算符为可选值提供默认值.

在控制流语句中可以使用 where 语句和 let 语句。

### 循环遍历

使用`for-in`循环来遍历序列.

遍历字典类型时,获取的对象是键值对组成的元组成员(`(key, value)`).  
还可以遍历由[区间运算符](#%E5%8C%BA%E9%97%B4%E8%BF%90%E7%AE%97%E7%AC%A6)组成的序列.

还可以使用`while`和`repeat-while`进行循环遍历.

### 条件语句

`if`语句和`switch`语句.

> 在Swift中的`switch`语句不再默认从每个case末尾贯穿到下一个case中,因此不再需要显式地使用`break`语句.
> * `switch`语句必须要匹配到每一种case,且每种case都必须有可执行语句.
> * `switch`语句中的每种case都可以匹配多个值,多个值之间使用`,`隔开.
> * `switch`语句中的case值还可以进行**区间匹配**.
> * `switch`语句中的还可以使用**元组**进行匹配.
> * `switch`语句中的还可以将匹配到的值进行**值绑定**为常量或变量,并在函数体内使用.
> * `switch`语句中的还可以使用`where`对匹配值进行检查.

```Swift
let anotherPoint = (2, 0)
switch anotherPoint {
// 使用了元组进行匹配
// 将匹配的值使用值绑定为常量
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
// 使用where语句对匹配值进行检查,筛选出符合条件的值
case let (x, y) where x == y:
    print("somewhere else at (\(x), \(y))")
default:
    print("somewhere else at (\(x), \(y))")
}
```

### 控制转移语句

* `continue`  
表示终止当前循环继续进行下一次循环,而不是退出循环.
* `break`  
终止整个控制流语句.希望提前退出`switch`语句或者循环语句时都可以使用.
* `fallthrough`  
在`switch`某个case后使用`fallthrough`语句,可以使得代码继续执行下一个case.
> 有点类似C语言中`switch`语句中不使用`break`语句时对应case的操作.

* `guard`  
`guard`语句要求一个条件必须是真的才能执行其后的语句.  
功能类似于`if`语句,但是其后必须有一个`else`分句在条件不为真的时候执行.

```Swift
// 判断代码可执行版本,检查API可用性
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

* `return`
* `throw`

## 函数

使用`func`关键字声明函数,函数由函数名,参数列表(形参),返回值组成.
### 函数类型

它由形式参数类型和返回值类型组成.(`(Int, Int) -> Int`)  
函数也是一等公民,可以对函数类型进行相关操作.
### 参数列表

函数参数列表可以为空,还可以指定实际参数标签或省略实际参数标签(使用`_`).  
函数中还可以指定形式参数标签的默认值.  
函数中还可以使用`...`关键字设置可变形式参数.在函数体内部可变参数传入的值被当做对应类型的数组.
函数中可以通过`inout`关键字设置输入输出形式参数.

> 函数调用传入`inout`类型参数时需要使用`&`取得对应变量地址.  
此时传入的参数需要确保已经初始化,因为无法确定在何时会从指针中读取数据.

### 返回值

函数可以无返回值,可以拥有多个返回值(`元组`/`可选元组`),还可以设置函数类型的返回值.

## 闭包

闭包是可以在你的代码中被传递和引用的功能性独立模块.  
闭包能够捕获和存储定义在上下文的任意常量和变量的引用.

闭包和函数都是引用类型.它们赋值时,实际上都是设置相关引用.

> `全局函数`是一个有名字但不会捕获任何值的闭包,  
`内嵌函数`是一个有名字且能从其上层函数捕获值的闭包,  
`闭包表达式`可以捕获其上下文中常量或变量值的没有名字的闭包.

### 闭包表达式
闭包表达式是一种在简短行内就能写完闭包的语法.

```Swift
// parameters支持常量形式参数,变量形式参数和输入输出形式参数,但是不支持默认参数值.
{ (parameters) -> (return type) in
    statements
}
```

Swift中的闭包能够根据实际参数来推断形式参数类型和返回类型,在实际应用中可以省略形式参数类型和返回类型.  
单表达式的闭包还可以省略`return`关键字来隐式返回单个表达式结果.  
Swift自动支持对行内闭包提供简写实际参数名(`$0`,`$1`,`$2`等).  
还可以使用系统支持的运算符函数对闭包进行简化.

```Swift
let names = ["Chris","Alex","Ewa","Barry","Daniella"]
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
// 从语境中推断出参数类型,并省略掉形式参数类型和返回类型
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
// 单表达式闭包的隐式返回.省略掉return字段.
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
// 简写实际参数名
reversedNames = names.sorted(by: { $0 > $1 } )
// 使用系统提供的运算符函数简化
reversedNames = names.sorted(by: >)
```

### 尾随闭包
尾随闭包是一种被书写在函数形式参数的括号外边(后边)的闭包表达式.

```Swift
// 将闭包写在函数方法括号外边
reversedNames = names.sorted() { $0 > $1 }
// 将闭包写在函数名后.由于函数只有一个参数,且使用了尾随闭包的语法,不需要在函数名后写圆括号.
reversedNames = names.sorted { $0 > $1 }
```

### 捕获值
闭包能够从上下文捕获已被定义的常量和变量.
> 嵌套函数可以捕获其外部函数所有的参数以及定义的常量和变量.

### 逃逸闭包
当闭包作为参数传到一个函数中,但是这个闭包在函数返回后才会被执行,就称该闭包从函数中逃逸.  
在定义接受闭包作为参数时,可以在参数名前使用`@escaping`来允许闭包逃逸出该函数.

> 如果将闭包标记为`@escaping`就必须在闭包中显式地引用`self`.

逃逸闭包常用在**异步操作**的函数中:
1. 将闭包保存在函数外部定义的变量中.
2. 异步函数接受一个闭包参数.
3. 异步函数开始后闭包会立即返回,但是闭包会在异步操作完成后再调用.

```Swift
// 定义一个保存闭包对象的数组
var completionHandlers: [() -> Void] = []
// 函数接受一个闭包作为参数,在参数名前使用@escaping允许闭包逃逸出该函数
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    // 将获取的闭包添加到数组中
    completionHandlers.append(completionHandler)
}

// 定义非逃逸闭包
func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}

class SomeClass {
    var x = 10
    func doSomething() {
        // 逃逸闭包必须显式的使用self
        someFunctionWithEscapingClosure { self.x = 100 }
        // 非逃逸闭包可以隐式的使用self
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
// 逃逸闭包未被执行
instance.doSomething()
print(instance.x)
// 打印出 "200"

// 执行逃逸闭包
completionHandlers.first?()
print(instance.x)
// 打印出 "100"
```

### 自动闭包
自动闭包是一种自动创建的闭包,用于包装传递给函数作为参数的表达式.  
通过将参数标记为`@autoclosure`来接收一个自动闭包.

自动闭包可以延迟求值,直到调用这个闭包时代码段才会被执行.

```Swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// 打印出 "5"

// customerProvider的类型为:() -> String
let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// 打印出 "5"

// customerProvider调用后才会执行闭包中的语句
print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// 打印出 "4"
```

## 枚举

在Swift中枚举是一等公民(`first-class`),使用关键字`enum`创建并定义枚举.  
他们可以含有[`计算属性`](#%E5%B1%9E%E6%80%A7),[`实例方法`](#%E6%96%B9%E6%B3%95),[`构造函数`](#%E6%9E%84%E9%80%A0%E8%BF%87%E7%A8%8B),`协议`等(类似`类`).

### 枚举值
1. 不必为每个枚举成员设置值,
2. 可以为枚举成员设置`字符串`,`字符`,`整型`,`浮点型`等初始值.
3. 在设置枚举值和`switch-case`语句中可以省略枚举类型名

>Swift中枚举成员在创建后**不会**被赋予一个默认的`整型值`(不同于在OC中的实现).  
而这些枚举成员本身已经是定义好的枚举对应值.

### 关联值
Swift中枚举类型可以用来存储任意类型的关联值.(`类似于存储了一个方法在枚举中,需要时调用就好`)

```Swift
// 枚举类型为Barcode
enum Barcode {
    // 类型关联值为upc
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
// 通过不同的关联值类型设置枚举值
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")

// 使用switch-case时,必须覆盖所有case,或者使用default代替未尽case
switch productBarcode {
    // 可以省略枚举类型Barcode
    case .upc(let numberSystem, let manufacturer, let product, let check):
        print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
    case .qrCode(let productCode):
        print("QR code: \(productCode).")
}
// QR code: ABCDEFGHIJKLMNOP.
```

### 原始值
枚举成员可以在定义时被默认值(`原始值`)预填充.此时原始值的类型必须相同.  

**原始值的隐式赋值**:在使用原始值为整数(`从0开始`)或者字符串类型(`与枚举成员名相同`)的枚举时,不必为每个枚举成员设置默认值.  
使用枚举成员的`rawValue`属性可以访问该枚举成员的原始值,还可以使用这个初始化方法创建一个新的枚举实例.

```Swift
// 指定枚举成员的类型为Character
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
// possibleCharacter为可选型
let possibleCharacter = ASCIIControlCharacter(rawValue: "1")
```

### 递归枚举
递归枚举有一个或者多个`枚举类型`作为关联值.  
在`枚举成员`前加`indirect`字段来表示该成员可递归,还可以在`枚举类型`前添加字段表示所有成员都是可递归的.

```Swift
// 使用indirect表示枚举成员都可以递归
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
// (5 + 4) * 2
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))

// 定义计算公式,传入枚举类型的表达式
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}
print(evaluate(product))
// 18
```

## 类和结构体

* 相同点:
    * 可以定义`属性`用于存储值
    * 可以定义`方法`用于提供相关功能
    * 可以通过[构造方法](#%E6%9E%84%E9%80%A0%E8%BF%87%E7%A8%8B)定义新实例
    * 都可以使用`点语法`调用(取值/赋值)
* 区别
    * 类允许继承另一个类
    * 类允许在运行时检查实例类型
    * 类允许被多次引用,而结构体是使用*复制*的方式进行传递,不存在`引用计数`概念
    * 类定义时使用`class`关键字,结构体使用`struct`关键字
    * 结构体或者枚举都是**值类型**,在赋值操作中其值会被拷贝.而类是**引用类型**,在赋值操作值不会被拷贝.

```swift
struct Resolution {
    var width = 0
    var height = 0
}
let vga = Resolution(width:640, height: 480)
// 默认构造通过为所有存储属性设置默认值实现
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    // 可选型默认值为nil
    var name: String?
}
enum CompassPoint {
    case North, South, East, West
}
```

>注意:
> * **结构体或者枚举是值类型**(基本的值类型在底层都是以*结构体*存储),定义新值实质上是定义一个新的Swift值类型(类似于`Int`,`Bool`,`Array`,`Dict`等).  
另在OC中`NSArray`,`NSDictionary`类型是**类**的形式存在的.
> * Swift允许直接设置结构体属性的子属性值.  
`someVideoMode.resolution.width = 1280`
> * 子类如果需要重写父类方法,需要使用`override`关键字.

恒等运算符:  
引用类型具有同一性（`identity`）。  
可以使用`等价于`（`===`，不等价于`!==`）来判断两个类类型(`class type`)的常量或者变量引用的是否为**同一个类实例**。

|`==`|`===`|
|:------:|:------:|
|结构相等|指针相等或引用相等|
|两个变量的值是否相等|两个变量是否持有相同的引用|

> * Swift中的`==`表示两个实例的值相等或者相同.  
> * OC中的`==`用于判断是否值相等/为同一对象:对于基本类型比较的是*值*,对于对象类型比较的是*对象地址*(特指不支持运算符重载的语言).  
> * OC中的`isEqual`(以及类似的`isEqualToString`等)判断的是对象的**值**是否相等,是否为其**子类**,再依次遍历对象的属性是否相等.

```objectivec
- (BOOL)isEqual:(id)other {  
    if (other == self)
        return YES;
    if (!other || ![other isKindOfClass:[self class]])
        return NO;
    return [self isEqualToWidget:other];
}

// 逐步遍历对象的各个属性是否相等
- (BOOL)isEqualToWidget:(MyWidget *)aWidget {
    if (self == aWidget)
        return YES;
    if (![(id)[self name] isEqual:[aWidget name]])
        return NO;
    if (![[self data] isEqualToData:[aWidget data]])
        return NO;
    return YES;
}
```

## 属性

### 存储属性
指在特定的类或者结构体的实例中的一个常量(`let`)或变量(`var`).  
还可以在定义属性时指定默认值,也可以在构造工程中修改其值.
### 延迟存储属性
指当第一次被调用时才会计算其初始值的属性,在属性前添加`lazy`关键字标识.

> 常用于耗时的操作,避免不必要的过早初始化,  
其针对的是变量属性,不能对常量属性使用,  
不是线程安全的,需要考虑多线程同步的问题.  

### 计算属性
其不存储值,而是使用`setter`,`getter`来获取,设置属性值.

```swift
struct Point {
    // 存储属性
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}

struct Rect {
    // 存储属性
    var origin = Point()
    var size = Size()
    // 计算属性
    var center : Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        // 可以不声明newCenter,使用newValue代替
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}

var square = Rect(origin: Point(x: 10.0, y: 11.0),size: Size(width: 20.0,height: 30.0))
print("square.origin \(square.origin.x),\(square.center.x)")
// square.origin 10.0,20.0
```

### 只读计算属性
其总是返回一个值,只有`getter`方法而没有`setter`方法.

```swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        // 在书写上可以简化,去掉get关键字和括号
        return width * height * depth
    }
}
```

### 属性观察器
内部用来监听和响应属性值的变化,每次属性值的变化都会调用(即使新值与当前值相等).  
* `willSet`在新的值被设置之前调用(传入新值的默认名称为`newValue`)
* `didSet`在新的值被设置之后调用(传入旧值的默认名称为`oldValue`)

```swift
class StepCounter {
    var totalSteps = 0 {
        willSet {
            print("totalSteps:\(totalSteps),new count:\(newValue)")
        }
        didSet {
            if totalSteps > oldValue {
                print("old count:\(oldValue),increase count:\(totalSteps - oldValue)")
            }
        }
    }
}
let counter = StepCounter()
counter.totalSteps = 100
counter.totalSteps = 120
/*
totalSteps:0,new count:100
old count:0,increase count:100
totalSteps:100,new count:120
old count:100,increase count:20
*/
```

> 属性使用`in-out`方式传入函数也会调用`willSet`和`didSet`方法.[**输入输出参数**]()

### 类型属性
常用来定义某个类型的所有实例的共享数据,比如所有实例都能使用的常量/变量.

>* 使用关键字`static`定义.  
>* 类型属性必须给存储类型属性指定默认值.  
>* 类型属性是通过类型本身来访问.

```swift
struct AudioChannel {
    // 设置最大值
    static let maxAudioLevel = 10
    // 设置历史最大值
    static var historyMaxAudioLevel = 0
    var currentLevel = 0 {
        didSet {
            // 使用类型本身访问,而不是某个实例
            if currentLevel > AudioChannel.maxAudioLevel {
                currentLevel = AudioChannel.maxAudioLevel
            }
            if currentLevel > AudioChannel.historyMaxAudioLevel {
                AudioChannel.historyMaxAudioLevel = currentLevel
            }
        }
    }
}

var leftChannel = AudioChannel()
leftChannel.currentLevel = 11
print(leftChannel.currentLevel)
// 10
```

## 方法

### 实例方法
实例方法要写在它所属的类型的前后大括号之间.

> 实例方法能够隐式访问它所属类型的所有实例方法和属性,  
实例方法只能在现存的实例中调用.

```swift
class Counter {
    var count = 0
    func increment() {
        // self等价于实例本身
        self.count += 1
    }
    func increment(by amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
let counter = Counter()
counter.increment()
counter.increment(by: 5)
counter.reset()
```

在实例方法中修改值类型:如果需要修改结构体或者枚举的属性,需要在方法前增加`mutating`修饰.

```swift
struct Point {
    var x = 0.0, y = 0.0
    // 方法定义时增加mutating,允许修改属性
    mutating func moveByX(deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveByX(2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// "The point is now at (3.0, 4.0)"
```

### 类型方法
类型方法是写在类型本身上的方法,在方法`func`前加`static`关键字来指定.(类比`类型属性`)

> 在`类型方法`方法体中可以直接调用本类的其他`类型方法`/`类型属性`,  
而在`实例方法`方法体中调用时需要添加类型名称

```swift
struct LevelTracker {
    // 类型属性,在属性前加static关键字
    static var highestUnlockedLevel = 1
    var currentLevel = 1
    // 类型方法,在方法前加static关键字
    static func unlock(_ level: Int) {
        // 在类型方法中,可以直接访问类型属性
        // 在此方法体内,self指向的是类型本身,而不是某个实例
        if level > highestUnlockedLevel {
            highestUnlockedLevel = level
        }
    }
    static func isUnLocked(_ level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }
    // 在实例方法中修改内部属性值,在方法前加mutating关键字
    mutating func advance(to level:Int) -> Bool {
        // 在实例方法中调用类型属性/类型方法
        if LevelTracker.isUnLocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}

class Player {
    var tracker = LevelTracker()
    let playerName : String
    func complete(level: Int) {
        // 解锁关卡
        LevelTracker.unlock(level + 1)
        // 调至某关
        tracker.advance(to: level + 1)
    }
    init(name: String) {
        playerName = name
    }
}

var player1 = Player(name: "张三")
// 完成第1关,最高未解锁为第2关
player1.complete(level: 1)
print("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")

var palye2 = Player(name: "李四")
// 新建对象直接调至10关,提示失败
if palye2.tracker.advance(to: 10) {
    print("player is now on level 10")
} else {
    print("level 10 has not yet been unlocked")
}
// 调用类方法判断第10关解锁状态
if LevelTracker.isUnLocked(10) {
    print("player is now on level 10")
} else {
    print("level 10 has not yet been unlocked")
}
/*
highest unlocked level is now 2
level 10 has not yet been unlocked
level 10 has not yet been unlocked
*/
```

## 下标

`下标语法`支持在实例名称后的方括号传入一个/多个索引值来对索引值进行存取.  
1. 定义`下标语法`时需要使用`subscript`字段,指定一个/多个输入参数和返回类型.  
2. `下标方法`可以设置读写权限(使用`setter`和`getter`实现,有点类似计算型属性).
3. `下标方法`支持*下标的重载*(*`通过入参的数量和类型区分`*).  
    下标方法可以接受任意数量的入参,入参的类型也可以是任意类型.返回值的类型也可以是任意类型.  
    下标方法可以有多个不同的实现,使用时根据不同的入参进行区分.

```swift
struct Matrix {
    let rows: Int,columns: Int
    // 使用一维数组保存二维数组数据
    var grids: [Double]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grids = Array(repeating: 0.0, count: rows * columns)
    }
    func indexsIsAvailable(row: Int, column: Int) -> Bool {
        return row >= 0 && column >= 0 && row < rows && column < columns
    }
    // 使用关键字subscript修饰
    subscript(row: Int, column: Int) -> Double {
        // 使用setter和getter方法设置读写权限
        set {
            // 判断数组是否越界
            assert(indexsIsAvailable(row: row, column: column),"Index out of range")
            grids[(row * columns + column)] = newValue
        }
        get {
            assert(indexsIsAvailable(row: row, column: column),"Index out of range")
            return grids[(row * columns + column)]
        }
    }
    // 下标的重载(通过入参的数量和类型区分)
    subscript(valueOfIndex: Int) -> Double {
        assert(valueOfIndex < grids.count, "index out of girds.count")
        return self.grids[valueOfIndex]
    }
}

var matrix = Matrix(rows: 2, columns: 3)
print(matrix)
matrix[1, 1] = 1.0
print(matrix)
print("二维数组第5个元素为:\(matrix[4])")
matrix[1, 3] = 1.0
/*
Matrix(rows: 2, columns: 3, grids: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0])
Matrix(rows: 2, columns: 3, grids: [0.0, 0.0, 0.0, 0.0, 1.0, 0.0])
Assertion failed: Index out of range
*/
```

## 继承

一个类可以继承另一个类的方法,属性和其他特性.
* 基类:Swift中不继承于其它类的类,称为`基类`.若不为新定义的类指定`父类`,该类就自动称为`基类`.
* 子类:`子类`可以继承,重写`父类`的方法,属性和下标等  
> 重写父类相关内容时使用`override`关键字修饰,  
访问父类相关内容时使用`super`关键字修饰.  
可以使用`final`关键字防止父类的相关内容被重写,  
还可以在类前加`final`修饰符防止该类被~~重写~~/**`继承`**.

```swift
// 基类Vehicle
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // 什么也不做-因为车辆不一定会有噪音
    }
}

class Train: Vehicle {
    // 重写父类方法
    override func makeNoise() {
        print("Choo Choo")
    }
}
let train = Train()
train.makeNoise()

class Car: Vehicle {
    var gear = 1
    // 重写父类属性
    override var description: String {
        // 使用super修饰符访问父类属性
        return super.description + " in gear \(gear)"
    }
}
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")

class AutomaticCar: Car {
    // 重写父类属性观察器
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}
let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
/*
Choo Choo
Car: traveling at 25.0 miles per hour in gear 3
AutomaticCar: traveling at 35.0 miles per hour in gear 4
*/
```

## 构造过程

`构造过程`是指使用类,结构体和枚举类型等的实例之前的准备过程,主要包括设置实例中存储类型的初值和其他必须的设置初始化工作.  

### 存储属性初始赋值

类和结构体在创建实例时,**必须**为所有存储型属性设置合适的初始值.  
可以在`构造器`中设置,也可以在定义时为其设置默认值.
> 当为存储属性设置初值时,不会触发`属性观察器`.  
构造过程可以为`常量属性`设置一个确定值,且一旦设置成功后不能再被修改.

### 构造器

构造器在创建创建某个特定类型的新实例时被调用,最简单的形式是以关键字`init`命名.  
* 自定义构造器:可以在自定义构造过程中传入相应的参数数据(类似*自定义方法*).  
    结构体的自定义构造器需要进行逐一设置成员属性([结构体的逐一成员构造器](#%E7%B1%BB%E5%92%8C%E7%BB%93%E6%9E%84%E4%BD%93)).
* 默认构造器(`default initializers`):如果结构体或类的所有属性都有默认值,同时没有自定义的构造器,默认构造器就会生效.  
* 构造器的代理:构造器通过调用其它构造器来完成实例的部分构造过程.
    * 值类型:`结构体`和`枚举类型`只能代理自己的其他构造方法.
    * 类类型:`类类型`除了可以代理自己的其他构造方法外,还可以继承自其它类.它们分别是指定构造器和便利构造器.

        |指定构造器|便利构造器|
        |:------:|:------:|
        |类中最主要的构造器.|类中比较次要的,辅助型构造器.|
        |初始化类中提供的所有属性,<br />并通过调用父类的构造器来实现父类的初始化.|定义用来调用同一个类中的指定构造器,<br />并为其参数提供默认值.|
        |父类的指定构造器|同类的其它构造器,<br />最终导致调用一个指定构造器|
        |每一个类都必须拥有至少一个指定构造器.|只在必要的时候为类提供便利构造器.<br />使用convenience关键字修饰.|

```swift
init(parameters) {
    statements
}
// 使用convenience关键字修饰
convenience init(parameters) {
    statements
}
```

类的构造器代理规则:  
1. `指定构造器`必须调用其直接父类的的指定构造器  
2. `便利构造器`必须调用同类中定义的其它构造器  
3. `便利构造器`必须最终导致一个`指定构造器`被调用  

* `指定构造器`必须总是**向上代理**
* `便利构造器`必须总是**横向代理**

![类的构造器对比](https://quxiaolei.github.io/imgs/initializerDelegation.png)

> 注意:  
值类型的自定义构造器会覆盖`默认构造器`(`结构体类型`还无法访问`逐一成员构造器`).  
如果希望`默认构造器`,`逐一成员构造器`和用户自定义构造器共存,都能用来创建实例,可以将用户自定义构造器写到[扩展](#%E6%89%A9%E5%B1%95)(`extension`)中.

### 两段式构造过程

两段式构造过程可以防止属性值在初始化前被修改,也可以防止属性被另一个构造器意外的赋值.

为确保两段式构造过程执行而进行的4项安全检查:

1. `指定构造器`确保其所在类中的所有属性都已初始化完成,之后再将其它构造任务向上代理给**父类**中的构造器.
> 对象的内存空间只有在其所有的存储型属性被确定后才能完全初始化.
2. `指定构造器`必须先向上代理调用**父类**构造器,然后才能为继承的属性设置新值.
> 如果不这么做,子类为继承属性设置的新值会被父类构造器赋值操作覆盖.
3. `便利构造器`必须先代理调用**同一类**中的其他构造器,然后再为任意属性赋新值.
> 否则,便利构造器赋予的新值会被同一类中的其他指定构造器赋值操作所覆盖.
4. 构造器在第一阶段构造完成之前,不能调用任何实例方法,不能读取任何实例属性的值,不能引用self作为一个值.
> 在第一阶段构造完成前,类实例并不是有效的.进行相关调用会导致报错.

两段式构造过程的构造流程展示:

1. 阶段1
* 某个指定构造器或者便利构造器被调用.
* 此时已经完成新实例内存的分配,但是内存还未被初始化.
* 指定构造器确保所在类中引入的所有存储型属性都已被赋值,存储型属性所属的内存完成初始化.
* 指定构造器调用父类的构造器,完成父类属性的初始化.
* 沿着调用父类构造器的过程一直向上执行,直到到达构造器链的最顶部.
* 当到达了构造器链式最顶部,且已确保所有实例包含的存储属性都被赋值.至此,这个实例的内存被认为已经完全初始化.

![两段式构造过程1](https://quxiaolei.github.io/imgs/twoPhaseInitialization01.png)

构造过程从子类的`便利构造器`调用开始,此时便利构造器无法修改任何属性,它把构造任务代理给同一类中的`指定构造器`.  
`指定构造器`确保所有子类的属性都有值,然后调用父类的`指定构造器`,并沿着构造器链一直向上完成父类的构造过程.

父类的`指定构造器`来确保所有父类的属性都有值.当没有更多的父类需要初始化时就无需继续向上代理.  
此时父类中的所有属性都有了初始值,实例的内存被认为是完全初始化.

2. 阶段2
* 从顶部构造器链一直往下,每个构造器链中类的指定构造器进一步定制.此时构造器可以访问self,修改属性或调用实例方法等.
* 最后,任意构造器链中的便利构造器都可以定制实例和使用self.

![两段式构造过程2](https://quxiaolei.github.io/imgs/twoPhaseInitialization02.png)

父类中`指定构造器`反过来进行实例定制.  
父类中的`指定构造器`完成调用后,子类中的`指定构造器`就可以执行更多的定制操作.  
子类的`指定构造器`完成调用后,最开始调用的`便利构造器`就可以执行更多的定制操作.

参考资料:[两段式构造过程](http://wiki.jikexueyuan.com/project/swift/chapter2/14_Initialization.html#class_inheritance_and_initialization)

### 构造器的继承和重写
Swift中的子类默认是不会继承父类的构造器.子类可以手动继承或重写父类构造器(使用`override`关键词修饰,即使是重写系统的`默认构造器`).

```Swift
class Vehicle {
    var numberOfWheels = 0
    var description: String {
        return "\(numberOfWheels) wheel(s)"
    }
}
let vehicle = Vehicle()
print("Vehicle: \(vehicle.description)")

class Bicycle: Vehicle {
    // 重写父类默认构造器
    override init() {
        // 需要调用父类的默认构造器
        super.init()
        numberOfWheels = 2
    }
}
let bicycle = Bicycle()
print("Bicycle: \(bicycle.description)")
/*
Vehicle: 0 wheel(s)
Bicycle: 2 wheel(s)
*/
```

### 构造器的自动继承
子类在默认情况下不会继承父类的构造器,某些特殊情况下父类构造器是可以被自动继承的.
1. 子类中没有任何`指定构造器`,他会自动继承所有父类的指定构造器.
2. 子类提供了所有父类`指定构造器`的实现.

### 可失败构造器
一个类,结构体或枚举类型(是否含有原始值)的对象在构造过程中有可能失败.`可失败构造器`会创建一个类型为自身类型的`可选类型对象`.其语法为在init关键字后面添加问号(`init?`)(也可以使用`init!`代表该类型为隐式解包可选类型).  
可失败构造器可以传递,可以进行`向上代理`(父类的可失败构造器),`横向代理`(类型中的其他可失败构造器).

```Swift
class Product {
    let name: String
    // 可失败构造器
    init?(name: String) {   
        if name.isEmpty { return nil }
        self.name = name
    }
}

class CartItem: Product {
    let quantity: Int
    init?(name: String, quantity: Int) {
        if quantity < 1 { return nil }
        self.quantity = quantity
        super.init(name: name)
    }
}
```

### 必要构造器
在类的构造器前添加`required`修饰符表示该类的子类必须实现该构造器方法.  
且子类重写父类必要构造器前必须添加该修饰符(重写父类的必要构造器时不需要添加`override`修饰符).

使用闭包或者函数设置属性的默认值:每当某个属性所在类型的新实例被创建时,对应的闭包或函数会被调用(需要在大括号结尾添加`()`),而它们的返回值会当做默认值赋值给这个属性.

```swift
struct Checkerboard {
    let boardColors: [Bool] = {
        var temporaryBoard = [Bool]()
        var isBlack = false
        for i in 1...8 {
            for j in 1...8 {
                temporaryBoard.append(isBlack)
                isBlack = !isBlack
            }
            isBlack = !isBlack
        }
        return temporaryBoard
        // 闭包结尾需要添加大括号使Swift立马执行此包.
    }()
    func squareIsBlackAtRow(row: Int, column: Int) -> Bool {
        return boardColors[(row * 8) + column]
    }
}

let board = Checkerboard()
// 每次调用squareIsBlackAtRow内部执行
print(board.squareIsBlackAtRow(row: 0, column: 1))
print(board.squareIsBlackAtRow(row: 7, column: 7))

```

## 析构过程

`析构器`只适用于**类类型**,当一个类的实例被*释放之前*析构器会被立即调用.用关键字`deinit`来标示.  
在类的定义中,一个类有且只有一个析构器.且析构器不带任何参数(类似于`dealloc`方法).

```swift
class Bank {
    // 类型属性
    static var coinsInBank = 10_000
    // 类型方法
    static func distribute(coins numberOfCoinsRequested: Int) -> Int {
        // 超过余额后,取余额
        let numberOfCoinsToVend = min(numberOfCoinsRequested, coinsInBank)
        coinsInBank -= numberOfCoinsToVend
        return numberOfCoinsToVend
    }
    static func receive(coins: Int) {
        coinsInBank += coins
    }
}
class Player {
    var coinsInPurse: Int
    init(coins: Int) {
        coinsInPurse = Bank.distribute(coins: coins)
    }
    func win(coins: Int) {
        coinsInPurse += Bank.distribute(coins: coins)
    }
    // 在资源释放前调用
    deinit {
        Bank.receive(coins: coinsInPurse)
    }
}

var playerOne: Player? = Player(coins: 100)
print("A new player has joined the game with \(playerOne!.coinsInPurse) coins")
print("There are now \(Bank.coinsInBank) coins left in the bank")
playerOne!.win(coins: 2_000)
print("PlayerOne won 2000 coins & now has \(playerOne!.coinsInPurse) coins")
print("The bank now only has \(Bank.coinsInBank) coins left")
// 设置释放playerOne资源,回收金币
playerOne = nil
print("PlayerOne has left the game")
print("The bank now has \(Bank.coinsInBank) coins")
/*
A new player has joined the game with 100 coins
There are now 9900 coins left in the bank
PlayerOne won 2000 coins & now has 2100 coins
The bank now only has 7900 coins left
PlayerOne has left the game
The bank now has 10000 coins
*/
```

## 自动引用计数

> 引用计数仅仅应用于`类`的实例.`结构体`和`枚举`是`值类型`,不通过引用进行存储和传递.

### `循环强引用`
如果两个类实例互相持有对方的强引用,从而每个实例都让对方一直存在.  

解决方法:使用`弱引用`(weak reference)或者`无主引用`(unowned reference).

> * 两个属性的值都允许为`nil`.这种场景最适合用`弱引用`来解决.
> * 一个属性的值允许为`nil`,而另一个属性的值不允许为`nil`.这种场景最适合通过`无主引用`来解决.
> * 两个属性都必须有值，并且初始化完成后永远不会为`nil`.在这种场景中.需要一个类使用`无主属性`另外一个类使用`隐式解析可选属性`.

### 弱引用
`弱引用`不会对其引用的实例保持强引用,因而不会阻止ARC销毁被引用的实例.在声明属性或者变量时,在其前添加`weak`来表明弱引用.  
> ARC会控制引用的实例被销毁后自动置为`nil`,因此弱引用的对象应该定义为可选型变量.  
当ARC设置设置弱引用为`nil`时,属性观察期不会触发.

### 无主引用
`无主引用`不会牢牢保持住引用的实例.在声明属性或者变量时,在其前添加`unowned`来表明无主引用.

> 无主引用通常都被期望拥有值.  
使用`无主引用`,你必须确保引用始终指向一个未销毁的实例.  
在实例被销毁后,无主引用不能被设为`nil`.

```swift
// 一个客户可能有或者没有信用卡,但是一张信用卡总是关联着一个客户
class Customer {
    let name: String
    // 客户可以没有信用卡,card允许为nil
    var card: CreditCard?
    init(name: String) {
        self.name = name
    }
    deinit { print("\(name) is being deinitialized") }
}
class CreditCard {
    let number: UInt64
    // 每张信用卡一定是对应一个客户的
    // 使用unowned将customer对象设置为无主引用,避免循环强引用
    unowned let customer: Customer
    init(number: UInt64, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    deinit { print("Card #\(number) is being deinitialized") }
}

var john: Customer?
john = Customer(name: "John Appleseed")
john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)
// john释放后,Customer实例被销毁,再也没有指向CreditCard实例的强引用,该实例也就被销毁.
john = nil
/*
John Appleseed is being deinitialized
Card #1234567890123456 is being deinitialized
*/
```

无主引用以及隐式解析可选属性:使用隐式解析可选值意味着满足了类的构造函数的两个构造阶段的要求.通常通过在类型结尾处加上感叹号(`!`)处理.

```swift
// 每个国家必须有首都,每个城市必须属于一个国家.
class Country {
    let name: String
    // 隐式解析可选属性:capitalCity默认值为nil,但是不需要展开它的值就可以访问.
    var capitalCity: City!
    init(name: String, capitalName: String) {
        // 当在构造方法中将name属性赋值后,初始化过程就已经完成,就可以调用隐式的self.
        self.name = name
        self.capitalCity = City(name: capitalName, country: self)
    }
}
class City {
    let name: String
    unowned let country: Country
    init(name: String, country: Country) {
        self.name = name
        self.country = country
    }
}

// 可以通过一条语句同时创建Country和City的实例,而不会产生循环强引用.
var country = Country(name: "Canada", capitalName: "Ottawa")
print("\(country.name)'s capital city is called \(country.capitalCity.name)")
// Canada's capital city is called Ottawa
```

### 闭包引起的循环强引用
把闭包赋值给类实例的某个属性,且闭包体内又使用了该类实例时,就会存在循环强引用.

> 闭包和类一样,都是`引用类型`.闭包的赋值是将闭包的引用进行赋值.  
闭包的循环强引用和类实例的循环强引用不同.闭包的循环强引用一个是闭包,一个是类实例.

```Swift
class HTMLElement {
    let name: String
    let text: String?
    
    // 闭包赋值给了asHTML属性
    // 实例对asHTML有强引用
    lazy var asHTML: Void -> String = {
        // 闭包体中捕获了self,持有了HTMLElement的强引用
        // 将self捕获为无主引用
        [unowned self] in
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    deinit {
        print("\(self.name) is beging deinit")
    }
}

var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello world")
print(paragraph!.asHTML())
// 将paragraph对象置为nil时,析构函数未被调用,证明该对象没有被销毁释放
paragraph = nil
```

解决方案:可以使用`闭包捕获列表`解决闭包引起的循环强引用.

在定义闭包时,同时定义闭包捕获列表作为闭包的一部分.  
捕获列表定义了闭包体内捕获一个或者多个引用类型的规则.

捕获列表中的每一项都有一对元素组成,一个元素是`weak`或`unowned`关键字,一个是类实例的引用或初始化过的变量.这些项在方括号中有逗号分隔.

> 闭包和被捕获实例总是相互引用且同时销毁时,将闭包中的捕获定义为`无主引用`.  
当被捕获的引用**可能**变为nil时,将闭包内的捕获定义为`弱引用`.

```Swift
lazy var someClosure: (Int, String) -> String = {
    [unowned self, weak delegate = self.delegate!] (index: Int, stringToProcess: String) -> String in
    // 这里是闭包的函数体
}
```

* [Strong Reference Cycles Between Class Instances & Strong Reference Cycles for Closures](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html#//apple_ref/doc/uid/TP40014097-CH20-ID51)
* [自动引用计数](http://wiki.jikexueyuan.com/project/swift/chapter2/16_Automatic_Reference_Counting.html)

## 可选链式调用

可选链式调用是一种可以在当前值为`nil`的可选值上请求和调用属性,方法及下标的方法.  
可选链式调用的返回值结果和原始返回结果具有相同的类型,但是被包装成了一个`可选值`.如果可选值有值,那么调用就会成功.  
多个调用在一起可以形成一个调用链.其中任何一个节点为`nil`,整个调用链都会失败.

链式调用的展开:在可选值后使用`?`代替`!`来强制展开值.  
`可选链式调用`可以用在属性调用,可选类型的访问下标(`判断可选类型是否有值`)和方法的可选返回值中.

> 当可选值为空时,**可选链式调用**只会失败,而**强制展开**则会触发运行时错误.  
当连接多层可选链式调用时,返回值仍为原始可选型.

```Swift
class Person {
    var residence: Residence?
}
class Residence {
    var numberOfRooms = 1
}

let john = Person()
// 使用去强制解包会抛出运行时错误
// john.residence展开是没有值的,无法调用对象的numberOfRooms属性
let roomCount = john.residence!.numberOfRooms
print("rooms count:\(roomCount)")
// 使用问号代替感叹号,表明residence对象可能为空.可选链式会返回Int?类型
if let roomCount = john.residence?.numberOfRooms {
    print("rooms count:\(roomCount)")
} else {
    print("unable to get rooms")
}

john.residence = Residence ()
if let roomCount = john.residence?.numberOfRooms {
    print("rooms count:\(roomCount)")
} else {
    print("unable to get rooms")
}
// unable to get rooms
// rooms count:1

// 在可选类型数组变量的下标前使用
if let firstRoomName = john.residence?[0].name {
    print("The first room name is \(firstRoomName).")
} else {
    print("Unable to retrieve the first room name.")
}

var testScores = ["Dave": [86, 82, 84], "Bev": [79, 94, 81]]
testScores["Dave"]?[0] = 91
testScores["Bev"]?[0] += 1
testScores["Brian"]?[0] = 72
// "Dave" 数组现在是 [91, 82, 84]，"Bev" 数组现在是 [80, 94, 81]

// 返回的johnsStreet为String?可选类型
if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}

// 在方法的可选返回值后进行可选链式调用
// buildingIdentifier()是方法的调用,在其后加?是判断其可选返回值
if let beginsWithThe =
    john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
    if beginsWithThe {
        print("John's building identifier begins with \"The\".")
    } else {
        print("John's building identifier does not begin with \"The\".")
    }
}
```

## 错误处理

错误处理是指响应错误,并作出相应处理的过程.Swift提供了对错误的抛出,捕获,传递和操作等一等公民.  
在Swift中使用符合`Error`协议类型的值表示.使用`throw`关键字抛出错误.

> Swift中错误处理并不涉及解除调用栈(代价较高),因此`throw`语句的性能很高.

```Swift
// 使用枚举类型定义错误类型
enum VendingMachineError: Error {
    case invalidSelection                    //选择无效
    case insufficientFunds(coinsNeeded: Int) //金额不足
    case outOfStock                          //缺货
}
// 使用throw直接抛出错误
throw VendingMachineError. insufficientFunds(coinsNeeded: 5)
```

错误处理方式:

* 将错误传递给上级调用函数
* 使用`do-catch`语句处理错误
* 将错误转为`可选类型`处理
* 使用`断言`处理

### 使用`throwing`函数传递参数

`throwing函数`是指在函数声明的参数列表后加上`throws`关键字的函数.  
`throwing函数`可以在其内部抛出错误,并将错误传递到函数被调用时的作用域(`其他函数抛出错误后无法在外部处理`).

```Swift
// 指定返回值类型时,throws的位置要在返回值类型前
func canThrowErrors() throws -> String

// 无返回值函数中throws的位置有所不同
func vend(itemNamed name: String) throws {
        // 使用guard语句来做提前退出方法
        guard let item = inventory[name] else {
            // 抛出错误
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else {
            throw VendingMachineError.outOfStock
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited)
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
```

### 使用`Do-Catch`处理错误

可以使用`Do-Catch`的运行一段闭包代码处理错误.  
如果在`do`子语句的代码中抛出一个错误,这个错误就会和`catch`子句做匹配并做出处理.

在内部未作处理的错误会传递到上一级,被相应的语句捕捉处理.

```Swift
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    // 在调用的方法前加try关键字
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
}
```

### 将错误转换为可选值

使用`try?`将错误转换为一个可选值进行处理(未抛出错误时就是`nil`).

```Swift
func fetchData() -> Data? {
    // 返回的data为Data?
    // 如果抛出错误,data=nil,否则data有值
    if let data = try? fetchDataFromDisk() { return data }
    if let data = try? fetchDataFromServer() { return data }
    return nil
}
```

### 禁用错误传递

某个函数在运行时不会有错误抛出,适合使用禁用错误传递.  
在表达式前面写`try!`来禁用错误传递,会将调用包装在一个不会有错误抛出的运行时断言中,真的抛出错误就会是运行时错误.

```Swift
let photo = try! loadImage(atPath: "./Resources/John Appleseed.jpg")
```

### 指定清理操作

使用`defer`语句在即将离开当前代码块时执行一系列操作.

延迟执行语句由关键字`defer`和要被延迟执行的语句组成.延迟执行语句中不能含有控制转移语句或者错误(即逻辑分支).

延迟执行操作的执行顺序是按照声明顺序**从后向前**.

```Swift
func processFile(filename: String) throws {
    if exists(filename) {
        let file = open(filename)
        defer {
            // 关闭文件.在处理文件后执行.
            close(file)
        }
        while let line = try file.readline() {
            // 处理文件.
        }
    }
}
```

## 常见的类型处理

Swift常见类型详见->[类型](#%E7%B1%BB%E5%9E%8B)

### 类型转换

类型转换可以判断实例的类型,也可以将实例看做是父类或者子类的实现.  
类型转换在Swift中使用`is`和`as`关键字实现.

类型检查:使用`is`来检查实例是否是某一特定子类型.

向下转型:常量或者变量在底层可能属于一个子类,可以使用类型转换操作符(`as?`或者`as!`)向下转到它的子类型.

`Any`和`AnyObject`两种特殊的类型别名:
* `Any`可以表示任何类型,包括函数类型,甚至是可选类型.
* `AnyObject`可以表示任何类类型的实例.

### 嵌套类型

要在一个类型中嵌套另一个类型,需要将嵌套的定义写在其外部类型的`{}`作用域内.  
在外部引用嵌套类型时,在嵌套类型的类型名前加上其外部类型的类型名作为前缀.

```Swift
struct BlackjackCard {
    enum Suit: Character {
        case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
    }
    
    enum Rank: Int {
    }
    
    // 声明属性rank和suit
    let rank: Rank, suit: Suit
    var description: String {
        return "output"
    }
}
// 引用嵌套类型
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
```

## 扩展

扩展就是为已有类,结构体,枚举类型或者协议类型添加新功能.其中包括在没有权限获取原始源代码的情况下扩展类型的能力(`逆向建模`).  
扩展时使用`extension`关键字.

> 扩展是为了避免出现*类继承*的情况.  
扩展是向类型中添加新的功能,不是重写已有功能.  
扩展定义会改变该类型的所有实例,不论其创建顺序.

> **NOTICE**:Swift 4.0不再允许重载`extension`中的方法(包括`instance`,`static`,`class`方法).

Swift中的扩展支持:
* 添加计算型属性和计算性类型属性

```swift
extension Double {
    var km: Double { return self*1_000.0 }
    var m: Double { return self }
    var mm: Double { return self/1_000.0 }
    var ft: Double { return self/3.28084 }
}
// 设置计算型属性扩展
let oneInch = 25.4.mm
print("one inch is \(oneInch) meters")
let threeFeet = 3.ft
print("three feet is \(threeFeet) meters")
let aMarathon = 42.km + 195.m
print("a marathon is \(aMarathon) meters")
// one inch is 0.0254 meters
// three feet is 0.914399970739201 meters
// a marathon is 42195.0 meters
```

* 添加实例方法和类型方法

```Swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}
3.repetitions {
    print("hello world")
}

extension Int {
    // 在实例方法中修改属性,需要在方法前加mutating
    mutating func square() {
        self = self * self
    }
}
var someInt = 3
someInt.square()
// someInt 的值现在是 9
```

* 提供新的构造器

通过扩展为已有类型增加新的构造器.但是只能添加`便利构造器`,不能添加新的`指定构造器`或`析构器`(这两种构造器必须由原始类实现).

```Swift
extension Rect {
    // 结构体为center,size等存储属性提供了默认值.
    // 已经存在了默认构造器,可以增加新的构造器.
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```

* 定义下标

扩展可以为已有类型添加新的下标.

```Swift
extension Int {
    subscript(digitIndex: Int) -> Int {
        var decimalBase = 1
        for _ in 0..<digitIndex {
            decimalBase *= 10
        }
        return (self / decimalBase) % 10
    }
}

746381295[0]
// 返回 5
746381295[1]
// 返回 9
```

* 定义和使用新的嵌套类型
* 使某个已知类型符合某协议

## 协议

`类`,`结构体`或`枚举`都可以遵循协议,并可以为协议定义提供具体实现.  
要让自定义类型遵循某个协议时,要在类型名称后加协议名称,并用`:`分割,多个协议用`,`分割.

* 属性要求

协议不指定属性是存储属性还是计算型属性,只指定属性的名称和类型.还可以指定属性的可读写限制.

协议中使用`var`关键字来声明变量属性,在类型声明后加上`set/get`来控制属性的读写.  
也可以使用`static`/`class`关键字作为前缀来声明类型属性.

```Swift
// 任何遵守SomeProtocol协议的类型,都必须有个可读可写的mustBeSettable属性和只读的doesNotNeedToBeSettable属性
protocol SomeProtocol {
    // 可读可写
    var mustBeSettable: Int { get set }
    // 只读
    var doesNotNeedToBeSettable: Int { get }
}
```

* 方法要求

协议可以要求遵循协议的类型实现某些指定的`实例方法`或者`类方法`.  
也可以使用`static`/`class`关键字做前缀来声明类型方法.

> 协议中定义的方法不支持默认参数值.

```Swift
protocol RandomNumberGenerator {
    func random() -> Double
}
```

* Mutating方法要求

Mutating方法允许在方法中改变方法所属的实例.  
常在`func`关键字前加`mutating`关键字作为前缀,表示可以在该方法中修改所属实例以及实例的任意属性值.

```Swift
protocol Togglable {
    // toggle方法在定义时使用mutating关键字,表示支持改变该实例属性
    mutating func toggle()
}

enum OnOffSwitch: Togglable {
    case off,on
    mutating func toggle() {
        switch self {
        case .off:
            self = .off
        case .on:
            self = .on
        }
    }
}

var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
// lightSwitch 现在的值为 .On
```

* 构造器要求

构造器可以在遵循协议的类型中实现指定的构造器.

在类中实现构造器时,必须为构造器实现前加`required`修饰符.  
子类重写父类的指定构造器时,需要在构造器前加`override`修饰符.

```Swift
protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // 这里是构造器的实现部分
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
    // 因为遵循协议，需要加上 required
    // 因为继承自父类，需要加上 override
    required override init() {
        // 这里是构造器的实现部分
    }
}
```

* 将协议作为类型

协议的常见使用场景:

1. 作为函数,方法 或者构造器中的参数类型或者返回值类型.
2. 作为常量,变量或者属性的类型.
3. 作为数组,字典或者其他容器中的元素类型.

* 委托代理模式

`委托`允许类或者结构体将一些需要它们负责的功能委托给其他类型的实例处理.  
可以定义协议来封装需要被委托的功能,就可以确保遵循协议的类型能够提供这些功能.

* 通过扩展遵循协议  
通过空扩展体为原始类型扩展遵循协议.
* 协议类型的集合
* 协议的继承

协议能够继承一个或者多个其他协议,可以在继承协议的基础上增加新的需求.

* 类类型专属协议

在协议的继承列表中,通过添加`class`关键字来限制协议只能被类类型遵循,而其他类型不能遵循该协议.

* 协议合成

当需要同时遵循多个协议时,可以将多个协议采用`&`进行组合,称为`协议合成`.

* 检查协议一致性

使用`is`和`as`操作符来检查协议的一致性,还可以转换到指定的协议类型([类型转换](#%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2)).

* 可选的协议要求

通过使用`optional`关键字作为前缀来定义可选要求,使得遵循协议的类型可以选择是否实现这些要求.  
使用`@objc`关键字可以标记协议只能被继承自Objective-C的类或者`@objc`类遵循.

使用可选要求时,它们的类型会变成可选型(例如整个函数类型变为可选型).

* 协议扩展

协议可以通过扩展为遵循协议的类型提供属性,方法以及下标的实现.

协议扩展可以使用自定义实现代替扩展中的默认实现.

扩展协议时可以指定一些限制条件,只有满足这些限制条件时,才能获得协议扩展提供的默认实现.  
限制条件写在协议名后,使用`where`关键字来描述.可以使用`Self`来表示约束泛型,类似于OC中的`instancetype`.

## 泛型

泛型函数可以用于任何类型.  
泛型函数:通过在函数名后跟上一对尖括号(`<>`),括号内是类型的形式参数名.

```Swift
// 交换两个int值
func swapTwoInts(_ a: inout Int, _ b: inout Int)
// 交换两个值,在<>内标出支持的类型
// T是占位符类型,表示任意类型
func swapTwoValues<T>(_ a: inout T, _ b: inout T)
```

### 类型形式参数

`swapTwoValues(_:_:)`函数中,占位符类型`T`就是一个类型形式参数.  
类型形式参数指定并命名一个占位符类型,紧挨着函数名后的一对尖括号中(`<T>`).

另一种常见的类型形式参数是`Dictionary<Key, Value>`,其中`Key`和`Value`都是用来标识占位符类型.

### 泛型类型

Swift还允许自定义泛型类型.

```Swift
// 定义泛型类型Stack,指定Element为类型形式参数,又称占位符类型名.
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
// 调用时传入String类型.
var stackOfStrings = Stack<String>()
```

对泛型类型进行扩展时,可以直接使用泛型类型的占位符类型名.

```Swift
extension Stack {
    // 可以直接使用原占位符类型Element.
    var topItem: Element? {
        return items.isEmpty ? nil : items[items.count - 1]
    }
}
```

### 类型约束

在一个类型形式参数名称后面放置一个类或者协议作为形式参数列表的一部分,并用冒号隔开以写一个类型约束.

```Swift
// 指定T的类型为SomeClass,U的类型为SomeProtocol
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here
}

// 使用T标识任意类型
func findIndex<T>(of valueToFind: T, in array:[T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

### 关联类型

关联类型是给**协议**中用到的类型占位符名称,通过`associatedtype`关键字指定.

```Swift
// 关联类型针对的是协议对象
protocol Container {
    // 使用associatedtype自定义占位符类型名称
    associatedtype ItemType
    mutating func append(_ item: ItemType)
    var count: Int { get }
    subscript(i: Int) -> ItemType { get }
}

struct IntStack: Container {
    var items = [Int]()
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
    // 把ItemType抽象类型转换为具体的Int类型
    typealias ItemType = Int
    mutating func append(_ item: Int) {
        self.push(item)
    }
    // 重写getter方法
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

### 泛型下标

泛型Where分句以where关键字开头,写在一个类型或函数体的左半个大括号前面,后接关联类型的约束或类型和关联类型一致的关系.  
泛型where分句还可以用在扩展中,关联类型中.

```Swift
// 自定义Container为泛型形式参数名
// 传入两个参数C1和C2
// 使用泛型where语句限制C1的ItemType必须和C2的ItemType相同,且C1的ItemType必须遵循Equatable协议
func allItemsMatch<C1: Container, C2: Container>
    (_ someContainer: C1, _ anotherContainer: C2) -> Bool
    where C1.ItemType == C2.ItemType, C1.ItemType: Equatable {
    return false
}
```

下标也可以是泛型,可以包括泛型`where`分句.

```Swift
extension Container {
    // 在下标操作中使用泛型where语句
    subscript<Indices: Sequence>(indices: Indices) -> [Item]
        where Indices.Iterator.Element == Int {
            var result = [Item]()
            for index in indices {
                result.append(self[index])
            }
            return result
    }
}
```

## 访问控制

[Access Control 权限控制的黑与白](http://wiki.jikexueyuan.com/project/swift/chapter4/01_Access_Control.html)

[访问控制和protected](http://wiki.jikexueyuan.com/project/swift/chapter4/06_Access_Control_and_Protected.html)

`模块`是单一的代码分配单元,一个框架或者应用程序会作为独立的单元构建和发布并且可以使用Swift中的`import`关键字导入到另一个模块.  
`源文件`是一个模块中当个Swift源代码文件(`常指应用程序或者是框架中的单个文件`).

访问控制限制其他源文件和模块对你的代码的访问,允许你隐藏代码的实现细节,并指定一个偏好的接口让其他代码可以访问和使用.

### 访问级别

Swift中访问级别遵循的原则:实体不可以被更低(限制更多)访问级别的实体定义.

Swift中提供了五种不同的访问级别:
* `open`,`public`访问允许实体被定义模块中的任意源文件访问,同样支持另一个模块的源文件通过导入该定义模块来访问.(`常指框架的访问级别`)
* `internal`访问允许实体被定义模块中的任意源文件访问,但不能被模块外的任何源文件访问.此为默认访问级别.
* `fileprivate`访问将实体的使用限制于当前定义源文件中.
* `private`访问将实体的使用限制于封闭声明中.

> `open`访问和`public`访问:
> * `open`可以在其定义的模块中被继承,也可以在导入定义模块的其他模块中被继承.
> * `open`可以在其定义的模块子类中重写,也可以在导入其定义模块的任何模块重写.
> * `public`只能在其定义的模块中被继承和在模块的子类中重写.

### 各种类型的访问控制

可以在定义类型时,给类型指定访问级别.  
* 类别类型的访问控制级别也会影响成员的默认访问级别(属性,方法,初始化方法,下标).
* 函数类型的访问级别由函数成员类型和返回类型中的最严格访问级别决定.
* 枚举中的独立成员自动使用该枚举类型的访问级别.
* 子类的访问级别不能高于父类.
* `Setter`/`Getter`方法,初始化器,协议,扩展,泛型都可以设置访问级别.

## 高级运算符

在Swift中可以自由的定义中缀,前缀,后缀和赋值运算符,以及相应的优先级和结合性.

> Swift中算术运算符默认是**不会**溢出的.  
所有的溢出行为都会被系统捕捉并报告为错误.

### 位运算符

* 按位取反运算符(`~`):对一个数值的全部比特位进行取反.
* 按位与运算符(`&`):可以对两个数的比特位进行合并.
* 按位或运算符(`|`):可以对两个数的比特位进行比较,当两个数中任意一个数的对应为1时,新的数值对应位就为1.
* 按位异或运算符(`^`):可以对两个数的比特位进行比较,当两个数的对应位不一致时,新的数值对应位为1.
* 按位左移(`<<`)右移(`>>`)运算符:`逻辑位移`中按位移动运算可以简单理解为将原始数值乘以或除以2.`算术位移`指负数的位移运算.

### 溢出运算符

在默认情况下,当数值超出它的容量时就会产生溢出,Swift就会报出错误,而不是生成一个无效的数值.  
对数值溢出的常见处理有:溢出加法`&+`,溢出减法`&-`,溢出乘法`&*`.

数值溢出:数值上溢时,会从最大值变为最小值;数值下溢时,会从最小值变为最大值.

### 优先级和结合性

运算符都具有优先级,可以使用括号改变结合性达到想要的优先级.

### 运算符函数

在类和结构体中可以为现有的运算进行自定义实现,即`运算符重载`.

* 前缀后缀运算符:  
在声明运算符函数时在`func`关键字之后添加`prefix`/`postfix`修饰符.
* 复合运算符:  
将赋值运算符(`=`)和其它运算符进行结合.且当左侧参数的值在运算符函数中可能会改变时,需要将左侧参数设置为`inout`类型.
* 等价运算符:  
自定义类和结构体默认不实现等价运算符方法.在对自定义类型进行等价判断时需要手动实现此方法.
* 自定义运算符:  
使用`operator`关键字进行全局定义,同时还要加上`prefix`,`infix`或`postfix`修饰符等.

```Swift
// 自定义前缀运算符
prefix operator +++
// 自定义运算符的优先级
infix operator +-: AdditionPrecedence
```

## 语法结构

Swift中的`语法结构`描述了能够构成该语言的合法符号的字符序列.  
一个字符序列常由`标识符`,`关键字`,`标点符号`,`字面量`或`运算符`组成.

* 空白与注释  
`空白`常用于分隔源文件中的符号以及帮助区分运算符属于前缀还是后缀,其他情况下会被忽略.  
`注释`被编译器当做`空白`处理.

* 标识符  
常由大小写英文字母,下划线,Unicode字符等组成.  
闭包中的隐式参数名称`$0`,`$1`等都是标识符.

* 关键字和标点符号  
某些被保留的关键字/符号不允许作为标识符.

* 字面量  
字面量用来表示源码中某种特定类型的值.  
常见的字面量有数值字面量,字符串字面量,布尔值字面量,nil字面量等 .

* 运算符  
包括`基础运算符`,`高级运算符`和自定义运算符([`运算符函数`](#%E8%BF%90%E7%AE%97%E7%AC%A6%E5%87%BD%E6%95%B0)).

## 类型

Swift语言中的类型有`命名型类型`和`复合型类型`.

命名类型:指定义时可以指定类型名字,其包括类,结构体,枚举,协议等.

复合类型:指没有名字的类型,它由Swift系统定义.Swift中有两种复合类型,函数类型和元组类型.

类型注解:显式地指出指定一个变量或表达式的值类型.

类型标识符:引用命名型类型,还可以引用命名型或复合型类型的别名.

### 常见的几种类型

> Swift里面的类型分为两种:  
[值类型与引用类型](http://wiki.jikexueyuan.com/project/swift/chapter4/05_Value_and_Reference_Types.html)
> * 值类型:每个实例都保留了一分独有的数据拷贝(线程安全),一般以`struct`,`enum`或者`tuple`形式存在.
> * 引用类型:每个实例共享同一份数据来源(拷贝指针),一般以`class`的形式存在.

* 元组类型

只有当元组中元素个数大于等于2时才可以命名元组元素.

`Void`是空元组类型`()`的别名.

* 函数类型

函数类型表示一个函数,方法或闭包的类型,它由参数类型和返回值类型组成,中间用箭头(`->`)隔开.

函数类型可以使用`autoclosure`关键字自动将参数表达式改为闭包类型,表达式结果就是闭包返回值.  
可以拥有可变长参数作为参数类型中的最后一个参数.  
可以在参数类型前加`inout`指定参数读写类型.

* 数组类型

定义使用命名类型`Array[element]`或者`[类型]`.

* 字典类型

定义使用命名类型`Dictionary<Key, Value>`或者`[键类型 : 值类型]`.

* 可选类型

用后缀`?`代替命名类型`Optional<Wrapped>`.

`Optional<Wrapped>`是枚举值,有`none`和`some(Wrapped)`两个值.用来表示可能有值也可能没有值.

如果在声明或定义可选变量或属性时未指定初始值,它的值会自动赋为默认值`nil`.

* 隐式解析可选型类型

用后缀`!`代替命名类型`Optional<Wrapped>`来实现自动解包功能.

* 协议合成类型

指符合协议列表中每个指定协议的类型.协议合成类型可能会在类型注解和泛型参数中([协议](#%E5%8D%8F%E8%AE%AE)).

* 元类型

元类型是指类型的类型,包括有类类型,结构体类型,枚举类型和协议类型.  
协议类型使用`.Protocol`获取元类型,其它类型则通过`.Type`获取元类型.  
还可以使用`.self`表示元类型.

* 类型继承

用来指定一个命名类型继承自那个类([继承](#%E7%BB%A7%E6%89%BF))或遵循那些协议.

* 类型推断

允许省略代码中变量和表达式的类型或者部分类型([类型标注](#%E7%B1%BB%E5%9E%8B%E6%A0%87%E6%B3%A8)).

[造个类型不是梦-白话Swift类型创建(Bool类)](http://wiki.jikexueyuan.com/project/swift/chapter4/02_Type_Custom.html)

## 表达式

### 前缀/后缀表达式

前缀表达式由可选的前缀运算符和一个表达式组合而成.([基本运算符](#%E5%9F%BA%E6%9C%AC%E8%BF%90%E7%AE%97%E7%AC%A6),[高级运算符](#%E9%AB%98%E7%BA%A7%E8%BF%90%E7%AE%97%E7%AC%A6))

一个try表达式由一个`try`运算符和一个可抛出错误的表达式组成.

```Swift
// 如果表达式不能抛出错误,那么可选try表达式的值就是一个包含了表达式值的可选项.
try? expression
```

### 二元表达式

二元表达式由一个中缀二元运算符和两个表达式作为左实际参数和右实际参数.

`实际解析时,通常会按照运算符的优先级把表达式转换为树.`

### 三元条件运算符

三元条件运算符会基于条件的值来对两个给定值中的一个进行计算.

### 类型转换运算符

常见的有`is`运算符,`as`运算符,`as?`运算符和`as!`运算符.

### 字面量表达式

当作为函数或是方法的默认值时,特殊字面量的值取决于默认值表达式调用的时候.

|表达式|表示意义|
|:------:|:------|
|`#file`|所在的文件名|
|`#line`|所在的行数|
|`#column`|所在的列数|
|`#function`|所在的声明的名字|
|`#selector`|可以引用属性的setter,getter方法或者方法的选择器|
|`#keyPath`|可以访问Objective-C中引用属性的字符串,用来使用键值编码和键值观察|
|`[]`|数组字面量|
|`[:]`|字典字面量|

> 在Swift 4.0中`selector`的适配问题:
> 1. 确保工程的`Build Settings`中的`Swift 3 @objc inference`设置为`Default`.
> 2. 使用`#selector`参数指定实例方法时(不论该方法是否是`private`修饰)必须使用`@objc`修饰.

元组表达式:使用括号括起来用逗号分隔的表达式组成.

通配符表达式:可以在赋值时显示地忽略一个值,使用`_`关键字标记.

### Self表达式和父类表达式

self表达式用来明确当前类型或实例类型的显式引用(`self`).

父类表达式使类能够与它的父类互动.子类可以在它们的成员,下标和初始化器的实现中使用父类表达式,来使用父类的实现(`super`).

### 闭包表达式

闭包表达式主要用于创建闭包,也就是lambda或匿名函数.

闭包表达式可以进行相关省略:
* 闭包可以省略像是参数类型或者返回类型,或者两者都省略(此时`in`关键字也需要省略).
* 闭包可以省略形式参数名(此时使用$0,$1等代表形式参数).
* 闭包还可以只有一个表达式组成(此时表达式的值就是闭包的返回值).

更多参考:[闭包表达式](#%E9%97%AD%E5%8C%85%E8%A1%A8%E8%BE%BE%E5%BC%8F)

### 可选链表表达式和强制取值表达式

使用后缀运算符`?`会根据表达式形成可选链但是不会改变其值,  
使用后缀运算符`!`对可选项展开后返回非可选的相关类型,否则就是运行时错误.

## 语句

### 常见的几种语句

详见[控制流](#控制流)

### 编译器控制语句

Swift有两种编译器控制语句:`编译配置语句`和`线路控制语句`.

`编译配置语句`:编译配置语句可以根据一个或多个配置来有条件地编译代码.一个编译配置语句都以`#if`开始,`#endif`结束.

```Swift
#if 编译配置1
    如果编译配置1成立则执行这部分代码
#elseif 编译配置2
    如果编译配置2成立则执行这部分代码
#else
    如果编译配置均不成立则执行这部分代码
#endif
```

`行控制语句`:行控制语句可以为被编译的源代码指定行号和文件名,从而改变源代码的定位信息,以便进行分析和调试.

```Swift
#sourceLocation(file: 文件名 , line:行号)
#sourceLocation()
```

`可用性条件`:可用性条件可作为`if`,`while`,`guard`语句的条件,可以在运行时基于特定的平台参数来查询API的可用性.

```Swift
if #available(平台名称 版本, ..., *) {    
    如果 API 可用，则执行这部分语句    
} else {    
    如果 API 不可用，则执行这部分语句
}
// 表示此方法仅在iOS 11及其以后的系统可用
@available(iOS 11.0, *)
func tableView(_ tableView: UITableView, trailingSwipeActionsConfigurationForRowAt indexPath: IndexPath) -> UISwipeActionsConfiguration? {
}
```

## 声明

### 常见的声明关键词

|关键字字段|含义|备注|
|:-----:|:---|:---:|
|`import`|导入声明|
|`let`/`var`|常量声明/变量声明|
|`override`|重写标记|
|`static`|声明类型变量属性/类型方法|
|`typealias`|类型别名|
|`func`|函数声明|
|`enum`|枚举声明|
|`indirect`|标记对象可以被递归调用|
|`set`/`get`和`willSet`/`didSet`|计算型属性和存储型属性|
|`struct`/`class`/`protocol`/`extension`|结构体/类/协议/扩展声明|
|`init`/`deinit`|构造器/析构器初始化|
|`subscript`|下标声明|
|`operator`|运算符声明|
|`inout`/`_`/`...`|可以在方法体内部修改外部值的参数/显式忽略参数/可变参数.实际接收参数类型为序列.|特殊参数处理|
|`mutating`|在实例对象中修改相关值|
|`throws`/`catch`|抛出错误/捕捉错误|错误处理方法|
|`infix`/`prefix`/`postfix`|中缀/前缀/后缀|运算符声明|
|`dynamic`/`final`/`lazy`/`optional`/`required`|动态属性标记/类不能被继承,属性不能在子类中被重写/懒加载/属性方法等可选型标记/属性方法等必选标记|声明修饰符|
|`public`/`internal`/`private`|可以被同模块和导入声明的模块中访问/只能被同模块的代码访问/只能被所在源文件的代码访问|访问控制级别|

## 特性

符号`@`后跟特性的名称和特性接收的任何参数来指定一个特性.

```Swift
@ 特性名
@ 特性名（特性参数）
```

### 声明特性

声明属性只能应用于声明中.

* `available`表明声明的生命周期与特定的平台和操作系统版本有关.
* `unavailable`表明声明在指定的平台上是无效的.
* `introduced`表明指定平台是从哪一版本开始引用该声明.
* `deprecated`表示从指定平台从哪一个版本开始**弃用**该声明.
* `obsoleted`表示从指定平台从哪一个版本开始**废弃**该声明(声明废弃后就会从平台中移除,不再被使用).
* `message`用来提供文本信息.
* `renamed`用来提供文本信息,用以表示被重命名的声明的新名字.
* `objc`用来修饰可以在Objective-C中表示的声明.`nonobjc`反之.
* `testable`在导入允许测试的编译模块时,用于修饰`import`声明.使得允许访问被导入模块中任何标有`internal`访问级别的实体.
* `NSApplicationMain`该特性用于类中表示该类是应用程序的委托类.效果等同调用`NSApplicationMain(_:_:)`函数,并把该类类名作为为委托类类名传入函数.
* `UIApplicationMain`该特性用于类中表示该类是应用程序的委托类.效果等同调用`UIApplicationMain`函数,并把该类类名作为为委托类类名传入函数.
* `NSCopying`用于修饰一个存储型变量属性.该特性将使属性赋值时使用传入值的副本(`copyWithZone(_:)`函数).

`@objc`主要是处理OC和Swift混编时方法的调用以及属性获取问题.`Swift 4.0`将去掉了相关的隐式类型推断,因此需要手动来管理.

Interface Builder中的声明特性有:`IBAction`(修饰类的方法),`IBDesignable`(修饰类的声明),`IBOutlet`和`IBInspectable`(修饰类的属性声明).

### 类型特性

类型特性只能用于修饰类型.

* `autoclosure`将表达式自动封装成无参数的闭包来延迟表达式的计算([自动闭包](#自动闭包)).
* `convention`用于修饰函数类型,指出函数调用的约定.
* `escaping`在函数或者方法声明上使用该属性,表示参数不会被存储以供延迟调用.确保了参数不会超出函数调用的生命周期.([逃逸闭包](#逃逸闭包))

## 模式

模式是代表单个值或者复合值的结构.

Swift下的模式分为两类:  
* 第一种,能够成功匹配任何类型的值.常用于解构简单变量,常量和可选绑定中的值.此类模式包括常用的`通配符模式`,`标识符模式`以及包含前两种模式的`值绑定模式`和`元组模式`.
* 另一种在运行时匹配某个特定值时可能会失败.用于全模式匹配来检验匹配的值在运行时是否存在.此类模式包括`枚举用例模式`,`可选模式`,`表达式模式`和`类型转换模式`.

### 通配符模式

使用通配符表达式`_`来忽略任何值.

### 标识符模式

标识符模式匹配任何值,并将匹配的值和一个变量或常量绑定起来.

### 值绑定模式

值绑定模式把匹配到的值绑定给一个变量(`var`)或常量(`let`).

### 元组模式

元组模式是由逗号分隔的,具有零个或多个模式的列表,并由一对圆括号括起来.  
可以使用[类型标注](#类型标注)来限制元组能够匹配到那种元组类型.

### 枚举用例模式

枚举用例模式匹配现有的某个枚举类型的某个用例.

### 可选模式

可选模式由一个标识符模式和紧随其后的一个问号组成.

### 表达式模式

表达式模式代表表达式的值.表达式模式只出现在switch语句中的case标签中.

### 类型转换模式

类型转换有两种类型转换模式,is模式和as模式.

```Swift
is 类型
模式 as 类型
```

## Swift 使用 Tips

### Swift 中的良好编程风格

- API 命名要清晰
- 尽量使用类型推断来提高代码的可读性，在存在歧义或者进行定义时不要使用类型推断（比如 func 需要显式的指定返回类型）
- 优先使用结构体，只在确实需要使用到类特性或者引用语义时才使用类
- 在设计的类不需要被继承时，将他们标记为 final
- 尽量使用尾随闭包，除非闭包后立即跟随左括号
- 使用 guard 来提早退出方法
- 避免对可选值进行强制解包和隐式强制解包
- 建议使用 let 来声明不可改变的变量，而使用函数将可变的部分封装，来隔离可变变量的副作用
- 尽量使用类型和协议的扩展来替代全局函数

### Swift 中的宏定义

由于命名空间的缘故，Swift 中是不能使用宏定义的。但是可以使用其他方法达到宏定义的目的。

* 没有参数的宏定义

  将不需要参数的宏定义为 let 常量。

* 接收参数的宏定义

  将需要参数的宏定义为函数。

```swift
// 使用let常量定义无参数的宏定义
let kScreenHeight = UIScreen.main.bounds.height
let kScreenWidth = UIScreen.main.bounds.width

// 使用函数定义有参数的宏定义
func KRGBColor(_ red:CGFloat, green:CGFloat, blue:CGFloat) -> UIColor {
    return UIColor.init(red:red , green: green, blue: blue, alpha: 1.0)
}
func KRandomColor() -> UIColor {
    return KRGBColor(CGFloat(Double(exactly: arc4random_uniform(256))!/255.0),
                     green: CGFloat(Double(exactly: arc4random_uniform(256))!/255.0),
                     blue: CGFloat(Double(exactly: arc4random_uniform(256))!/255.0))
}
```

参考资料:[swift中的宏定义](http://www.jianshu.com/p/5f5f7c4e1dc0)

### NSRange 和 Range 的互转

```swift
// Swift 4.0

// NSRange -> Range
let range = Range(nsrange, in: str)

// Range -> NSRange
let nsrange = NSRange(range!, in: str)

// Swift 3.0
extension String {
    func toNSRange(_ range: Range<String.Index>) -> NSRange {
        guard let from = range.lowerBound.samePosition(in: utf16), let to = range.upperBound.samePosition(in: utf16) else {
            return NSMakeRange(0, 0)
        }
        return NSMakeRange(utf16.distance(from: utf16.startIndex, to: from), utf16.distance(from: from, to: to))
    }
    func toRange(_ range: NSRange) -> Range<String.Index>? {
        guard let from16 = utf16.index(utf16.startIndex, offsetBy: range.location, limitedBy: utf16.endIndex) else {
            return nil
        }
        guard let to16 = utf16.index(from16, offsetBy: range.length, limitedBy: utf16.endIndex) else {
            return nil
        }
        guard let from = String.Index(from16, within: self) else {
            return nil
        }
        guard let to = String.Index(to16, within: self) else {
            return nil
        }
        return from ..< to
    }
}
```

[Methods to convert between Swift string ranges (Range<String.Index>) and NSString ranges (NSRange)](https://stackoverflow.com/questions/25138339/nsrange-to-rangestring-index/30404532#30404532)

### `substring` 方法/求子串的使用

```swift
// modelString.substring(with: range)
// 'substring(with:)' is deprecated: Please use String slicing subscript.

// Substring
let newStr = str[..<index]
// String
let newStr = String(str[..<index])
```

[How can I use String slicing subscripts in Swift 4?](https://stackoverflow.com/a/45562735/9147670)

## Swift和Objective-C对比

### 两种语言的区别

// TODO: 区别

### 两种语言的混编

* 在工程中尝试混编时,XCode会提示创建`${ProductModuleName}-Bridging-Header.h`文件.  
可以在bridge文件中添加希望在Swift代码中使用的OC代码头文件.此后在Swift文件中使用时不再需要导入.
> 自定义bridge文件时需要在`Build Setting -> Swift Compiler - Objective-C Bridging Header`选项中指定文件路径.
* OC代码中使用Swift代码时直接导入`${ProductModuleName}-Swift.h`文件或者使用`@import ${ProductModuleName};`即可.  
项目工程中的所有Swift头文件都可以通过此文件导入,且该文件是在项目中出现Swift文件时自动生成.
> OC代码中导入该文件时,必须是在同一个module中.  
可以使用`#import <XXXSDK/XXXSDK-Swift.h>`来避免出现错误.

* 在需要支持混编的Swift类前最好使用`@objc`明确标记,所声明的类尽量继承自`NSObject`及其子类.

参考资料:

[Objective-C Mix Swift Configuration：混编设置](https://www.jianshu.com/p/bc47287f2c30)

[Swift与C语言指针友好合作](http://wiki.jikexueyuan.com/project/swift/chapter4/04_Interacting_with_C_Pointers.html)

[The Swift Programming Language 中文版(Swift 3.0)](http://wiki.jikexueyuan.com/project/swift/)

[Swift 编程语言(Swift 4.0)](https://www.cnswift.org/about-swift)

---

[⬆️ 回到顶部 ⬆️](#Swift初窥)