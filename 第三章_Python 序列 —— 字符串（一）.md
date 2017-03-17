# 第三章 Python 序列 —— 字符串（一）

标签（空格分隔）： python 会python就够了

---

> python 类型中的字符串、列表和元组，有一个共同点就是——它们的成员是有序排列的，它们的每一个元素可以通过指定的偏移量的方式得到，也就是所谓的切片方式。拥有这类特性的 python 类型，我们统称为序列。

## 3.1 序列

python 的序列还要涉及到一个crud的概念，就是把序列当作一个持久层，可以对其进行**增加(Create)、读取查询(Retrieve)、更新(Update)和删除(Delete)**操作。

### 3.1.1 序列类型操作符

一般情况下，**标准类型操作符**适用于所有的序列类型。当然，说这样的话还需要有所保留，下面会按照优先级从高到底的顺序列出适合序列类型的操作符。

|序列操作符|作用|
|---|---|
|seq[index]|获得下下标为 index 的元素|
|seq[index1:index2]|获得下标从 index1 到 index2 间的元素集合|
|seq * expr|序列重复 expr 次|
|seq1 + seq2|连接序列 seq1 和 seq2 |
|obj in seq| 判断 obj 元素是否包含在 seq 中|
|obj not in seq| 判断 obj元素是否不包含在 seq 中|

### 3.1.2 内建函数（BIF）

序列类型也属于“可迭代对象”，序列本身就包含有迭代的概念，因为迭代这个概念就是从序列、迭代器或者其它支持迭代操作的对象中泛化得来的。

**序列类型转换工厂函数**

|函数|含义|
|:---:|---|
|list(iter)|把可迭代对象转换为列表|
|str(obj)|把 obj 对象转换称字符串（对象的字符串表示法）|
|unicode(obj)|把对象转换称 Unicode 字符串（使用默认编码）|
|basestring()|抽象工厂函数，其作用仅仅是为 str 和 unicode 函数提供父类，所以不能被实例化，也不能北调用。|
|tuple(iter)|把一个可迭代对象转换成一个元组对象。|

**序列类型可用的内建函数**

|函数名|功能|
|:---:|---|
|enumerate(iter)|接受一个可迭代对象作为参数，返回一个 enumerate 对象（同时也是一个迭代器），该对象生成由 iter 每个元素的 index 值和 item 值组成的元组。|
|len(seq)|返回 seq 的长度|
|max(iter, key=None) or max(arg0, arg1,...,key=None)|返回iter或（ arg0, arg1,...) 中的最大值，如果指定了key， 这个 key 必须是一个可以传给 sort() 方法的，用于比较的回调函数。|
|min(iter, key=None) or min(arg0, arg1,...,key=None)|返回iter或（ arg0, arg1,...) 中的最小值，如果指定了key， 这个 key 必须是一个可以传给 sort() 方法的，用于比较的回调函数。|
|reversed(seq)|接受一个序列作为参数，返回一个以逆序访问的迭代器。|
|sorted(iter, func=None,key=None,reverse=False)|接受一个可迭代对象作为参数，返回一个有序的列表；可选参数func, key 和 reverse 的含义跟 ilst.sort()内建函数的参数含义一样。|
|sum(seq, init=0)|返回 seq 和可选参数 init 的总和，其效果等同于 reduce(operator.add,seq,init)。|
|zip([iter0,iter2,...itN])|返回一个列表，其第一个元素是iter0, iter1...这些元素的第一个元素组成的一个元组，第二个...以此类推|


## 3.2 字符串

字符串是每个编程语言的基础，字符串类型是 python 里面最常见的类型，是不可变类型，就是说改变一个字符串的元素需要新建一个字符串，字符串是由独立的字符组成的，并且这些字符可以通过**切片操作顺序地访问**。今后的正则表达、爬虫技术等对字符串的处理能力要求较高。

通常意义的字符串（str）和 Unicode 字符串（unicode）都是抽象类 basestring 的子类。这个 basestring 表示不能实例化的。

```bash
>>> basestring('abs')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: The basestring type cannot be instantiated
>>> 
```

### 3.2.1 字符串的 CRUD 操作

- 创建和赋值

```bash
>>> a = 'abcdef'
```

- 访问字符串的值（字符和子串）

```bash
>>> a[0]
'a'
>>> a[1:4]
'bcd'
>>> a[::2]
'ace'
>>> 
```

- 改变字符串

```bash
>>> a = a[3:] + 'update'
>>> print a
defupdate
>>> 
```

- 删除字符和字符串

```bash
>>> a = ''
>>> print a 

>>> del a
>>> print a
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'a' is not defined
```

在大部分应用程序里，没有必要显式的删除字符串。定义这个字符串的代码最终会结束，那时 python 会自动释放这些字符串。

### 3.2.2 字符串和操作符

- 标准类型操作符

```bash
>>> str1 = 'ousikongjian'
>>> str2 = 'eastossifrage'
>>> str3 = 'xyz'
>>> str1 < str2
False
>>> str1 > str2
True
>>> str2 != str3
True
>>> str1 < str2 and str3 == 'xyz'
False
>>> 
```

做比较操作的时候，字符串是按照 ASCII 值的大小来比较的。

- 序列操作符切片

1. 正向索引
2. 反向索引
3. 默认索引

以字符串 `abcdef` 为例。分别列出了使用正索引和负索引来定位字符的情况。

![001.png-8.1kB][1]

先用长度操作符来确认该字符串的长度为6。

```bash
>>> str = 'abcdef'
>>> len(str)
6
```

正向索引时，索引值开始于 0 ，结束于长度减 1（因为我们时从 0 开始索引的）。

在这个范围内[start:end]，我可以访问到包括 start 在内到 end（不包含 end）的所有字符。可以这么说，假设 x 是[start:end] 中的一个索引值，那么有 `start<=x<end`。

```bash
>>> str[0]
'a'
>>> str[2:6]
'cdef'
>>> str[6]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

使用不在允许范围内的索引值会导致错误。直接那字符串的长度来作为索引访问是不被允许的，但是 start 或 end 的值同时设定的时候，可以超出范围。

在进行反向索引时，时从 -1 开始，向字符串开始的方向计数，到字符串长度的负数为索引的结束。

```bash
>>> str[2:6]
'cdef'
>>> str[2:7]
'cdef'
>>> str[-1]
'f'
>>> str[-1:-4]
''
>>> str[-4:-1]
'cde'
>>> str[-4:]
'cdef'
>>> str[-6:]
'abcdef'
>>> str[-6]
'a'
>>> str[:]
'abcdef'
```

如果开始索引和结束索引没有被指定，则分别以字符串的第一个和最后一个索引值为默认值。

- 性能问题

一般情况下，从性能的角度来考虑，把重复操作作为参数放到循环里面进行时非常低效的。

```bash
while i > len(str):
    print '超出范围'
```

上面的循环操作把大把的时间都浪费到了重复计算字符串 str 的长度上了。每次循环迭代都要运行一次这个函数。**如果把这个值做一次保存，我们就可以用更为高校的方法重写我们的循环操作**。

```bash
length = len(str)
while i > length:
    print '超出范围'
```

### 3.3.3 字符串特有的操作符

- 格式化操作符（%）

**字符串格式化符号**

|格式化字符|转换方式|
|---|:---|
|%c|转换称字符（ASCII码值，或者长度为一的字符串）|
|%r|优先用 repr() 函数进行字符串转换|
|%s|优先用 str() 函数进行字符串转换|
|%d / %i|转换成有符号十进制数|
|%u|转换成无符号十进制数|
|%o|转换成无符号八进制数|
|%x / %X|转换成无符号十六进制（x/X代表转换后的十六进制字符的大小写）|
|%e / %E|转换成科学计数法（e/E控制输出e/E）|
|%f / %F|转换成浮点型（小数部分自然截断）|
|%g / %G|%e 和 %f%E 和 %F 的简写|
|%%|输出%|

**格式化操作辅助指令**

|符号|作用|
|:---:|---|
|*|定义宽度或者小数点精度|
|-|用作左对齐|
|+|在正数前面显示加号（+）|
|`<sp>`|在正数前面显示空格|
|#|在八进制数前面显示零（'0'），在十六进制前面显示'0x'或者‘0X'|
|0|显示的数字前面填充'0'而不是默认的空格|
|%|'%%'输出一个单一的'%'|
|(var)|映射变量（字典参数）|
|m.n|m是显示的最小总宽度，n是小数点后的位数|


- 字符串模板

string 模块由于新式的字符串 Template 对象的引进，又重新活了过来，Template 对象有两个方法，substitute()和safe_substitute()。前者更为严谨，在 key 缺少的情况下会报一个 KeyError 的异常出来，而后者在缺少 key 时，直接原封不动的把字符串显示出来。

```bash
>>> from string import Template
>>> s = Template('欢迎${name}来到${company}!')
>>> print s.substitute(name='东方鹗',company='藕丝空间')
欢迎东方鹗来到藕丝空间!
>>> print s.substitute(company='藕丝空间')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/lib/python2.7/string.py", line 176, in substitute
    return self.pattern.sub(convert, self.template)
  File "/usr/lib/python2.7/string.py", line 166, in convert
    val = mapping[named]
KeyError: 'name'
>>> print s.safe_substitute(company='藕丝空间')
欢迎${name}来到藕丝空间!
>>> 
```

- 原始字符串操作符（r/R）

关于原始字符串的目的就是为了对付那些在字符串中出现的特殊字符。

```bash
>>> '\n'
'\n'
>>> print '\n'


>>> print r'\n'
\n
>>>
```


### 3.2.4 内建函数

- 标准类型函数  cmp()
- 序列类型函数 len() max() min() enumerate() zip()
- 字符串类型函数

raw_input()

```bash
>>> input = raw_input('请输入您的名字：')
请输入您的名字：东方鹗
>>> input
'\xe4\xb8\x9c\xe6\x96\xb9\xe9\xb9\x97'
>>> print input
东方鹗
>>> len(input)
9
>>>
>>> print input[0:2]
��
>>> print input[0:3]
东
>>> print input[0:5]
东��
>>> print input[0:6]
东方
>>> print input[6:]
鹗
>>> 
```

str() 和 unicode()

略

chr()、unichr() 和 ord()

chr()函数用一个范围在 256 内的正数作为参数，返回一个对应的字符。unichr() 跟它一一，只不过返回的是 Unicode 字符。如果是配置为 USC2 的 Unicode ，那么它的范围是 65536 或者 0x0000-0xFFFF；如果是配置为 USC4 ,那么它的范围是1114112 或 0x000000-0x110000。

ord()函数是 chr() 函数（对于8位的 ASCII 字符串）或 unichr() 函数（对于 Unicode 对象）的配对函数，它以一个字符（长度为1的字符串）作为参数，返回对应的 ASCII 数值，或者 Unicode 数值。

```bash
>>> ord('A')
65
>>> chr(65)
'A'
>>> 
```

### 3.2.5 字符串内建函数

**字符串类型的内建方法**

|方法|描述|
|---|---|
|string.capitalize()|把字符串的第一个字符大写|
|string.center(width)|返回一个原字符串居中，并使用空格填充至长度 width 的新字符串|
|string.count(str, beg=0, end=len(string))|返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数|
|string.decode(encoding='UTF-8'，error='strict')|以 deconding 指定的编码格式解码 string，如果出错默认报一个 VAlueError 的异常，除非 errors 指定的是 'ignore' 或者 'replace'|
|string.encode(encoding='UTF-8'，error='strict')|以 enconding 指定的编码格式解码 string，如果出错默认报一个 VAlueError 的异常，除非 errors 指定的是 'ignore' 或者 'replace'|
|string.endswith(obj,beg=0,end=len(string))|检查字符串是否以 obj 结束，如果 beg 或者 end 指定则检查指定的范围内是以 obj 结束，如果是，返回 True，否则返回 False。|
|string.expandtabs(tabsize=8)|把字符串 string 中的 tab 符号转换为空格，默认的空格数 tabsize 是 8 |
|string.find(str, beg, end=len(string))| 检测 str 是否包含在 string 中，如果 beg 和 end 指定范围，则检查是否包含在指定范围内，如果是返回索引值，否则返回-1|
|string.index(str, beg, end=len(string))|跟 find() 方法一样，只不过如果 str 不在 string 中会报一个异常|
|string.isalnum()|如果 string 至少有一个字符并且所有字符都是字母或数字则返回 True，否则返回 False。|
|string.isalpha()|如果 string 至少有一个字符并且所有字符都是字母则返回 True，否则返回 False。|
|string.isdecimal()|如果 string 中只包含十进制数字则返回 True，否则返回 False。|
|string.isdigit()|如果 string 中只包含数字则返回 True，否则返回 False。|
|string.islower()|如果 string 中包含至少一个区分大小写的字符，并且所有这些（区分大小写）字符都是小写，则返回 True，否则返回 False。|
|string.isnumeric()|如果 string 中只包含数字字符，则返回 True，否则返回 False。|
|string.issapce()|如果 string 中只包含空格，则返回 True，否则返回 False。|
|string.istitle()|如果 string 是标题化的（title())则返回 True，否则返回 False。|
|string.isupper()|如果 string 中包含至少一个区分大小写的字符，并且所有这些（区分大小写）字符都是大写，则返回 True，否则返回 False。|
|string.join(seq)|以 string 作为分隔符，将 seq 中所有的元素（字符串表示）合并为一个新的字符串|
|string.ljust(width)|返回一个原字符串左对齐，并使用空格填充至长度 width 的新字符串|
|string.lower()|转换 string 中所有大写字符为小写|
|string.lstrip()|截掉 string 左边的空格|
|string.partition(str)|有点像 find() 和 split() 的结合体，从 str 出现的第一个位置起，把字符串 string 分成一个 3 元组（string_pre_str，str，string_post_str），如果 string 中不包含 str ，则 string_pre_str = string。|
|string.replace(str1,str2,num=string.count(str1))|把 string 中的 str1 替换成 str2，如果 num 指定，则替换不超过 num 次。|
|string.rfind(str,beg=0,end=len(string))|类似于 find() 函数，不过是从右边开始查找|
|string.rindex(str,beg=0,end=len(string))|类似于 index(), 不过是从右边开始|
|string.rjust(width)|返回一个原字符串右对齐，并使用空格填充至长度 width 的新字符串。|
|string.rpartition(str)|类似于 partition() 函数，不过是从右边开始查找|
|string.rstrip()|删除 string 字符串末尾的空格。|
|string.split(str="",num=string.count(str))|以 str 为分隔符切片 string，如果 num 有指定值，则仅分隔 num 个子字符串|
|string.splitlines(num=string.count('\n')|按照行分隔，返回一个包含各行作为元素的列表，如果 num 指定则仅切片 num 行。|
|string.startwith(obj,beg=0,end=len(string))|坚持字符串是否是以 obj 开头，是则返回 True，否则返回 False，如果 beg 和 end 指定值，则在指定范围内检查。|
|string.strip([obj])|在 string 上执行 lstrip()和 rstrip()|
|string.swapcase()|翻转 string 中的大小写|
|string.title()|返回“标题化”的 string，也就是说首字母大写，七月均为小写。|
|string.translate(str, del="")|根据 str 给出的表（包含256个字符）转换 string 的字符，要过滤调的字符放在 del 参数中。|
|string.upper()|转换 string 中的小写字母为大写|
|string.zfill(width)|返回长度为 width 的字符串，原字符串 string 右对齐，前面填充0|

translate 实例

```bash
>>> from string import maketrans
>>> t=maketrans('abc','ABC')
>>> s='转换实例，将字符eastossifrage里的小写abc转换成大写,并删除fg'
>>> s.translate(t,'fg')
'\xe8\xbd\xac\xe6\x8d\xa2\xe5\xae\x9e\xe4\xbe\x8b\xef\xbc\x8c\xe5\xb0\x86\xe5\xad\x97\xe7\xac\xa6eAstossirAe\xe9\x87\x8c\xe7\x9a\x84\xe5\xb0\x8f\xe5\x86\x99ABC\xe8\xbd\xac\xe6\x8d\xa2\xe6\x88\x90\xe5\xa4\xa7\xe5\x86\x99,\xe5\xb9\xb6\xe5\x88\xa0\xe9\x99\xa4'
>>> print s.translate(t,'fg')
转换实例，将字符eAstossirAe里的小写ABC转换成大写,并删除
>>> 
```

### 3.2.6 Unicode 

```bash
>>> a = 'ousikongjian' # ASCII 字符串
>>> b = u'ousikongjian' # Unicode 字符串
>>> c = u'%s,%s欢迎您！' % (u'东方鹗', u'藕丝空间')   # 字符串格式化操作
>>> print c
东方鹗,藕丝空间欢迎您！
```

- 字符串编码解码

decode() 和 encode() 内建函数接受一个字符串做参数返回该字符串对应的解码后/编码后的字符串。decode() 和 encode() 都可以应用于常规字符串和 Unicode 字符串。

根据个人经验，一般有四种情况。

 1. string.decode('gbk')
 2. string.decode('utf-8')
 3. string.encode('gbk')
 4. string.encdoe('utf-8')

以上四种情况的总结可能不够严谨，请按照自己的实际情况执行。


  [1]: http://static.zybuluo.com/ossifrage/q3ondbilixul1vqa15l0hm1f/001.png
