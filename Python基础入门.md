# Python基础入门

[⬅️ Back](./)

<!-- TOC -->

- [Python基础入门](#python基础入门)
    - [Python语言的基本特点](#python语言的基本特点)
        - [环境相关](#环境相关)
        - [内存相关](#内存相关)
        - [数据存储](#数据存储)
            - [序列化](#序列化)
            - [JSON](#json)
    - [数据结构](#数据结构)
        - [字符串](#字符串)
            - [字符串的常见操作](#字符串的常见操作)
            - [字符串的格式化](#字符串的格式化)
            - [正则表达式的使用](#正则表达式的使用)
        - [列表](#列表)
            - [列表的常见操作](#列表的常见操作)
            - [列表解析](#列表解析)
            - [列表的切片操作](#列表的切片操作)
        - [元组](#元组)
        - [字典](#字典)
        - [集合](#集合)
        - [枚举类型](#枚举类型)
    - [运算符](#运算符)
    - [控制流](#控制流)
        - [条件语句](#条件语句)
        - [循环](#循环)
            - [`for-in`循环](#for-in循环)
            - [`range`函数](#range函数)
    - [输入输出](#输入输出)
    - [函数](#函数)
        - [函数的定义](#函数的定义)
        - [匿名函数](#匿名函数)
        - [递归函数和尾递归函数](#递归函数和尾递归函数)
        - [高阶函数](#高阶函数)
            - [map/reduce 函数](#mapreduce-函数)
            - [filter 函数](#filter-函数)
            - [sorted 函数](#sorted-函数)
        - [闭包](#闭包)
        - [装饰器](#装饰器)
        - [偏函数](#偏函数)
        - [迭代器和生成器](#迭代器和生成器)
            - [迭代器](#迭代器)
            - [生成器](#生成器)
        - [协程](#协程)
        - [变量作用域](#变量作用域)
        - [模块](#模块)
    - [类](#类)
        - [类的定义](#类的定义)
        - [访问控制](#访问控制)
        - [类的继承](#类的继承)
        - [类的多态和封装](#类的多态和封装)
            - [多态](#多态)
            - [封装和私有化](#封装和私有化)
        - [对象信息的获取](#对象信息的获取)
        - [特殊方法](#特殊方法)
        - [类的导入](#类的导入)
    - [进程和线程](#进程和线程)
        - [进程](#进程)
            - [子进程](#子进程)
            - [进程池](#进程池)
            - [进程同步](#进程同步)
        - [线程](#线程)
            - [线程锁](#线程锁)
            - [ThreadLocal](#threadlocal)
    - [文件和异常](#文件和异常)
    - [异常处理](#异常处理)
        - [异常捕捉](#异常捕捉)
        - [异常抛出](#异常抛出)
        - [清理行为](#清理行为)
        - [代码调试](#代码调试)
            - [断言](#断言)
            - [错误记录](#错误记录)
            - [单元测试](#单元测试)
    - [数据可视化](#数据可视化)
        - [matplotlib 图表](#matplotlib-图表)
            - [使用`plot()`绘制折线图](#使用plot绘制折线图)
            - [使用`scatter()`绘制散点图](#使用scatter绘制散点图)

<!-- /TOC -->

## Python语言的基本特点

* 解释性、面向对象、具有动态语义（动态类型、动态绑定）

  使用变量类型时，不需要指定变量数据类型。

  Python 程序中用到的所有东西（甚至包括函数）都叫`对象`。  
  每一个对象都具有一个标识，一个类型和一个值.。 
  通过`头部信息`明确具体类型，头信息由`引用计数`和`类型指针`组成。 
  `is`用来比较两个对象的身份，`id`可以获得整数型对象标示。

* Python 具有模块和包的概念，支持程序的模块化和代码重用

* 不需要编译和链接、不需要变量和参数说明，语句的分组采用缩进方式

> Python 期望一个`物理行`就是一个`逻辑行`。否则就需要在一行中使用`;`进行逻辑分割。  
行首的空白缩进（空格和制表符）在语法上代表`逻辑行`的缩进层次。

### 环境相关

直接运行py 文件：

* 使用命令行`python3 hello.py`
* 首先，在`.py`文件前加上一行特殊的注释： `#!/usr/bin/env python3`  
其次，通过命令给文件赋予权限`chmod a+x hello.py`

使用`type -a python3`查看python3路径，进而可以在相关编辑器中设置语言环境路径。

> 在文件第一行使用`# -*- coding: <encoding-name> -*- `表示文件编码格式。(Python 脚本能够匹配正则表达式`coding[=:]\s*([-\w.]+)`)

使用`os`模块可以查询相关环境配置信息：

```python
import os

# 操作系统类型
os.name
# 详细系统信息
os.uname()
# 环境变量
os.environ
# 获取某个环境变量的值
os.environ.get('key')

# 查看当前目录的绝对路径
os.path.abspath('.')
# 目录拼接
os.path.join('/Users/michael', 'testdir')
# 目录路径拆分
os.path.split()
# 创建目录
os.mkdir('/Users/michael/testdir')
# 删除目录
os.rmdir('/Users/michael/testdir')
# 获取目录中符合条件的文件
os.listdir()
# 判断路径是否为文件夹
os.path.isdir()
# 判断路径是否为文件
os.path.isfile()

# 获取文件扩展名
os.path.splitext()
# 文件重命名
os.rename()
# 文件删除
os.remove()
```

### 内存相关

Python 语言使用`内存池`来减少操作系统内存分配和回收操作。  
小于256字节的对象，直接从内存池中获取存储空间。  
大于256字节的对象，直接用 malloc 在`堆`上分配内存。

对象是使用`指针`进行引用的传递，所以 Python 中的对象都是存储在`堆`上（Python 中没有`值类型`和`引用类型`之分）。

Python 语言含有`引用计数`和`GC垃圾回收机制`两种内存管理模式。

当将对象赋值给一个新的变量时，这个变量只是`参考`对象的指针，而不是对象本身。  
变量名指向计算机中存储对象内存的操作，被称为名称到对象的`绑定`。

> 可以使用`sys.getsizeof()`获取对象的内存占用。

### 数据存储

####序列化

Python 中可以使用`pickle`模块实现序列化。

* 序列化（pickling）：把变量从内存中变为可存储或可传输的过程。
* 反序列化（unpickling）：把变量内容从序列化的对象重新读取到内存中的过程。

`pickle.dumps()`方法把任意对象序列化成一个`bytes`，然后，就可以把这个`bytes`写入文件。  
`pickle.dump()`方法直接把对象序列化后写入一个file-like Object。  

用`pickle.loads()`方法反序列化出对象。  
用`pickle.load()`方法从一个`file-like Object`中直接反序列化出对象。

#### JSON

Python 中的`json`模块提供了对象到 JSON 数据的转换。

| 方法  | 意义                                       |
| ----- | ------------------------------------------ |
| dump  | 将 Python 对象按照 JSON 格式序列化到文件中 |
| dumps | 将 Python 对象处理成 JSON 格式的字符串     |
| load  | 将文件中的 JSON 数据反序列化成对象         |
| loads | 将字符串的内容反序列化成 Python 对象       |

JSON 对象和`Class`对象之间互转需要做特殊处理：

```python
import json

# 转换函数
def student2dict(std):
    return {
        'name': std.name,
        'age': std.age,
        'score': std.score
    }
# 将对象转换为 JSON
# 可选参数 default 传入转换规则
print(json.dumps(s, default=student2dict))
print(json.dumps(s, default=lambda obj: obj.__dict__))

# 从 JSON 对象中获取字典数据
def dict2student(d):
    return Student(d['name'], d['age'], d['score'])
json_str = '{"age": 20, "score": 88, "name": "Bob"}'
# 可选参数 object_hook 传入解析规则
print(json.loads(json_str, object_hook=dict2student))
```

## 数据结构

在文件和文件夹的命名中，最好使用小写字母，并使用下划线来表示空格。

### 字符串

#### 字符串的常见操作

| 方法名     | 意义       |
| --------- | ---------- |
| `title()` | 首字母大写 |
| `upper()` | 所有字母都大写 |
| `lower()` | 所有字母都小写 |
| `rstrip()` | 删除右侧空格 |
| `lstrip()` | 删除左侧空格 |
| `strip()` | 删除两端空格 |
| `ljust()`/`rjust()` | 字符串左/右对齐 |
| `split()` | 以空格为分隔符将字符串进行拆分，并返回列表 |
| `zfill()` | 在数字的左边填充0 |
| `find()` | 查找子串的位置 |
| `startsWith()`、`endsWith()` | 检查字符串是否以指定字符串开头、结尾 |
| `isdigit()`、`isalpha()`、`isalnum()` | 检查字符串是否由数字、字母、数字和字母构成 |

#### 字符串的格式化

使用`format()`函数对字符串格式化显示。

使用`{}`做占位符，其内可：
* 使用位置/关键字指定对应的参数。
* 使用`!a`（使用`ascii()`）、`!s`（使用`str()`）、`!r`（使用`repr()`）在格式化某值前将其转换。
* 可选项`:`后可跟格式化标识。

```python
for x in range(1, 11):
    # ：后跟数字表示该字符串宽度
	print("{0:3}   {1: 3d}   {2: 4d}".format(x, x*x, x*x*x))

#   1     1      1
#   2     4      8
#   3     9     27
#   4    16     64
#   5    25    125
#   6    36    216
#   7    49    343
#   8    64    512
#   9    81    729
#  10    100    1000


table = {"Google": 1, "Runoob": 2, "Taobao": 3}
# 使用0[] 访问对应的键值
print("Runoob:{0[Runoob]:d};Google:{0[Google]:d};Taobao:{0[Taobao]:d}".format(table))
print("Runoob:{Runoob:d};Google:{Google:d};Taobao:{Taobao:d}".format(**table))

# Runoob:2;Google:1;Taobao:3
# Runoob:2;Google:1;Taobao:3
```

~~还可以使用旧式字符串格式化工具。~~

```python
print("pi=%.10f" % math.pi)
# pi=3.1415926536
```

使用单引号/双引号(`''`/`" "`)表示其间的字符串。

使用三引号(`''' '''`)表示其间的多行字符串。

还可以使用`+`运算符进行行连接，使用`*`运算符进行重复连接。

在字符串前加前缀`r`/`R`表示该字符串中的转义字符等特别处理不可用。该字符串被称为`自然字符串`。  
在字符串前加前缀`u`/`U`表示该字符串是 Unicode 文本。

#### 正则表达式的使用

Python 提供`re`模块，包含了所有正则表达式的功能。

> 在设置正则表达式字符串时，建议使用 `r` 前缀修饰表示原始字符串。这样就不需要进行字符的转义。


**函数速查表：**

| 函数                                         | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| compile(pattern, flags=0)                    | 编译正则表达式返回正则表达式对象。                           |
| match(pattern, string, flags=0)              | 用正则表达式匹配字符串。成功返回匹配对象，否则返回 None。    |
| search(pattern, string, flags=0)             | 搜索字符串中第一次出现正则表达式的模式。成功返回匹配对象，否则返回 None。 |
| split(pattern, string, maxsplit=0, flags=0)  | 用正则表达式指定的模式分隔符拆分字符串，返回列表。           |
| sub(pattern, repl, string, count=0, flags=0) | 用指定的字符串替换原字符串中与正则表达式匹配的模式，可以用 count 指定替换的次数。 |
| fullmatch(pattern, string, flags=0)          | match 函数的完全匹配（从字符串开头到结尾）版本。             |
| findall(pattern, string, flags=0)            | 查找字符串所有与正则表达式匹配的模式，返回字符串的列表。     |
| finditer(pattern, string, flags=0)           | 查找字符串所有与正则表达式匹配的模式，返回一个迭代器。       |
| purge()                                      | 清除隐式编译的正则表达式的缓存。                             |

参考资料：

- [正则表达式在Python中的应用](https://quxiaolei.github.io/%E5%B8%B8%E8%A7%81%E7%9A%84%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%8F%8A%E5%85%B6%E5%BA%94%E7%94%A8.html#%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%9C%A8python%E4%B8%AD%E7%9A%84%E5%BA%94%E7%94%A8)
- [6.2. re — Regular expression operations — Python 3.6.6rc1 documentation](https://docs.python.org/3.6/library/re.html#module-contents)

### 列表

列表是**有序**集合，使用方括号`[]`表示列表，并用逗号来分割其中的元素。

1. 列表对象和存储元素指针的数组是分开的两块内存，存储元素指针的数组是在`堆`上分配的。
2. 列表是`可变类型`，会动态的调整指针数组大小。预分配的内存大小大于实际元素数量。
3. 列表中元素的数据类型可以不同。

#### 列表的常见操作

* 取值

  Python 支持`负数索引`，`-1`表示列表最后一个元素。

* 添加值

  支持使用`append()`在列表末尾，使用`insert()`在列表任意位置添加元素，使用`extend()`在列表尾部追加新列表。

* 删除元素

  使用`del`语句，`pop()`和`remove()`删除列表元素。

  |                      | `del`语句 | `pop()`函数 | `remove()`函数 |
  | :------------------- | --------- | ----------- | -------------- |
  | 删除时是否返回该值   | ×         | √           | √              |
  | 是否支持删除任意位置 | √         | √           | ×              |
  | 是否支持删除某元素值 | ×         | ×           | √              |

  >`pop()`函数默认删除列表末尾的元素。  
可以在括号中指定要删除元素的索引值。

* 列表元素排序

  * 列表元素的永久排序

    永久排序使用`sort()`函数。反向排序时使用`sort(reverse=True)`即可。

  * 列表元素的临时排序

    临时排序使用`sorted()`函数。方向排序同样设置`reverse=True`即可。

  * 列表元素的反向打印

    使用`reverse()`函数反转列表元素的排列顺序。同时，此操作会改变原始列表。

* 其他常见命令

  | 函数                    | 意义                                               |
  | ----------------------- | -------------------------------------------------- |
  | `len()`                 | 返回列表的长度                                     |
  | `count()`               | 统计某元素在列表中出现的次数                       |
  | `extend()`              | 在列表某追加另一列表元素                           |
  | `max()`/`min()`/`sum()` | 列表元素最大值<br />列表元素最小值<br />列表元素和 |
  | `index()`               | 返回某元素在列表中的索引值                         |
  | `clear()`/`copy()`      | 清除列表<br />复制列表                             |

#### 列表解析

列表解析是将 for 循环和创建新元素的代码合并为一行，并自动附加新元素。

每个列表推导式都在 for 之后跟一个表达式，然后有零到多个 for 或 if 子句。

```python
# 生成简单的列表
squares = [value ** 2 for value in range(1, 4)]
# 简单的生成器
# (value ** 2 for value in range(1, 4))
print(squares)
# [1, 4, 9]

# 在 for 之后跟 if 子句
threeNums = [3*x for x in range(1, 6) if x > 3]
print("threeNums：", threeNums)
# threeNums： [12, 15]

# 在 for 之后跟多个 for 或 if 子句
sumOfThreeNums = [x*y for x in range(1, 6) if x > 3 for y in range(1, 6)]
print("sumOfThreeNums：", sumOfThreeNums)
# 多个 for 循环生成全排列
# sumOfThreeNums： [4, 8, 12, 16, 20, 5, 10, 15, 20, 25]
```

> 列表和生成器的主要区别：
>
> 列表使用时需要将列表内容一次性读入内存中。  
迭代器（[生成器](#生成器)是迭代器）的优势就在于少占内存，无需将生成器实例化就可以直接对其操作。

#### 列表的切片操作

使用`range()`函数来生成一系列的数字，可以使用`list()`函数将其转换为一个列表。  
另外`range()`函数使用时可以支持指定步长。

```python
# 第一个参数表示切片开始的位置，第二个参数表示切片到指定位置前结束。第三个参数表示步长。
even_numbers = list(range(1,20,2))
print(even_numbers)
# [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

使用`range()`函数可以输出从指定位置到列表末尾的所有元素。  
在对进行列表的切片操作时，默认是从列表开头进行提取。  
可以使用`[:]`复制整个列表。

```python
players = ["charles", "martina", "michael", "florence", "eli"]
print(players[0:3])
print(players[:4])
print(players[2:])
# 逆序输出元素
print(players[-3:])

new_players = players[:]
new_players.append("张三")
print(players)
print(new_players)
# ['charles', 'martina', 'michael']
# ['charles', 'martina', 'michael', 'florence']
# ['michael', 'florence', 'eli']
# ['michael', 'florence', 'eli']
# ['charles', 'martina', 'michael', 'florence', 'eli']
# ['charles', 'martina', 'michael', 'florence', 'eli', '张三']
```

### 元组

元组和列表类似，是**不可变**的列表。用`()`来表示，其他操作同列表。

> 元组在创建时间和内存的复用上更高效，类似于列表的**只读**版本。

可以使用`tuple()`函数将列表转换为元组。  
可以使用`list()`方法，将元组转换为列表。

| 列表     | 元组         | 字典                 |
| -------- | ------------ | -------------------- |
| 有序集合 | 不可变的列表 | 由一系列的键值对组成 |
| `[]`     | `()`         | `{}`                 |
| 可变     | 不可变       | 可变                 |

### 字典

字典另外一种可变类型，由一系列的键值对组成。用`{}`来表示。

字典采用`开放地址法的哈希表`实现。

* 元素超出自带容量后，才会到`堆`上额外分配元素内存。
* 虚拟机会缓存字典复用对象，但是在`堆`上分配的元素内存会被释放。
* 按需动态调整容量，扩容或者收缩都会重新分配内存，重新哈希。
* 删除元素*不会*立即回收内存。

字典的常见操作：
* 可以使用`del`语句删除相应的键值对。
* 使用`items()`函数返回字典的**键值对**列表。
* 使用`keys()`函数返回字典的**键值**列表。
* 使用`values()`函数返回字典的**值**列表。
* 可以使用`zip()`组合同时遍历多个序列。

```python
dict = {"key1":"value1","key2":"value2"}
for key, value in dict.items():
    print("key:" + key + ",value:" + value)
# key:key1,value:value1
# key:key2,value:value2
```

### 集合

集合用来存储**无序**不重复对象，可以使用`set()`剔除字典中的重复项。

集合中只能存储可哈希对象。
> 自定义对象时需要保证 hash 和 equal 方法都成立。

集合支持集合间的运算。

### 枚举类型

`Enum`可以把一组相关常量定义在一个不可变的 class 中，且成员可以直接比较。

在枚举类型中每个常量都是类的唯一实例。常见的实现方式：

```python
# 导入enum相关支持
from enum import Enum, unique

# @unique 装饰器可以帮助检查保证没有重复值
@unique
# 自定义对象继承自Enum
class Weekday(Enum):
    Sun = 0 # Sun的value被设定为0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5
    Sat = 6
    
day1 = Weekday.Mon
print(day1)
print(Weekday['Tue'])
print(Weekday.Tue.value)
print(Weekday(1))
# Weekday.Mon
# Weekday.Tue
# 2
# Weekday.Mon
```

`@unique`装饰器可以帮助我们检查保证没有重复值。

## 运算符

* `**`：幂运算，返回x的y次幂。（`3 ** 4 = 81`）
* `//`：取整除，返回商的整数部分。(`4 // 3.0 = 1.0`)
* `<<`/`>>`：左移/右移运算符。（`2 << 2 = 8,2的二进制表示为10.   11 >> 1 = 5,11的二进制表示为1011.`)
* Python 中用`\t`表示制表位，用`%s`将任意类型转为字符串，用`None`表示一个特殊的空值。

## 控制流

### 条件语句

使用`if`、`elif`和`else`进行条件判断。需要在相应的语句后紧跟`:`来连接下一个语句块。

`and`：且运算符

`or`：与运算符

`in`/`not in`：判断元素是否在列表中

```python
if age > 18:
    # Do SomeThing
elif age > 6:
    # DO SomeThing
else:
    # DO SomeThing
```

### 循环

#### `for-in`循环

进行循环操作时，可以使用`enumerate()`函数获取索引和对应值。

遍历多个序列时，可以使用`zip()`进行打包操作。

* `break`语句提前退出循环。
* `continue`语句跳出此次循环，直接开始下次循环。
* `pass`语句用来表示空代码块。

> **Python 中的循环不包含域的概念。**
>
> 当循环结束后，循环体中的临时变量不会被销毁，而是继续存在于当前执行环境中。  
> 而且，Python 的函数只有在执行时才会去找函数体中变量的值（类比懒加载）。

```python
flist = []
# 遍历完成后 i = 2
for i in range(3):
    def foo(x):
        print("foo:", x+i)
    flist.append(foo)

for f in flist:
    # 在执行时 i = 2
    f(2)

# foo: 4
# foo: 4
# foo: 4
```

#### `range`函数

`range()`函数可以用来产生一个不变的数值序列，还可以生成指定步长的序列。

```Python
# 使用list()将一系列数字转换为列表
even_numbers = list(range(1,20,2))
print(even_numbers)
# [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

> 1. 注意语句的缩进
> 2. 可以使用`pass`表示占位空语句代码

## 输入输出

`input()`函数允许用户进行输入操作。  
该函数可以接受一个参数来向用户显示提示或者说明。

```python
# 使用 input 函数获取输入内容
name = input("what is your name?")
ageString = input("pls input your age？")
age = int(ageString)

# 使用"r"表示输入原始字符串
print(r"test for no 括\n号",1.01+1,1<2)
print('''1.this is mutable
2.line
3.哈哈
''')
print("this one line \
string")
# test for no 括\n号 2.01 True
# 1.this is mutable
# 2.line
# 3.哈哈
# this one line string
```

> 1. 使用`r`表示输出原始字符串
> 2. 使用`'''`表示输出多行字符串
> 3. 使用`\`连接一行字符串

## 函数

### 函数的定义

使用关键字`def`来表示要定义函数，依次写出函数名、括号、括号中的参数和冒号。

> 可以使用`global`字段定义全局变量（允许在当前作用域外使用该变量）。

函数支持对参数个数的校验，但是不支持对参数类型的校验。

函数中参数的顺序为：`必选参数`、`默认参数`（`默认参数值`必须是不可变对象）、`可变参数`（`*`）、`命名关键字参数`和`关键字参数`（`**`）。

* 默认参数

  默认参数值必须是**不可变对象**。

* **可变参数**

  可变参数允许传入0个或任意个参数，定义时在参数名前加`*`号。在函数调用时会将参数自动封装为一个 tuple。

* 命名参数

  直接指定参数名传入参数值时，可以不按照参数命名顺序设置参数值。

* 命名关键字参数

  命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

* **关键字参数**

  使用`**`字段标识为关键字参数。关键字参数允传入0个或任意个含参数名的参数，关键字参数在函数内部自动组装为一个 dict。

```python
# 设置形参b默认值为"0"
def add(a , b="0"):
    # 使用三对双引号括起表示文档字符串
    """加法"""
    return int(a) + int(b)
# 使用位置实参
c = add("1", "12")
# 使用关键字实参
c = add(b="1", a="12")
# c = add("1")
print(c)
# 13

# * 号分割命名关键字参数
def person(name, age, *, city, job):
    print(name, age, city, job)
# 传入0个或者任意个含参数名的参数
person('Jack', 24, city='Beijing', job='Engineer')
```

使用`*`表示**空元组**接收**可变参数**。  
使用`**`表示**空字典**接收**关键字参数**。

```python
# toppings为空的元组，接受可变参数
def make_pizza(*toppings):
    """制作pizza需要的材料,显示为可变参数"""
    print(toppings)

# 传入0个或多个参数值
make_pizza("1")
make_pizza("1", "2", "3")
# ('1',)
# ('1', '2', '3')

# user_info为空的字典，接受可变个数的关键字参数
def build_profile(filename, **user_info):
    """创建用户信息文件,传入可变个数的字典"""
    print(filename)
    for key, value in user_info.items():
        print(key + ":" + value)

# 传入0个或者任意个含参数名的参数
build_profile("userinfo", username = "张三", age = "22")
# userinfo
# username:张三
# age:22
```

### 匿名函数

Python 使用`lambda`来创建匿名函数。

`lambda [arg1 [,arg2,.....argn]]:expression`

> lambda 后面直接跟变量；  
变量后面是冒号；  
冒号后面是表达式（有且仅有一个），表达式计算结果就是本函数的返回值。

* lambda 只是一个表达式，函数体比 def 定义简单。
* lambda 的主体是一个表达式，而不是一个代码块。因此，只能在表达式中封装有限的逻辑。
* lambda 函数有自己的命名空间，且不能访问自己参数列表之外/全局命名空间里的参数。
* lambda 函数带来的是代码的简洁，并没有给程序带来性能上的提升。

  > C 或 C++ 的内联函数调用小函数时不占用栈内存，从而使得运行效率得到提高。

```python
sum = lambda a, b: a+b
print(sum(10, 20))
print(sum(20, 20))
# 30
# 40

list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
# [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### 递归函数和尾递归函数

`递归函数`是在函数内部调用该函数本身，缺点是可能会出现**栈溢出**的 bug。

> 函数调用是通过数据结构——栈来实现的。每当进入一个函数调用/返回，栈就会增加/减少一层。

`尾递归函数`<u>指在函数返回时调用自身，并且 return 语句不能包含表达式</u>。编译器或解释器做尾递归优化后，使递归函数不论调用多少次都只占用一个栈帧，不会出现栈溢出现象。

```python
def fact(n):
    if n == 1:
        return 1
    else:
        # return 语句是表达式
        # 在函数内部调用该函数本身
        return fact(n-1) * n
print fact(5)

# 使用尾递归函数,避免出现栈溢出现象
def newFact(n,product):
    if n == 1:
        return product
    else:
        # return 语句中调用该函数本身
        # 在调用函数前进行计算,不影响函数的调用
        return newFact(n - 1, n * product)
print newFact(5,1)
# 120
# 120
```

### 高阶函数

一个函数可以接受另一个函数作为参数，这种函数就叫做**高阶函数**。

#### map/reduce 函数

* `map()`函数

  `map()`函数接收两个参数，一个是函数，一个是可遍历的序列。  
  `map()`函数将传入的函数依次作用于序列的每个元素并把结果作为新的序列返回。

* `reduce()`函数

  `reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数。  
  `reduce`把当前结果继续和序列的下一个元素做累积计算，最终返回计算结果。

#### filter 函数

`filter()`也接收一个函数和一个序列，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。

```python
# <filter object at 0x10b2bb0f0>
filterObject = filter(lambda str : str.endswith(".py"), list)
for item in filterObject:
    print(item)
```

#### sorted 函数

Python 内置的`sorted()`函数可以直接对 list 进行排序，它还可以接收一个`key`函数来实现自定义的排序。

```python
# 按照绝对值的大小进行排序
# 使用 reverse 进行反向排序
sorted([36, 5, -12, 9, -21], key=abs, reverse=True)
```

### 闭包

在函数中可以嵌套（定义）另一个函数，如果内部函数引用了外部函数变量，并且外部函数的返回值含有内部函数的引用，则就产生了闭包。

> 一般情况下，当一个函数结束后函数内部的所有资源都会被释放，局部变量会消失。
>
> 但是，闭包是一种特殊情况：外部函数在结束时发现自己的临时变量还被内部函数使用。

Python 语言中形成闭包的条件：

* 函数间的嵌套：必须有一个内嵌函数（在函数内定义的函数）；
* 内部函数引用外部变量：内嵌函数必须引用一个定义在闭包范围外（外部函数）的变量；
* 必须返回内部函数：外部函数必须返回内嵌（内部）函数。

> 返回函数不要引用任何循环变量，或者后续会发生变化的变量。

```python
def outer(x):
    # 内部函数
    def inner(y):
        # 引用外部变量
        return x + y
    # 返回内部函数
    return inner

def count():
    fs = []
    for i in range(1, 4):
        # 内部函数
        def f():
             # 返回的函数引用了变量i，并没有立刻执行。
             # 而是直到3个函数都返回时才执行f()，而此时变量i值为3。
             return i*i
        fs.append(f)
    # 返回内部函数
    return fs

f1, f2, f3 = count()
# 直接调用f()，此时变量i值为3
print(f1())
print(f2())
print(f3())

# 9
# 9
# 9
```

使用闭包时的注意事项：

闭包无法修改外部函数的局部变量。

闭包无法直接访问外部函数的局部变量。

* 在 Python3 前可以间接的使用容器类型来解决；
* 在 Python3 及其以后可以使用`nonlocal`关键字解决（表示这个变量不是局部空间的变量，需要向上一层变量空间中查找。[变量作用域](#变量作用域)）。

```python
def outer():
    x = 5 
    def inner(): 
        # 把 x 声明为非局部变量
        nonlocal x
        x *= x
        return x
    return inner 

print(outer()())
```

### 装饰器

在代码运行期间动态增加功能的方式称为**装饰器**（Decorator）。

装饰器的本质上就是一个接收一个函数作为参数，并返回一个函数的高阶函数。

常见的装饰符有：

| 装饰器            | 含义                                                         |
| ----------------- | ------------------------------------------------------------ |
| @unique           | 帮助检查枚举值保证成员没有重复值                             |
| @property         | 负责把一个方法变成属性调用的                                 |
| @abstractproperty | 用来控制子类必须全部实现重写父类的属性                       |
| @abstractmethod   | 用来控制子类必须全部实现重写父类的方法                       |
| @staticmethod     | 表示修饰的方法是**静态方法**<br />（静态方法在对象未创建时就可以调用） |
| @classmethod      | 表示修饰的方法是**类方法**<br />（默认不传递参数 self，但是必须传递参数 cls。<br />能够访问方法类属性，但是无法访问实例属性。） |

abc模块 —— Python 对于 ABC 的支持模块，定义了一个特殊的 metaclass —— `ABCMeta`，还有一些装饰器 `@abstractmethod` 和 `@abstarctproperty`。  
`abc.ABCMeta` 是一个metaclass，用于在 Python 程序中创建抽象基类。

[Python装饰器、metaclass、abc模块学习笔记 - 王智愚 - 博客园](https://www.cnblogs.com/Security-Darren/p/4094959.html)

修饰符的定义：

```python
import functools
def log(func):
    # 将原始函数中的__name__等属性赋值到wrapper()函数中
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        # 调用原始函数
        return func(*args, **kw)
    return wrapper

# 使用Python的@语法，把decorator置于函数的定义处。调用函数时会自动运行log装饰器
@log
def now():
    print('2015-3-25')

# 相当于执行 now = log(now)
now()

# call now():
# 2015-3-25
```

### 偏函数

`functools.partial`就是把函数的某些参数给固定，返回一个新函数。

偏函数定义：`partial(func, *args, **keywords) `，3个类型参数分别为：函数名，可变参数（元组），关键字参数（字典）。

```python
from functools import partial

def newSum(*args):
    s = 0
    for value in args:
        s = s + value
    return s

print("newSum:", newSum(1, 2, 3, 4, 5))

# 等同于 sum(10, *args)
sum_add_10 = partial(newSum, 10)
print("sum_add_10:", sum_add_10(1, 2, 3, 4, 5))

# 等同于 sum(10, 20, *args)
sum_add_10_20 = partial(newSum, 10, 20)
print("sum_add_10_20:", sum_add_10_20(1, 2, 3, 4, 5))

# 修改偏函数的关键字参数
def mod(m, key=2):
    return m % key == 0

print("mod_2:", mod(12))
# 修改 key 值为5
print("mod_3:", mod(12, key=5))
```

### 迭代器和生成器

#### 迭代器

迭代器对象（Iterator）表示一个数据流，对象中含有`iter()`和`next()`方法。

前者返回迭代器对象，后者依次返回数据，直到引发 StopIteration 异常结束。

使用内置`iter()`函数返回迭代器对象，可以避免对象状态在外部被修改。

* 迭代器对象从集合的第一个元素开始，直到所有的元素都被访问完结束。
* 迭代器只能向前不能向后遍历。
* 字符串、列表、集合或元组都可以用于创建迭代器。

> 凡是可作用于`for`循环的对象都是`Iterable`类型；
>
> 凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；  
> 集合数据类型如 list、dict、str 等是`Iterable`但不是`Iterator`。
>
> 可以使用`isinstance( ,Iterator)`来判断对象是否为`Iterator`对象。

```python
from collections import Iterator
list = [1, 2, 3, 4]
# 创建迭代器对象
it = iter(list)
# 输出迭代器下一个元素
print(next(it))
print(it.__next__())
# 判断是否为迭代器类型
print(isinstance(it, Iterator))

# 此时 it 遍历到第三位
for item in it:
    print("item:", item)

# 1
# 2
# True
# item: 3
# item: 4
```

#### 生成器

在 Python 中一边循环一边计算的机制，称为**生成器**。实质上，生成器保存的是能够推算出列表元素的某种算法逻辑。

编译器将包含`yield`的方法（或函数）重新打包，使其返回 Generator 对象。内部含有`next`方法，能够进行迭代操作（通常使用 for 循环来遍历获取返回值）。

`yield`是一个类似`return`的关键字，迭代时遇到`yield`时就返回其后边（右边）的值。  
而且，下一次迭代时从上一次迭代遇到的`yield`后代码开始执行。

> 使用`isgeneratorfunction`方法判断函数是否为 generator 函数。

另外一种快捷创建 generator 生成器的方法是：把列表生成式的`[]`换为`()`。

```python
# 简单的设置生成器方法是：将列表生成式中的[]换为()(生成器表达式)
L = [x * x for x in range(10)]	# 列表，list
g = (x * x for x in range(10))	# 生成器，generator
# 生成器表达式
(x * x for x in range(1, 11) if x % 2 == 0)
(m + n for m in 'ABC' for n in 'XYZ')

class Data(object):
    def __init__(self,*args):
        self._data = list(args)
    def __iter__(self):
        for x in self._data:
            yield x
d = Data(1 ,2, 3)
print d
for x in d:
    print x
# <__main__.Data object at 0x106a8a810>
# 1
# 2
# 3

def fibonacci(n):
	a， b, counter = 0, 1, 0
	while True:
		if counter > n:
			return
        # 返回保存 a 的值，下次循环接入上次的 a 值
		yield a
		a, b = b, a+b
		counter += 1
# 返回generator对象
f = fibonacci(10)

while True:
	try:
		print(next(f), end=" ")
    # 可以用来捕获 StopIteration 错误，进行下一步操作
	except StopIteration:
		sys.exit()
# 0 1 1 2 3 5 8 13 21 34 55 

# 判断函数是否为generator函数
from inspect import isgeneratorfunction
print isgeneratorfunction(fibonacci)
import types
# fibonacci是generator function,而fibonacci(5)是generator
# fibonacci是不可迭代的,而fibonacci(5)是可迭代的
print isinstance(fibonacci(5),types.GeneratorType)
# True
# True
```

[生成器和列表的区别](#列表解析)

### 协程

子程序（函数）的调用是通过栈实现的，即 A 调用 B，B 调用 C ，C 执行完返回 B、A的层级调用。  
而协程（Coroutine）在执行过程中，子程序内部可以中断。可以在执行 A 的过程中随时中断，去执行 B（不是函数调用，类似于 CPU 的中断）。

协程比[多线程](#线程)有什么优势？

* 协程执行效率高

  *在协程中子程序间切换不是线程切换，且是由程序自身控制的。*没有线程切换的开销，因此协程执行效率高。

* 协程不需要线程锁

  *协程操作是在一个线程上进行的，不存在写变量的冲突。*在协程中控制共享资源不需要加锁，只需要判断状态即可。

```python
def coroutine():
    print "coroutine start"
    result = None
    while True:
        # 让出执行绪,等待消息
        s = yield result
        result = s.split(",")
        print result
c = coroutine()
# 启动协程
c.send(None)
# 向协程发送消息,使其恢复执行
c.send("a,b")
c.send("c,d")
# 引发协程GeneratorExit异常,关闭协程
c.close()
c.send("e,f")
# coroutine start
# ['a', 'b']
# ['c', 'd']
# StopIteration

# 1.创建协程对象后,使用send()/next()启动
# 2.协程在执行到yield result后让出执行绪,等待消息.
# 3.调用方发送send("a,b")消息,协程恢复执行,将收到的数据保存到s,继续执行后续流程.
# 4.再次循环至yield,协程返回到前边的处理结果,并再次让出执行绪.
# 5.直到关闭或者引发异常.


def consumer():
	r = ""
	while True:
		# 3.通过yield拿到数据
		n = yield r
		if not n:
			return
		print("consumer:", n)
		time.sleep(1)
		# 4.处理过数据后传回结果
		r = "200 ok"


def produce(c):
	# 1.调用next操作启动生成器
	next(c)
	n = 0
	while n < 5:
		n = n + 1
		print("produce:", n)
		# 2.通过send函数切换到consumer函数中执行，并获取传回的结果
		r = c.send(n)
		print("consumer return:", r)
	c.close()

c = consumer()
produce(c)
# produce: 1
# consumer: 1
# consumer return: 200 ok
# produce: 2
# consumer: 2
# consumer return: 200 ok
# produce: 3
# consumer: 3
# consumer return: 200 ok
# produce: 4
# consumer: 4
# consumer return: 200 ok
# produce: 5
# consumer: 5
# consumer return: 200 ok
```

跟协程相关的第三方库：

使用 gevent 可以帮助我们自动切换协程，就保证总有 greenlet 在运行，而不是等待 IO 。

当一个 greenlet 遇到 IO 操作时，比如访问网络，就自动切换到其他的 greenlet 。等到IO操作完成，再在适当的时候切换回来继续执行。

相关资料：

* [Python yield 使用浅析](https://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/)
* [Python yield与实现](http://www.cnblogs.com/coder2012/p/4990834.html)
* [gevent 的使用](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001407503089986d175822da68d4d6685fbe849a0e0ca35000)

### 变量作用域

Python 中程序的变量并不是在哪个位置都可以访问的，访问权限取决于变量是在哪里赋值的。常见的作用域有：
* L（`Local`）：局部作用域
* E（`Enclosing`）：闭包函数外的函数中
* G（`Global`）：全局作用域
* B（`Built-in`）：内建作用域

查找时按照 L->E->G->B 的规则。

在内部作用域想修改外部作用域的变量时，需要使用`global`和`nonlocal`关键字修饰。

```python
num = 1
def fun1():
	# 在函数中修改全局变量前先加global声明
	global num
	print("num:", num)
	num = 10

fun1()
print("global num:", num)

def counter():
	num = 11
	def inner():
        # 需要修改嵌套作用域中变量时使用nonlocal关键字
		nonlocal num
		num = 12
		print("inner num:",num)
	inner()
	print("local num:",num)

counter()
print("global num:", num)

# num: 1
# global num: 10
# inner num: 12
# local num: 12
# global num: 10
```

### 模块

模块是扩展名为`.py`的文件。可以将函数存储在独立文件（模块）中，使用`import`语句即可导入模块。

调用时使用`module_name.function_name()`/`module_name.Class_name()`即可，使用`from module_name import function_name`/`from module_name import Class_name()`导入模块的特定函数。

```python
# 将make_pizza方法放在独立的文件中
import making_pizza as pizza
# 导入模块某个特定的函数/类
from making_pizza import build_profile, Dog

pizza.make_pizza("1")
pizza.make_pizza("1","2","3")
build_profile("userinfo", username = "张三",age = "22")

dog1 = Dog("田园犬","12")
dog1.sit()
dog1.name = "泰迪"
dog1.eat()
```

`dir()`函数可以找到模块中定义的所有名称。

`__name__`属性用来判断该程序块是否是在该模块自身中运行（使用`__name__=='__main__'`判断）。

`__author__`可以用来设置代码作者。

> 默认情况下，Python 解释器会搜索当前目录、所有已安装的内置模块和第三方模块，搜索路径存放在`sys`模块的`path`变量中。

可以使用目录来组织模块结构，避免模块名冲突。这就被称为**包**（package）。

> 每个包目录下都会有一个`__init__.py`的文件，用来代表包的默认模块。  
> 否则，Python 就会把包目录当做普通目录，而不是一个包。

可以使用多级目录来组成多层次的包结构。

## 类

Python 是面向对象的语言。

* 问题空间

  > 问题空间是问题解决者对一个问题所达到的全部认识状态，它是由问题解决者利用问题所包含的信息和已贮存的信息主动地构成的。

  问题空间一般包含初始状态、目标状态、操作三部分。

* 对象

  > 对象（object），是面向对象（Object Oriented）中的术语。既表示客观世界问题空间（Namespace）中的某个具体的事物，又表示软件系统解空间中的基本元素。

  在 OOP 中对象的相关定义为：一个对象有自己的属性（状态）、方法（行为）和唯一的标识（本质上指对象的内存地址）。

* 类

  > 类（class）是一种面向对象计算机编程语言的构造，描述了所创建的对象共同的**属性**和**方法**。

  类有**接口**（描述了如何通方法与类及其实例相互操作）和**结构**（描述了实例中数据如何划分多个属性）。

  类的出现为面向对象编程（封装、继承、多态）提供了实现的手段。

### 类的定义

方法`__init__()`为系统约定的方法名。

* 方法中形参`self`是必不可少的。
* 每个与类相关联的方法调用都会自动传递实参`self`。
* 设置类的属性时，直接在 init 方法中赋值即可。
* init 方法中不需要显式地调用 return 语句，系统会自动返回创建成功的实例。

```python
# 默认继承父类object，可以不写
class Dog():
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def sit(self):
        print(self.name + "sit down")
    def eat(self):
        print(self.name.title() + "eating")
    def info(self):
        print("name:" + self.name + ",age:" + self.age)
dog1 = Dog("田园犬","12")
dog1.sit()
dog1.name = "泰迪"
dog1.eat()
# 田园犬sit down
# 泰迪eating
```

可以使用`.`语法来调用/设置类中的任意属性和方法。

可以使用方法或者直接修改类的属性。

> 同一个类的不同实例变量拥有的变量名称都可能不同。

### 访问控制

在类的内部可以有属性和方法，外部代码可以通过直接调用实例变量的方式来操作数据。

如果要让内部属性不被外部访问，可以在属性名称前加双下划线（`__`）。此方式使得实例的变量变为**私有变量**，只有内部可以访问，外部不能访问。

> 使用双下划线开头并结尾的变量（形如`__xxx__`）的是特殊变量，是可以直接访问的。
>
> 使用单下划线开头的变量（形如`_xxx`）的实例变量外部是可以访问的。  
> 但是按照约定俗成的规定，当你看到此类变量时请当做私有变量，不要随意访问。

### 类的继承

子类在继承了父类的方法后，可以对父类已有的方法给出新的实现版本，这个动作称之为方法重写（override）。

自定义子类时，需要在声明时将父类类型名称放于括号中。

> 继承可以存在多重继承。  
> 多重继承时对属性和方法搜索的顺序依照`广度优先`。（先后继承的类中含有相同的方法，但调用时使用前者类中的方法。）

```python
# 继承父类Dog
class SubDog(Dog):
    def __init__(self, subName, subAge, sex):
        # 初始化父类的属性
        super().__init__(subName, subAge)
        # 先初始化父类的属性，再设置子类的属性
        self.sex = sex
    # 重写父类方法
    def info(self):
        print("name:" + self.name + ",age:" + self.age + ",sex:" + str(self.sex))
subDog1 = SubDog("subDog", "10",False)
subDog1.info()
# name:subDog,age:10,sex:False
```

要使用 ABC（ABC 是一些无法被实例化的类），子类必须继承自此 ABC 并且还要覆盖其抽象方法。

可以使用`@abstractmethod`装饰器（抽象方法）来控制子类必须全部实现重写父类的方法。  
同理，还有`@abstractproperty`装饰器（抽象属性）。

**Mixin 设计模式**：

Mixin 是一种思想，用部分实现的接口来实现代码的复用。常见的实现方式有 protocol 和多重继承。

Mixin 的目的是给一个类添加多个功能，在设计类的时候尽量考虑使用 Mixin，而不是使用多层次的复杂继承关系。

```python
# 哺乳动物、能跑、肉食动物
class Dog(Mammal, RunnableMixIn, CarnivorousMixIn):
    pass
# 多进程模式的 TCP 服务
class MyTCPServer(TCPServer, ForkingMixIn):
    pass
# 多线程模式的 UDP 服务
class MyUDPServer(UDPServer, ThreadingMixIn):
    pass
```

### 类的多态和封装

#### 多态

在函数中不限制参数的类型。

经过子类重写后，不同的子类对象表现出不同的行为，这就是多态。

> 多态是指相同的信息给予不同的物件后会引发不同的动作。

**多态的特点：**

* 调用方只管调用，不管细节
* 对扩展开放（允许新增子类）
* 对修改封闭

**静态语言 VS 动态语言：**

静态语言传入类型必须是该类或者它的子类，否则对应的方法就无法调用。

而动态语言对传入的类型并没有严格要求，只需要传入的对象含有调用的方法即可。  
动态语言的这种特性叫做`鸭子类型`。Python 的`file-like object`就是一种鸭子类型。

#### 封装和私有化

> 封装(Encapsulation)是对 object 的一种抽象，即将某些部分隐藏起来，在程序外部看不到也无法调用。

Python 中在准备私有化的属性（包括方法、属性）名字前加双下划线。（[访问控制](#访问控制)）

### 对象信息的获取

* 类型判断

  可以使用`type()`函数来获取对象类型和创建新的类型。还可以使用`types`模块中定义的常量获取更多信息。

  ```python
  import types
    def fun():
        pass
  
  print(type(fun) == types.FunctionType)
  # type(abs)==types.BuiltinFunctionType
  # type(lambda x: x)==types.LambdaType
  # type((x for x in range(10)))==types.GeneratorType
  
  # True
  
  # 还可以使用type创建出新的类型
  def fn(self, name='world'): # 先定义函数
      print('Hello, %s.' % name)
  # type(name, bases, dict) -> a new type
  # 第一个参数：class的名称
  # 第二个参数：继承的父类集合，使用tuple表示多重继承
  # 第三个参数：class的方法名称与函数绑定
  Hello = type('Hello', (object,), dict(hello=fn)) # 创建Hello class
  ```

  可以使用`isinstance()`函数判断一个对象是否是该类型本身，或者位于该类型的父继承链上。

  可以使用`callable()`函数判断一个对象是否是可调用对象。

* 使用 dir() 方法

  可以使用`dir()`获取对象的所有属性和方法。

  > 使用双下划线开头并结尾的变量（形如`__xxx__`）是特殊变量。  
  > 比如`__len__`方法返回长度，在调用`len()`时函数内部会自动去调用对象的`__len__()`方法。

  如果希望在自定义类中使用此类方法，需要实现对应的双下划线方法。

  可以使用`hasattr()`、`setattr()`、`getattr()`来判断是否含有属性、设置属性、获取属性。

* 实例属性和类属性

  Python 中属性的获取是按照从下到上的顺序来查找属性。  
  Python 中实例属性是各个实例所有的，互不干扰。  
  Python 中类属性是类所有的，所有实例共享一个属性。

  > 在设置时要尽量避免实例属性和类属性同名，否则同名的实例属性会屏蔽掉类属性。

  ```Python
  class Student():
  	def __init__(self, name):
  		# 设置实例属性
  		self.nameStr = name
  
  	# 设置类属性
  	nameStr = "Student"
  
  s = Student("Jack")
  print("s.nameStr", s.nameStr)
  print("Student.nameStr", Student.nameStr)
  s.nameStr = "Mick"
  print("s.nameStr", s.nameStr)
  del s.nameStr
  print("del s.nameStr")
  print("s.nameStr", s.nameStr)
  print("Student.nameStr", Student.nameStr)
  
  # s.nameStr Jack
  # Student.nameStr Student
  # s.nameStr Mick
  # 删除实例属性后，类属性可以正常访问
  # del s.nameStr
  # s.nameStr Student
  # Student.nameStr Student
  ```

* 使用`__slots__`

  正常情况下可以在创建类的实例后给该实例绑定任何的属性和方法。  
  但是，给实例绑定的属性只有对该实例有用，对类绑定的属性对该类的所有实例都有效。

  > `__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。

  ```python
  class Student(object):
      pass
  
  s1 = Student()
  # 动态的给实例添加属性 name
  s1.name = "张三"
  print(s1.name)
  
  s2 = Student()
  # AttributeError: 'Student' object has no attribute 'name'
  # 实例 s2 没有添加属性 name
  print(s2.name)
  
  # 动态的给类添加属性 realName
  Student.realName = "Jim"
  
  s3 = Student()
  # 实例 s2 含有属性 realName
  print("s2.realName default:" + s2.realName + ",s3.realName default:" + s3.realName)
  s3.realName = "Mick"
  print("s3.realName now:" + s3.realName)
  ```

  为了达到限制的目的，Python 允许在定义类的时候定义一个特殊的`__slots__`变量，来限制该class实例能添加的属性。

  ```python
  class Student(object):
      __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
  
  s = Student()
  # AttributeError: 'Student' object has no attribute 'realName'
  s.realName = "张三"
  ```

* 使用 @property

  Python 内置的`@property`[装饰器](#装饰器)就是负责把一个方法变成属性调用的。

  与`@property`相关的是另一个装饰器`@score.setter`，负责把一个 setter 方法变成属性赋值。

  这对装饰器可以配合使用来控制属性的读写情况。

  ```python
  class Student():
      # birth为可读可写
  	@property
  	def birth(self):
          # 约定下划线开头的属性在外部调用时会被视为私有变量，不能随意访问
  		return self._birth
  	@birth.setter
  	def birth(self, value):
  		self._birth = value
      # age为只读属性
  	@property
  	def age(self):
  		return 2018-int(self._birth)
  
  s = Student()
  s.birth = "1992"
  print(s.birth,s.age)
  # 1992 26
  ```

  > 约定下划线开头的属性在外部调用时会被视为私有变量，不能随意访问。（[访问控制](#访问控制)）

  [python基础-abstractmethod、__属性、property、setter、deleter、classmethod、staticmethod - CSDN博客](https://blog.csdn.net/u013210620/article/details/78604077)

### 特殊方法

参考资料：[特殊方法 (1) - 《从零开始学 Python》(第二版) - 极客学院Wiki](http://wiki.jikexueyuan.com/project/start-learning-python/212.html)

* 静态方法和类方法
  * `@staticmethod`表示下面的方法是**静态方法**

    默认不传递参数 self，无法访问实例变量、类和实例的属性。静态方法在对象未创建时就可以调用。

  * `@classmethod`表示下面的方法是**类方法**

    默认不传递参数 self，但是必须传递参数 cls。类方法能够访问方法类属性，但是无法访问实例属性。

  ```python
  from math import sqrt
  
  class Triangle(object):
  	def __init__(self, a, b, c):
  		self._a = a
  		self._b = b
  		self._c = c
  
  	# 静态方法,对象未创建时就可调用
  	@staticmethod
  	def is_valid(a, b, c):
  		return a + b > c and a + c > b and b + c > a
  
  	def perimeter(self):
  		return self._a + self._b + self._c
  
  	def area(self):
  		half = self.perimeter() / 2
  		return sqrt(half * (half - self._a)) * (half - self._b) * (half - self._c)
  
  	# 定义类方法,类方法的第一个参数约定名为cls
      @classmethod
  	def class_method(cls, a, b, c):
  		if cls.is_valid(a, b, c) == False:
  			return cls(0, 0, 0)
  		return cls(a, b, c)
  
  a, b, c = 3, 4, 5
  # 静态方法和类方法都直接给类发消息调用
  if Triangle.is_valid(a, b, c):
  	t = Triangle(a, b, c)
  	print(t.perimeter())
  	# 可以通过给类发消息调用对象方法,但是需要传入接收对象
  	print(Triangle.area(t))
  	# 使用类方法创建对象
  	tt = Triangle.class_method(2, 3, 4)
  	print(tt.perimeter())
  else:
  	print("当前无法组成三角形")
  ```

* `__setattr__`、`__getattr__`等方法

  当要访问的属性不存在时，就会调用相关方法进行拦截。

  * `__setattr__(self,key,value)`：如果要给 key 赋值，就调用这个方法。

  * `__getattr__(self,item)`：如果 item 被访问，同时它不存在的时候，此方法被调用。

  * `__getattribute__(self,item)`：当 item 被访问时自动被调用，无论 item 是否存在，都要被调用。

  * `__delattr__(self,item)`：如果要删除 item，这个方法就被调用。

    ```python
    class A():
        # item被访问，且其不存在时被调用
        def getattr(self, item):
            print("getter:", item)
        # 给对象赋值时调用
        def setattr(self, key, value):
            print("setter:%s,%s" % (key, value))
            self.dict[key] = value
            
        # def getattribute(self, item):
        #   print("getter attr:", item)
    print("-----⬇️-----")
    a = A()
    print(a.x)
    a.x = 7
    print(a.x)

    # -----⬇️-----
    # getter: x
    # None
    # setter:x,7
    # 7
    ```

* ` __str__`方法的调用

  使用`__str__()`方法可以打印对象内部信息，此信息是用户可见的。  
  使用`__repr__()`可以返回程序开发者看到的字符串。

  ```python
  class Student(object):
      def __init__(self, name):
          self.name = name
      def __str__(self):
          return 'Student object (name=%s)' % self.name
      # 可以直接通过此方式设置两个函数返回的字符
      __repr__ = __str__
  # 调用__str__函数
  print(Student('Michael'))
  # 调用__repr__函数
  s = Student('Michael')
  s
  ```

* 使用`__iter__()`方法

  实现`__iter__()`方法和`__next__()`方法可以使得自定义对象具备迭代能力。（[迭代器](#迭代器)）

* 使用`__getitem__()`方法

  使得对象可以像 list 那样使用下标取出元素。

  ```python
  class Fib(object):
      # 自定义对象支持类似list的遍历
      def __getitem__(self, n):
          if isinstance(n, int): # n是索引
              a, b = 1, 1
              for x in range(n):
                  a, b = b, a + b
              return a
          if isinstance(n, slice): # n是切片
              start = n.start
              stop = n.stop
              if start is None:
                  start = 0
              a, b = 1, 1
              L = []
              for x in range(stop):
                  if x >= start:
                      L.append(a)
                  a, b = b, a + b
              return L
  
  f = Fib()
  print(f[3])		# 按照下标取值
  # 3
  print(f[0:5])	# 切片操作
  # [1, 1, 2, 3, 5]
  ```

* 使用`__getattr__()`方法

  使用该方法可以动态的返回属性。当调用不存在的属性时，Python 解释器会调用该方法来尝试获得属性。

  ```python
  class Student(object):
      # 当 score 属性不存在时，就会调用该方法来获取值
      def __getattr__(self, attr):
          if attr=='score':
              return 99
          # 其他不存在的属性值按照约定，抛出 AttributeError
          raise AttributeError('\'Student\' object has no attribute \'%s\'' % attr)
  ```

* 使用`__call__()`方法

  使用该方法可以直接对实例进行调用，还可以在调用过程中传入参数（就像对函数的调用）。

  通过`callable()`函数可以判断调用对象是否为`Callable`对象。

  ```python
  class Student(object):
      def __init__(self, name):
          self.name = name
  
      # __call__ 方法还可以传入参数
      def __call__(self, *args, **kwargs):
          print('My name is %s.' % self.name)
  
  s = Student('Michael')
  s()
  # My name is Michael.
  callable(Student())
  # True
  ```

### 类的导入

类可以导入一个模块中的单个、多个类甚至是整个模块中的所有类。导入声明使用`import`关键字。

## 进程和线程

对于操作系统而言，一个任务就是一个[**进程**](https://zh.wikipedia.org/wiki/%E8%A1%8C%E7%A8%8B)。一个进程内部拥有的多个可获得 CPU 调度的执行单元就是[**线程**](https://zh.wikipedia.org/wiki/线程)。

> **线程**（英语：thread）是操作系统能够进行运算调度的最小单位。

Python 既支持多进程又支持多线程，因此 Python 实现并发常见的模式有：多进程、多线程、多进程 + 多线程。

### 进程

Unix/Linux 操作系统提供了`fork()`的系统调用用来创建子进程。

Python 的`multiprocessing`模块封装了常见的系统调用，比如创建进程对象的 Process、批量启动进程的进程池（Pool）、进程间通信的队列（Queue）和管道（Pipe）。

#### 子进程

可以使用 Process 对象创建子进程。

* start()：启动进程。
* join()：等待所有子进程结束后再继续向下执行，常用于进程间的同步。
* terminate()：终止进程。

```python
def run_proc(name):
    print("run child process %s(%s)" % (name, os.getppid()))

print("\nparent process %s." % os.getpid())
# 创建子进程
p = Process(run_proc("test"))
# p = Process(name="test")
# p = Process(target=run_proc, args=('test',))
print("child process will start")
# 启动进程
p.start()
# 进程间同步
p.join()
print("child process end")
```

`subprocess`模块的`call()`方法或`communicate()`方法来也可以启动子进程，甚至控制其输入和输出。

> 创建子进程时，子进程复制了父进程及其所有的数据结构，每个子进程有自己独立的内存空间。

#### 进程池

如果需要启动大量的子线程，可以使用进程池（`Pool`）批量创建子进程。

close()：进程池关闭后会停止加入新的进程。

```python
def long_time_task(name):
    print("run task %s(%s)" %(name, os.getpid()))
    # 获取当前时间
    start = time.time()
    time.sleep(random.random() * 3)
    end = time.time()
    print("task %s run %0.2f sec" % (name, (end - start)))

print("\nparent process %s." % os.getpid())
# 进程池
p = Pool(4)
for i in range(5):
    p.apply_async(long_time_task(i))

print("waiting for all sub process done")
# 进程池停止加入新线程
p.close()
# 等待所有子进程完成
p.join()
print("all process done")
```

#### 进程同步

使用`Queue`可以实现进程间的通信。

```python
def write_method(q):
    print("process to write:%s" % os.getpid())
    for value in ["A", "B", "C"]:
        print("put %s into queue" % value)
        q.put(value)
        time.sleep(random.random())

def read_method(q):
    print("process to read:%s" % os.getpid())
    while True:
        value = q.get(True)
        print("get %s frome queue" % value)

# 队列
q = Queue()
pw = Process(target=write_method(q))
pr = Process(read_method(q))
# 启动子进程pw,写入
pw.start()
# 启动子进程pr,读取
pr.start()
# 等待pw结束
pw.join()
# 强行终止进程
pr.terminate()
```

### 线程

多任务可以由多进程完成，也可以由一个进程中的多线程完成。一个进程至少有一个线程，线程的调度是由操作系统决定的。

Python 中使用`threading`模块来实现多线程。  
启动一个线程就是把一个函数传入并创建`Thread`实例，然后调用`start()`开始执行。

- threading.currentThread：获取当前线程
- threading.Thread：创建新线程

```python
def loop():
    # threading.currentThread 获取当前线程
    print("thread (%s) is running" % threading.currentThread().name)
    n = 0
    while n < 5:
        n = n + 1
        print("thread (%s) >>> %s" % (threading.currentThread().name, n))
        time.sleep(1)
    print("thread (%s) ended." % threading.currentThread().name)

print("thread (%s) is running..." % threading.currentThread().name)
# threading.Thread 创建新线程
t = threading.Thread(target=loop, name="LoopThread")
# 开始新线程
t.start()
t.join()
print("thread (%s) is end." % threading.currentThread().name)

# thread (MainThread) is running...
# thread (LoopThread) is running
# thread (LoopThread) >>> 1
# thread (LoopThread) >>> 2
# thread (LoopThread) >>> 3
# thread (LoopThread) >>> 4
# thread (LoopThread) >>> 5
# thread (LoopThread) ended.
# thread (MainThread) is end.
```

#### 线程锁

线程间共享数据时可能会存在多个线程同时修改同一变量（临界资源），因此数据操作时需要做加锁处理。

> 多线程和多进程最大的不同在于：
>
> **多进程**中，同一变量在每个进程中都有拷贝，互不影响。  
> **多线程**中，所有变量都是线程共享的，因此存在多线程操作同一数据的问题。
>
> **[协程](#协程)**是由程序自身控制的子程序切换而不是线程切换，协程是在一个线程上的不需要线程锁。

- threading.Lock()：创建线程锁。
- acquire()：获取线程锁。当多个线程都执行此方法时，只会有一个线程能够成功获取锁。
- release()：释放锁。当前锁使用完成后，一定要释放锁的资源。
- multiprocessing.cpu_count()：多核 CPU 可以通过`multiprocessing`模块用来获取 CPU 数量。

```python
balance = 0
# 创建线程锁
lock = threading.Lock()

def run_thread(n):
    for i in range(100000):
        # 获取锁
        lock.acquire()
        try:
            # 修改数据
            change_it(n)
        finally:
            # 释放锁
            lock.release()

t1 = threading.Thread(target=run_thread, args=(5,))
t2 = threading.Thread(run_thread(8))
t1.start()
t2.start()
t1.join()
t2.join()
print("current balance:%s" % balance)
```

#### ThreadLocal

使用`threading.local()`方法创建一个`ThreadLocal`对象，每个 Thread 都对它的属性有读写权限。

可以将该对象视为全局变量，但是对象的属性对于每个线程来讲又是其局部变量。

```python
# 创建全局 ThreadLocal 对象
local_school = threading.local()
def process_student():
    # 获取当前线程关联的 student 对象
    std = local_school.student
    print("hello, %s (in %s)" % (std, threading.currentThread().name))

def process_thread(std_name):
    # 绑定对象至当前线程的 ThreadLocal 对象
    local_school.student = std_name
    process_student()


t1 = threading.Thread(target=process_thread, args=("张三",), name="Thread-A")
t2 = threading.Thread(target=process_thread, args=("李四",), name="Thread-B")
t1.start()
t2.start()
t1.join()
t2.join()

# hello, 张三 (in Thread-A)
# hello, 李四 (in Thread-B)
```

## 文件和异常

同步 IO 和异步 IO（回调模式、轮询模式）。

常见的文件操作函数：

* `open()`函数

  传入文件名和标识符用来打开文件，返回该文件的对象。

  读取非 UTF-8 编码的文本文件时，需要给函数传入 `encoding`参数。
  函数还可以接受一个`errors`参数，表示遇到错误后的处理方式。

  常见的操作标识符有：

  | 标识符 | 释义                               |
  | ------ | ---------------------------------- |
  | r      | 读取文本内容                       |
  | rb     | 读取二进制文件，图片、视频等       |
  | r+     | 读取和写入文件                     |
  | w      | 写文件（如果文件存在，会直接覆盖） |
  | wb     | 写二进制文件                       |
  | a      | 追加模式写入                       |
  | b      | 二进制模式                         |
  | t      | 文本模式（默认）                   |

  [open() 函数操作符的定义和含义](https://docs.python.org/3/library/functions.html#open)

* `close()`函数：关闭文件。读写操作后要记得关闭文件。

* `with`关键字：自动打开文件`open()`和关闭文件`close()`。

* `read()`函数

  读取文件信息。要尽量避免一次性读取文件的全部内容。

* `readline()`和`readlines()`函数

  每次读取一行内容和读取文件的多行，并存储在列表中。

  此函数能够很好的处理大文件读取操作。

* `tell()`函数：返回文件对象当前所处的位置。

* `seek()`  函数：改变文件当前位置（`seek(offset, from_what)`）。

> 获取文件内容时，要使用`try ... finally`语句来进行容错处理。

**StringIO 和 BytesIO**：

Python 中的 StringIO 模块负责字符串在内存中的读写，BytesIO 模块负责二进制数据在内存中的读写。

`write()`函数写入数据至内存，`getvalue()`函数用于获取写入后的数据。

## 异常处理

运行期间出现的错误被称为**异常**。  
异常错误信息中常含有异常发生的上下文，并以调用栈的形式显示具体信息。

Python 中所有的错误类型都继承自`BaseException`。（[常见的错误类型和继承关系](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) | [总结：Python中的异常处理 - Python测试开发 - SegmentFault 思否](https://segmentfault.com/a/1190000007736783)）

### 异常捕捉

常使用`try-except-else`语句捕捉处理异常。

一个 try 子句可以包含多个 except 异常，可以分别来处理对应异常或使用一个 except 子句处理多个异常（将异常放在元组中）。  
else 语句可以在 try 语句没有任何异常后执行。  
finally 子语句不论异常与否都会执行。

```python
try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
# 分别处理异常
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
# 处理多个异常
except (RuntimeError, TypeError, NameError):
    pass
except:
    print("Unexpected error:", sys.exc_info()[0])
    # 使用raise语句抛出指定异常
    raise NameError('HiThere')
else:
    print(arg, 'has', len(f.readlines()), 'lines')
    f.close()
```

### 异常抛出

Python 可以使用`raise`语句抛出异常、抛出指定异常或用户指定异常类型。

`raise`语句不带参数时，就会把当前错误原样抛出。

```python
class MyError(Exception):
def __init__(self, value):
    self.value = value
def __str__(self):
    return repr(self.value)

try:
    # 抛出自定义错误
    raise MyError(2*2)
except MyError as e:
    print('My exception occurred, value:', e.value)
```

### 清理行为

可以在 try 语句的`finally`子语句中添加无论任何情况下都会执行的清理行为。

```python
try:
    raise KeyboardInterrupt
finally:
    # 不论try子句里是否发生异常，finally子句都会执行。
    print('Goodbye, world!')
```

> `with`语句可以包含文件对象在使用完成后会被正确的关闭，这就是系统预定义的清理行为。

### 代码调试

#### 断言

使用`assert`来辅助进行调试。如果断言失败，`assert`语句就会抛出`AssertionError`错误。

在启动 Python 解释器时，可以使用`-o`参数来关闭`assert`。

#### 错误记录

Python 内置的`logging`模块可以记录错误信息。使用`logging.info()`就可以输出一段文本。

`logging`允许指定记录信息的级别：debug、info、warning、error等。

#### 单元测试

Python 中单元测试需要导入自带的`unittest`模块，编写的测试类要从`unittest.TestCase`继承，测试方法要以`test`开头。

单元测试有两个特殊的方法：`setup()`和`tearDown()`。

最常用的断言是`assertEqual()`，常见的错误有`KeyError`、`AttributeError`。

## 数据可视化

`数据可视化`是指通过可视化表示来探索数据。  
`数据挖掘`是指使用代码来探索数据集的规律和关联。其中`数据集`可以是用一行代码就能表示的小型数字列表，也可以是大型数据。

### matplotlib 图表

图表类库的导入:`import matplotlib.pyplot`

#### 使用`plot()`绘制折线图

* 图表绘制:`plot()`
* 打开查看器:`show()`
* 绘制标题:`title()`
* 设置x/y轴属性:`xlabel()/ylabel()`
* 设置刻度样式:`tick_params()`

```python
import matplotlib.pyplot as plt

input_values = [1, 2, 3, 4, 5]
squares = [1, 4, 9, 16, 25]
# 绘制方法(给plot方法同时指定输入输出)
plt.plot(input_values, squares, lineWidth=5)
# 设置图表标题
plt.title("Square Numbers", fontSize=24)
# 设置图表x/y轴标题
plt.xlabel("Value", fontSize=4)
plt.ylabel("Square of Value", fontSize=14)
# 设置刻度标记的大小
plt.tick_params(axis='both', labelsize=14)
# 打开matplotlib查看器，并显示图形
plt.show()
```

#### 使用`scatter()`绘制散点图

* 散点绘制:`scatter()`

  参数`c`可以直接设置点的颜色，还可以配合`cmap(colormap)`设置渐变颜色。  
  参数`s`用以设置点的大小。

* 指定坐标轴取值范围:`axis()`

* 保存图表到本地:`savefig()`

  参数`bbox_inches`可以设置裁去多余空白区域。

```python
import matplotlib.pyplot as plt

# 绘制散列点(传入一对坐标或者一组坐标)
# plt.scatter(2, 4, s=200)

# x_values = [1, 2, 3, 4, 5]
# y_values = [1, 4, 9, 16, 25]

x_values = list(range(0, 1001))
y_values = [x**2 for x in x_values]

# 设置渐变颜色(使用cmap转换颜色，使用edgecolors去除描边颜色，使用s设置点大小)
plt.scatter(x_values, y_values, c=y_values, cmap=plt.cm.Blues, edgecolors='none', s=200)
plt.title("Square Numbers", fontSize=24)
plt.xlabel("Value", fontSize=14)
plt.ylabel("Square of Value", fontSize=14)
plt.tick_params(axis='both', which="major", labelsize=14)
# 指定坐标轴取值范围
plt.axis([0, 1100, 0, 1100000])
# plt.show()
# 保存图表到本地文件(bbox_inches参数设置裁去多余空白区域)
plt.savefig('sactter_plot.png', bbox_inches='tight')
```

---

[⬅️ Back](./)

[⬆️ 回到顶部 ⬆️](#Python基础入门)