# 第一章 我和 Python 有个约定

---

> 车同轨，书同文，有了规矩好办事！

## 1.1 编程模式

### 1.1.1 交互模式编程：

调用解释器不经过脚本文件作为参数，显示以下提示：

```bash
$ python
Python 2.7.11+ (default, Apr 17 2016, 14:00:29) 
[GCC 5.3.1 20160413] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

键入下列文字在 Python 提示符，然后按 Enter 键：

```bash
>>> print "Hello, World!"
```

显示结果如下：

```bash
Hello, World!
```

### 1.1.2 脚本模式编程：

调用解释器及脚本作为参数，并开始执行的脚本，并一直持续到脚本完成。当脚本完成时，解释器不再是活动的。

让我们在脚本中编写一个简单的Python程序。所有的Python文件将具有.py扩展。所以，把下面的代码写在一个test.py文件。

```bash
# -*- coding:utf-8 -*-
__author__ = '东方鹗'

print "Hello, World!"
```

在 ubuntu 16.04 系统中，`python`已经在环境变量中设置，表示启动 `python 2`编译器, `python3`则表示启动 `python 3`编译器。执行如下命令：

```bash
$ python test.py
```

显示结果如下：

```bash
Hello, World!
```

还有一种方法，是赋予 test.py 文件执行权限。但需要修改源文件：

```bash
#!/usr/bin/python

print "Hello, Python!"
```

在这里，假设 Python 解释器在 /usr/bin 目录中可用,你也可以使用 `whereis python` 命令，查找 Python 的文件路径。现在，尝试如下运行这个程序：

```bash
$ chmod +x test.py     # 赋予文件执行权限
$./test.py
```

### 1.1.3 编程模式的约定

个人习惯，交互模式适合进行一下简单的代码调试，记住是，简单的调试；但脚本模式可以让你带着梦想去翱翔。因此**，在此提出一个约定，如无必要，我们一定使用脚本模式来进行编程**。


## 1.2 编程环境

Python 提供了丰富的第三方库，如果需要，可以随时安装第三方库，但是如果你又多个项目，并且都在全局 Python 环境直接安装的话，会造成包的混乱和版本冲突。为了解决这个问题，**在此提出一个约定，每一个项目都要有自己的虚拟环境**。

### 1.2.1 建立虚拟环境

请参阅本人的另一篇博文 [《第一章 使用 flask 虚拟环境》](http://www.os373.cn/article/1)。

虚拟环境使用第三方实用工具 virtualenv 创建。输入以下命令可以检查系统是否安装了virtualenv:

```bash
$ virtualenv --version
```

如果结果显示错误,你就需要安装这个工具。
安装命令:

```bash
$ sudo apt-get install python-virtualenv
```

下一步是在项目的目录下创建 Python 虚拟环境。

```bash
$ cd /opt
$ sudo mkdir test # 建立项目目录，可以自行命名目录
$ sudo chown xxpost:xxpost -R test # xxpost 为系统当前用户
$ cd test
$ virtualenv env # env 为 Python 的虚拟解释器环境
New python executable in env/bin/python
Installing setuptools, pip...done.
```

现在 test 文件夹下有一个名为 env 的子文件夹,它保存了一个全新的虚拟环境,其中有一个私有的 Python 解释器。在使用之前,你需要先将其“激活”。在 Ubuntu16.04 下使用bash shell 命令行:

```bash
$ source env/bin/activate
```

虚拟环境被激活后,其中 Python 解释器的路径就被添加进 PATH 中,但这种改变不是永久性的,它只会影响当前的命令行会话。激活后的命令提示符,加入环境名:

```bash
(env)$
```

如果你想回到局 Python 解释器中,可以在命令提示符下输入deactivate。

```bash
(env)$ deactivate
```
### 1.2.2 使用 pip 安装 Python 包

以 Flask 第三方库为例子。
在虚拟环境中安装 Flask:

```bash
(env)$ pip install flask
```
想要验证 Flask 是否安装正确,你可以启动 Python 解释器,尝试导入 Flask:

```bash
(env)$ python
>> import flask
>>
```

如果没有看到错误提醒,那么恭喜您,你已经完成基础环境的搭建了。

### 1.2.3 执行脚本

执行脚本时，一定要先激活虚拟空间。以以下方式执行：

```bash
(env)$ python ***.py
```

(env) 表示已经激活虚拟环境，python 是虚拟环境的解释器。

## 1.3 脚本头部

在此，我们约定每个脚本开始的时候要写入以下内容：

```bash
# -*- coding:utf-8 -*-
__author__ = '东方鹗'
```

第一行表示该脚本使用 utf-8 编码，第二行表示脚本的版权，即作者名称。

## 1.4 注释

### 1.4.1 单行注释（# ）

和很多 Uinx 脚本类似，Python 的注释是从 # 字符开始的，注释可以在一行的任意地方开始，解释器会忽略掉改行 # 之后的所有内容。**在此约定，单行注释，要以 # 加空格开始。**

### 1.4.2 多行注释（'''）
对多行进行注释有一个简便的方法就是使用三个单引号 `'''` 将要注释几行代码包含在内，比如：

```bash
# -*- coding:utf-8 -*-
__author__ = '东方鹗'

'''
if True:
    print "True"
else:
    print "False"
'''
```
但是，三个单引号`'''`也用来表示字符串内容，这样将对 `obj.__doc__` 造成污染，因此，**强烈建议只在代码调试时为了简便而使用多行注释，如无必要，不要使用这样的方法**。

## 1.5 Python 标识符

Python 标识符是用来标识一个变量，函数，类，模块或其他对象的名称。一个标识符开始以字母A到Z或a〜z或后跟零个或多个字母下划线（_），下划线和数字（0〜9）。

Python 中标识符内不允许标点符号，如@，$和％。 Python 是一种区分大小写的编程语言。因此，Manpower  和 manpower 在 Python 中是两个不同的标识符。

这里有Python标识符命名约定：

- 类名以大写字母以及所有其它标识符以小写字母。
- 开头单个前导下划线的标识符表示由该标识符约定意思是私有的。
- 开头两个前导下划线的标识符表示一个强烈的私有的标识符。
- 如果标识符末尾还具有两个下划线结束时，该标识符是一个语言定义的特殊名称。
- 变量命名可以使用“驼峰”命名规则，有两种方式，比如“changeName”和“change_name”，建议使用**每个单词之间使用下划线**的规则。
- 变量，类，函数命名要严禁使用**保留字**。

## 1.6 行和缩进

一个程序员学习Python时，遇到的第一个需要注意的地方是，不使用括号来表示代码的类和函数定义块或流程控制。代码块是由行缩进，这是严格执行表示方式。如果没有严格执行缩进，执行会报错。
缩进位的数目是可变的，但是在块中的所有语句必须缩进相同的量。**在此，我们约定在所有脚本中每行的每一个缩进都是四个“空格”。**

## 1.7 继续 （\）

Python语句通常用一个新行结束。 但是，**Python允许使用续行字符（\）来表示，该行应该继续下去（跨行**）。例如：

```bash
articles = Article.query.join(TagSpaces, TagSpaces.tag_id == tag.id).filter(TagSpaces.article_id == Article.id). \
        order_by(Article.timestamp.desc()). \
        paginate(page, per_page=current_app.config['OUSI_POSTS_PER_PAGE'], error_out=False)
```

包含在[]，{}，() 或 """，'''的陈述不需要使用续行符。

## 1.8 空格使用

空格除了要在注释符 # 后约定使用之外，在赋值和判断的时候也需要空格。例如：

```bash
mesg = u'注意降温'
if (weather_is_hot == 1) and \
    (shark_warnings == 0):
    send_goto_beach_mesg_to_pager(mesg=mesg)
```

`mesg = u'注意降温'` 变量赋值， `=` 两侧加上空格；`weather_is_hot == 1` 条件判断， 条件判断符 `==`，`！=` 不管是否在括号内， 两侧都要加上空格。`send_goto_beach_mesg_to_pager(mesg=mesg)` **括号内的变量赋值必须去掉 `=` 两侧的空格**。

## 1.9 在一行中多个语句（；）

分号( ; ) 允许在单行写入多条语句，不管语句是否启动一个新的代码块。下面是使用分号示例：

```bash
import sys; x = 'foo'; sys.stdout.write(x + ' ')
```

为了程序的可读性，在此约定，在使用**脚本模式**时，如无必要，严格禁止使用分号（；），禁止在一行中多个语句。

## 1.10 模块

每一个 python 脚本文件都可以被当作一个模块。模块里的代码可以是一段直接执行的脚本，也可以是一堆类似于库函数的代码，从而可以被别的模块导入（import）调用。

### 1.10.1 模块结构和布局

```bash
# -*- coding:utf-8 -*-
__author__ = '东方鹗'   # （1） 起始行


"""
这是一个测试模块
"""                    # （2）模块文档（文档字符串）

import sys
import os              # （3）模块导入

debug = True           # （4）变量定义（全局）

class FooClass(object):
    """
    类 Foo
    """
    pass               # （5）类定义

def test():
    """
    函数 test
    """                # （6）函数定义

if __name__ == '__main__':
    test()             # （7）主程序
```

（1） 起始行

我们脚本模式编程的一个约定。

（2）模块文档（文档字符串）

简要介绍模块的功能及重要全局变量的定义，模块外可通过 `module.__doc__` 访问这些内容。

（3）模块导入

导入当前模块的代码需要的所有模块：每个模块仅导入一次（当前模块被加载时）；函数内部的模块代码不会被执行，除非该函数正在执行。

（4）变量定义（全局）

这里定义全局变量，本模块中的所有函数可以直接使用。从好的编程风格角度来说，除非必要，否则就尽量使用局部变量代替全局变量，如果坚持这样做，你的代码不但容易维护，而且还可以提高性能并节省内存。

（5）类定义

所有的类都在这里定义。当模块被导入时 class 语句会被执行，类也就被定义。类的文档变量是 `class.__doc__`。

（6）函数定义

此处定义的函数可以通过module.function()在外部被访问到，当模块被导入时 def 语句会被执行，函数页就会定义好，函数的文档变量是 `function.__doc__`。

（7）主程序

无论这个模块是否被别的模块导入还是作为脚本直接执行，都会执行这部分代码。通常这里不会有太多功能性代码，而是根据执行的模式调用不同的函数。


更多关于 Python 风格的规范，请参阅 ： <a class="btn btn-primary" href="http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/python_style_rules/"> Python风格规范 </a>
