# 第七章 函数式编程——列表推导和生成器表达式

标签（空格分隔）： python 会python就够了

---

> Python 提供了一种精炼的写法，可以根据一份列表来制作另一份。这种表达式称为 list comprehension（列表推导）。另外，还有一种类似的结构，叫做生成器表达式（generator expreesion），它的工作方式是**每次处理一个对象，而不是一口气处理和构造整个数据结构，可以节省大量内存**。它们来自函数式编程语言 Haskell。当然，Python 不是也不大可能会成为一种函数式编程语言，但它支持许多有价值的函数式编程语言的构建。也有些表现得像函数式编程机制但是从传统上也不能被认为是函数式编程语言的构建。Python提供了四种内建函数apply()、filter()、map()、reduce()和 lambda 表达式的形式出现。**但如务必要，请使用列表推导和生成器表达式。**

## 7.1 匿名函数与 lambda

基本语法

```bash
lambda [arg1[, arg2[, ...argN]: expression
```

示例：

```bash
def add(x,y): return x+y <=> lambda x,y: x + y
```

```bash
>>> a = lambda x, y=2: x+y
>>> a(10)
12
>>> a(10,20)
30
>>> a(0)
2
>>> a(0, 20)
20
>>> b = lambda *z:z
>>> b(16, u'xyz')
(16, u'xyz')
>>> b(26)
(26,)
>>> 
```

## 7.2 内建函数apply()、filter()、map()、reduce()

- apply()

这个函数将逐步被淘汰。

- filter()

下面实例将演示“**用列表推导来取代 filter**” 的过程。

```bash
# /usr/bin/env python 
# -*- coding:utf-8 -*-
__blog__ = 'http://www.os373.cn'

from random import randint

def odd(n):
    return n % 2

if __name__ == '__main__':
    allNums = []
    for eachNum in range(9):
        allNums.append(randint(1,99))
    print filter(odd, allNums)
```

代码包含两个函数： odd()，确定一个整型是奇数（真）或者偶数（假）Boolean 函数，以及 main()。main() 的目的是用来产生 10 个 1～100 的随机数，然后调用 filter() 来移除掉所有的偶数。

显示结果如下：

```bash
eastossifrage@eastossifrage:~/python codes$ python oddnogen.py 
[39, 61, 35, 77]
eastossifrage@eastossifrage:~/python codes$ python oddnogen.py 
[61, 5, 41, 5]
eastossifrage@eastossifrage:~/python codes$ python oddnogen.py 
[13, 45, 17]
eastossifrage@eastossifrage:~/python codes$ python oddnogen.py 
[81, 37, 63, 39, 29]
eastossifrage@eastossifrage:~/python codes$ python oddnogen.py 
[29, 73, 37, 69]
eastossifrage@eastossifrage:~/python codes$ vim oddnogen.py 
```

1、 进行第一次重构

由于 odd() 函数非常简单，以至于能用一个 lambda 表达式来替代：

```bash
# /usr/bin/env python 
# -*- coding:utf-8 -*-
__blog__ = 'http://www.os373.cn'

from random import randint


if __name__ == '__main__':
    allNums = []
    for eachNum in range(9):
        allNums.append(randint(1,99))
    print filter(lambda n: n%2, allNums)
```

2、 进行第二次重构

用 list 列表来代替 filter()：

```bash
# /usr/bin/env python 
# -*- coding:utf-8 -*-
__blog__ = 'http://www.os373.cn'

from random import randint


if __name__ == '__main__':
    allNums = []
    for eachNum in range(9):
        allNums.append(randint(1,99))
    print [n for n in allNums if n%2]
```

3、第三次重构

由于列表推导比内建函数 map() 和 filter() 的语法更加清晰，无需编写额外的 lambda 表达式，所以建议使用列表推导来取代 map 和 filter。

```bash
# /usr/bin/env python 
# -*- coding:utf-8 -*-
__blog__ = 'http://www.os373.cn'

from random import randint as ri


if __name__ == '__main__':
    print [ n for n in [ri(1,99) for i in range(9)] if n%2]
```

- map()

map 是将函数调用“映射”到每一个序列的元素上，并且返回一个含有所有返回值的列表

```bash
>>> map((lambda x: x+2), range(6))
[2, 3, 4, 5, 6, 7]
>>> map((lambda x: x**2), range(6))
[0, 1, 4, 9, 16, 25]
```

用**列表推导来代替 map()**：

```bash
>>> [ x+2 for x in range(6)]
[2, 3, 4, 5, 6, 7]
>>> [ x**2 for x in range(6)]
[0, 1, 4, 9, 16, 25]
>>> ( x**2 for x in range(6))  # 生成器表达式
<generator object <genexpr> at 0x7f5e81893e10>
```

- reduce()

形象化 reduce ，就如同下面的例子：

```bash
reduce(func, [1, 2, 3, 4]) <=> func( func( func(1, 2), 3), 4)
```

示例：

```bash
>>> print u'总数是：%s' % reduce((lambda x,y: x+y), range(6))
总数是：15
```

上述例子的 reduce 进行了如下的算术操作：

```bash
(((((0+1) +2) +3) +4) +5) <=> 15
```

## 7.3 列表推导和生成器表达式

### 7.3.1 一般语法

- 列表推导

```bash
[expr for iter_var in iterable if cond_expr]
```

- 生成器表达式

```bash
(expr for iter_var in iterable if cond_expr)
```

### 7.3.2 为什么使用列表推导或生成器表达式

- 列表推导要比内建的 map 和 filter 函数清晰，因为它无需额外编写 lambda 表达式。
- 列表推导可以跳过输入列表中的某些元素，如果改用 map 来做，那就必须辅以 filter 方能实现。
- 字典于集合也支持推导表达式。
- 列表推导的一个不足就是必须生成所有的数据，用以创建整个列表。这可能对有大数据的迭代器有负面效应。因此使用生成器表达式，可以很好的解决这个问题，它能构架有效的使用内存。

一般情况下，对大数据两的**磁盘文件的读取**，请采用生成器表达式，会比列表推导的方式更加节省内存，非常环保。


示例如下:

```bash
>>> data = ['藕丝空间', '藕丝科技', '原来你也在这里', 'www.os373.cn', 'eastossifrage']
>>> sum([len(word) for word in data])
70
>>> sum(len(word) for word in data)
70
```







