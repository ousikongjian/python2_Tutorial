# 第二章 Python 对象

>Python 是解释性语言，但被认为是一种“面向对象的编程语言”，其内部任何类型的值都是一个对象。所有的 Python 对象都拥有三个特性：身份，类型和值。
身份：每一个对象都有一个唯一的身份标识自己，可以使用内建函数 id() 得到，极少用到这个值，不用太关心它究竟是什么。
类型：用内建函数 type() 查看 Python 对象的类型， type() 返回的是对象而不是简单的字符串。
值：对象表示的数据项。
上面三个特性在对象创建的时候就被赋值，除了值之外，其它两个特性都是只读的。**对于新式类型和类，对象的类型也是可以改变的，不过不推荐初学者这样做**。

## 2.1 标准类型

- Integer  整型
- Boolean  布尔型
- Long Integer  长整型
- Floating point real number  浮点型
- Complex number  复数型
- String  字符串
- List  列表
- Tuple  元组
- Dictionary  字典

## 2.2 其它内建类型

- 类型
- Null 对象（None）
- 文件
- 集合/固定集合
- 函数/方法
- 模块
- 类

### 2.2.1 类型对象和 type 类型对象

类型是保存对象的一系列固有行为和特性（比如支持哪些算法，有哪些方法）最合适的位置。类型不能是一些简单的字符串，这些信息不能也不应该和数据保存在一起，所以类型被定义为了对象。

下面我们来介绍一下内建函数type().

```bash
>>> import os
>>> os
<module 'os' from '/opt/ousikeji/flask/lib/python2.7/os.pyc'>
>>> type(os)
<type 'module'>
>>> type(type(os))
<type 'type'>
>>> 
```

首先，我们导入 os 模块， os 模块作为一个对象，直接显示出来对象的信息。再次，我们利用内建函数 type() 查看 os 模块的类型为 `<type 'module'>`，最后，我们可以得知类型对象的类型是type，它也是所有 Python 类型的根和所有 Python 标准类的默认元类（metaclass）。

随着 Python 2.2 中类型和类的统一，我们可以通过对比得知，类就是类型，实例是对应类型的对象。具体可以理解为类和类型都是`< >`来表示。

### 2.2.2 None —— python 的 null 对象

Python 有一个特殊类型，被成为 Null 对象或者 NoneType，它只有一个值，那就是 None。 None 没有什么有用的属性，它的布尔值总是 False。

空对象、值为零的任何数字或者 Null 对象的 None 的布尔值都是 False。
下列对象的布尔值是 False。

 - 列表项
 - None
 - Fasle（布尔类型）
 - 所有值为零的数
 - 0（整型）
 - 0.0（浮点型）
 - 0L（长整型）
 - 0.0 + 0.0j（复数）
 - ""（空字符串）
 - []（空列表）
 - ()（空元组）
 - {}（空字典）

## 2.3 内部类型

- 代码
- 帧
- 跟踪类型
- 切片
- 省略
- Xrange


一般的程序员通常不会直接和这些对象打交道，我们哟感到的机会很少，此处仅仅是做一下介绍。

### 2.3.1 代码对象

代码对象是编译过的 python 源代码片段，它是可执行对象。通过调用函数 `complie()` 可以得到代码对象。

```bash
>>> code = "for i in range(0, 10): print i"
>>> cmpcode = compile(code, '', 'exec')
>>> exec cmpcode
0
1
2
3
4
5
6
7
8
9
>>> str = "3 * 4 + 5"
>>> a = compile(str,'','eval')
>>> eval(a)
17
```

代码对象本身不包含任何执行环境信息，它是用户自定义函数的核心，在被执行时动态获得上下文。一个函数除了有代码对象属性以外，还有一些其它函数必须的属性，包括函数名、文档字符串、默认参数及全局命名空间等。

### 2.3.2 帧对象

帧对象表示 python 的执行栈帧。帧对象包含 Python 解释器在运行时所需要知道的所有信息。它的属性包括指向上一帧的链接，正在被执行的代码对象，本地及全局命名空间字典及当前指令等。每次函数调用产生一个新的帧，每一个帧对象都会相应创建一个 C 栈帧。用到帧对象的一个地方是跟踪记录对象。

### 2.3.3 跟踪记录对象

当你的代码出错时，Python 会引发一个异常。如果异常未被捕获和处理，解释器就会退出脚本运行，显示类似下面的诊断信息。

```bash
  File "demo.py", line 44
    a.extend(getTitle(html))
    ^
IndentationError: unexpected indent
```

当异常发生时，一个包含针对异常的帧跟踪信息的跟踪记录对象被创建。如果一个异常有自己的处理程序，处理程序就可以访问这个跟踪记录对象

### 2.3.4 切片对象

以字符串为例来展示切片，步进切片的语法 sequence[start:end:seq]。

```bash
>>> str = u'uvwxyz'
>>> str[::]
u'uvwxyz'
>>> str[::1]
u'uvwxyz'
>>> str[::-1]
u'zyxwvu'
>>> str[::-2]
u'zxv'
>>> str[::2]
u'uwy'
>>> list = [u'xyz', 678, 'abc',30.28]
>>> list[::]
[u'xyz', 678, 'abc', 30.28]
>>> list[::-1]
[30.28, 'abc', 678, u'xyz']
>>> 
```

### 2.3.5 省略对象

省略对象有一个唯一的名字 Ellipsis，它的布尔值始终为 True，没有任何属性。用于表示索引查找 [] 中省略号（...）是否存在。

```bash
>>> a = ['a','b']
>>> a.append(a)
>>> print a
['a', 'b', [...]]
>>> a[2]
['a', 'b', [...]]
>>> a[1]
'b'
>>> a[0]
'a'
>>> a[2]
['a', 'b', [...]]
>>> 
```

出现“...”的原因：出现了类似无限循环的结构，因为 a[2]=a

### 2.3.6 XRange 对象

```bash
>>> x = xrange(6)
>>> print x
xrange(6)
>>> print x[0]
0
>>> print x[6]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: xrange object index out of range
>>> print x[5]
5
>>> x = range(6)
>>> print x
[0, 1, 2, 3, 4, 5]
>>> print x[6]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
>>> 
```

**range()返回一个递增或递减的数字列表，列表的元素值由三个参数决定:**

 - start表示列表开始的值，默认为“0”。
 - stop 表示列表结束的值，该参数不可缺少。 
 - 参数step表示步长，默认值为“1”。
 - range()返回的是一个递增或递减的数字列表。

**xrange 是一个类，返回的是一个xrange对象。**使用 xrange() 进行遍历，每次遍历只返回一个值。range() 返回的是一个列表，一次性计算并返回所有的值。因此，xrange() 的执行效率要高于  range()，用于需要节省内存使用或 range() 无法完成的超大数据集场合。

## 2.4 标准类型操作符

### 2.4.1 对象值的比较

比较操作符用来判断类型对象是否相等，所有的内建类型均支持比较运算，比较运算返回布尔值 True 或 False。

**标准类型值比较操作符**

|操作符|功能|
|-----|-----|
|expr1 < expr2|expr1 小于 expr2|
|expr1 > expr2|expr1 大于 expr2|
|expr1 <= expr2|expr1 小于等于 expr2|
|expr1 >= expr2|expr1 大于等于 expr2|
|expr1 == expr2|expr1 等于 expr2|
|expr1 != expr2|expr1 不等于 expr2|

### 2.4.2 对象身份比较

**标准类型对象身份比较操作符**

|操作符|功能|备注|
|-----|-----|---|
|obj1 is obj2| obj1 和 obj2 是同一个对象| 等价于 id(obj1) == id(obj2)|
|obj1 is not obj2| obj1 和 obj2 不是同一个对象| 等价于 id(obj1) != id(obj2)|

### 2.4.3 布尔类型

**标准类型布尔操作符**

|操作符|功能|
|-----|-----|
| not expr | expr 的逻辑非（否）|
| expr1 and expr2 | expr1 和 expr2 的逻辑与|
| expr1 or expr2 | exor1 和 expr2 的逻辑或|

## 2.5 标准类型内建函数

**标准类型内建函数**

- cmp(obj1,obj2)
- repr(obj)
- str(obj)
- type(obj)
- isinstance(obj)

## 2.6 类型工厂函数

自从 python 统一了类型和类，所有的内建函数现在页都是类，原来所谓内建转换函数像 int()，type()，list() 等，现在都称了工厂函数。也就是说虽然它们看上去有点像是函数，实质上是类。当你调用它们时，实际上时生成该类型的一个实例，就像工厂生产货物一样。

## 2.7 标准类型的分类

标准类型也可以将它们成为 python 的“基本内建数据对象原始类型”。

- “基本”是指这些类型都是 python 提供的标准或核心类型。
- “内建”是由于这些类型是 python 默认就提供的。
- “数据”是因为他们用于一般数据存储。
- “对象”是因为对象是数据和功能的默认抽象。
- “原始”是因为这些类型提供的是最底层的粒度数据存储。
- “类型”是因为他们就是数据类型。

不过，上面这些描述实际上并没有告诉你每个类型如何工作，以及它们能发挥什么作用。下面是基于数据的存储、更新、访问三个方面对标准类型进行了一个分类，希望能提供一些简单直观的印象。

**标准类型分类**

|数据类型|存储模型|更型模型|访问模型|
|:---:|:---:|:---:|:---:|
|数字|标量|不可更改|直接访问|
|字符串|标量|不可更改|直接访问|
|列表|容器|可更改|顺序访问|
|元组|容器|不可更改|顺序访问|
|字典|容器|可更改|映射访问|
