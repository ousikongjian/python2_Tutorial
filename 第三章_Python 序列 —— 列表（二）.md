# 第三章 Python 序列 —— 列表（二）

标签（空格分隔）： python 会python就够了

---

## 3.3 列表

像字符串类型一样，列表类型也是序列式的数据类型，可以通过下标或者前片操作来访问某一个或者某一块连续的元素。然而，相同的地方也就这些，字符串只能由字符组成，而且是不可便的（不能单独改变它的某个值），而列表则是能保留任意树木的 Python 对象的灵活的容器。就像我们将要看到的例子中所示，创建列表非常简单，像列表中添加元素即可。

### 3.3.1 列表的 CRUD 操作

- 创建列表类型数据并给它赋值

```bash
>>> list1 = [123, 'abc', u'3.14', [456, 'xdt'], 2-1j]
>>> list2 = [None, u'藕丝科技']
>>> print list1
[123, 'abc', u'3.14', [456, 'xdt'], (2-1j)]
>>> print list2
[None, u'\u85d5\u4e1d\u79d1\u6280']
>>> list2 = []
>>> print list2
[]
>>> list(u'藕丝科技')
[u'\u85d5', u'\u4e1d', u'\u79d1', u'\u6280']
>>> 
```

- 访问列表中的值

```bash
>>> list1[1]
'abc'
>>> list1[2:4]
[u'3.14', [456, 'xdt']]
>>> list2[3:]
[]
>>> list1[3:]
[[456, 'xdt'], (2-1j)]
>>> list1[3][1]
'xdt'
```

- 更新列表

```bash
>>> list1
[123, 'abc', u'3.14', [456, 'xdt'], (2-1j)]
>>> list1[2]
u'3.14'
>>> list1[2] = u'PI'
>>> list1
[123, 'abc', u'PI', [456, 'xdt'], (2-1j)]
>>> list1.append(u'新增元素')
>>> list1
[123, 'abc', u'PI', [456, 'xdt'], (2-1j), u'\u65b0\u589e\u5143\u7d20']
>>> print list1
[123, 'abc', u'PI', [456, 'xdt'], (2-1j), u'\u65b0\u589e\u5143\u7d20']
>>> 
```

- 删除列表中的元素或者列表（本身）

```bash
>>> list1
[123, 'abc', u'PI', [456, 'xdt'], (2-1j), u'\u65b0\u589e\u5143\u7d20']
>>> del list1[0]
>>> print list1
['abc', u'PI', [456, 'xdt'], (2-1j), u'\u65b0\u589e\u5143\u7d20']
>>> list1.remove(u'PI')
>>> print list1
['abc', [456, 'xdt'], (2-1j), u'\u65b0\u589e\u5143\u7d20']
>>> 
```

### 3.3.2 列表类型操作符

- 标准类型操作符

 `>，<, ==, !=, and, or`

- 序列类型操作符

1. 切片（ [] ）
2. 成员关系操作（ in, not in ）
3. 连接操作符（ + ）
4. 重复操作符（ * )

- 列表类型操作符和列表推导

```bash
>>> matrix = [[1,2,3],[4,5,6],[7,8,9]]
>>> squared = [x**2 for x in row for row in matrix]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'row' is not defined
>>> squared = [[x**2 for x in row] for row in matrix]
>>> print squared
[[1, 4, 9], [16, 25, 36], [49, 64, 81]]
>>> flat = [x for row in matrix]
>>> print flat
[9, 9, 9]
>>> flat = [row for row in matrix]
>>> print flat
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> flat = [x for row in matrix for x in row]
>>> print flat
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> flat = [x for x in row for row in matrix]
>>> print flat
[7, 7, 7, 8, 8, 8, 9, 9, 9]
>>> flat = [row for x in row for row in matrix]
>>> print flat
[[1, 2, 3], [4, 5, 6], [7, 8, 9], [1, 2, 3], [4, 5, 6], [7, 8, 9], [1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> 
>>> 
>>> 
>>> squared = [x**2 for row in matrix for x in row]
>>> print squared
[1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> 
```

### 3.3.3 内建函数

- 标准类型函数 cmp() 
- 序列类型函数 len() max() min() sorted() reversed() enumerate() zip() sum() list() tuple()


### 3.3.4 列表类型内建函数

|列表函数|作用|
|---|---|
|list.append(obj)|向列表添加一个对象 obj|
|list.count(obj)|返回一个对象 obj 在列表中出现的次数|
|list.extend(seq)|把序列 seq 的内容添加到列表中|
|list.index(obj,i=0,j=len(list))|返回 list[k] == obj 的 k 值，别且 k 的范围在 `i <= k < j`；否则会引发 ValueError 异常。|
|list.insert(index, obj)|在索引量为 index 的位置插入对象 obj|
|list.pop(index=-1)|删除并返回指定位置的对象，默认是最后一个对象|
|list.remove(obj)|从列表中删除对象obj|


### 3.3.5 列表的特殊特性

列表有容器和可变的特性，这使得它非常灵活，用它来构建其它的数据结构不是难事。比如说构建堆栈和队列。

这些示例不再赘述。
