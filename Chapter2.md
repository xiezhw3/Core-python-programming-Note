# pytohn 基础特性
### 程序输出
%s 表示由一个字符串替换，%d 表示由一个整数来替换，%f 表示由浮点数来替换

    >>> print "%s is number %d!" % ("Python", 1)
    Python is number 1!

### 程序输入
从用户那里得到数据输入的最容易的方法是使用 raw_input()内建函数。它读取标准输入,
并将读取到的数据赋值给指定的变量。

    >>> user = raw_input('Enter login name: ')
    Enter login name: root

### 运算符
/ 和 // 都表示除法，// 用做浮点除法，对结果进行四舍五入。而 / 进行传统的除法

\*\* 表示乘方

Python 不支持 C 语言中的自增 1 和自减 1 运算符, 这是因为 + 和 - 也是单目运算符, Python 会将 --n 解释为-(-n) 从而得到 n , 同样 ++n 的结果也是 n

### 列表循环
你可以在一行中使用一个 for 循环将所有值放到一个列表当中

    >>>squared = [x ** 2 for x in range(4)]
    >>>for i in squared:
    ...    print i
    0
    1
    4
    9

### 文件和内建函数 open()、file()
file() 内建函数是最近才添加到 Python 当中的。它的功能等同于 open()，不过 file() 这个名字可以更确切地表达它是个工厂函数。（生成文件对象类似 int() 生成整数对象，dict() 生成字典对象。

### 类
\_\_init\_\_() 方法有一个特殊名字, 所有名字开始和 结束都有两个下划线的方法都是特殊方法。

当一个类实例被创建时，\_\_init\_\_() 方法会自动执行，在实例创建完毕后执行，类似构建函数。\_\_init\_\_() 可以被当成构建函数，不过不像其他语言中的构建函数，它并不创建实例--它仅仅是你的对象出那个键后执行的第一个方法。它的目的是执行一些该对象的必要初始化工作。通过创建自己的 \_\_init\_\_()  方法，你可以覆盖默认的 \_\_init\_\_() 方法（默认的 \_\_init\_\_() 方法深也不做），从而能够修饰刚刚创建的对象。

### 模块
模块是一种组织形式，它将彼此有关系的 Python 代码组织到一个个独立文件中。


### 实用的函数

|函数|描述|
|:--|:--
|dir([obj])| 显示对象的属性，如果没有提供参数，则显示全局变量的名字
|type(obj)|返回对象的类型（返回值本身也是一个 type 对象

