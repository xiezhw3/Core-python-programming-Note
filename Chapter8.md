# 条件和循环
### 三元操作符
语法为：

    X if C else Y

## for 语句
### 用于迭代器类型
用 for 循环访问迭代器和访问序列的方法差不多. 唯一的区别就是 for 语句会为你做一些额外的事情. 迭代器并不代表循环条目的集合.

迭代器对象有一个 next() 方法, 调用后返回下一个条目. 所有条目迭代完后, 迭代器引发一个 StopIteration 异常告诉程序循环结束. for 语句在内部调用 next() 并捕获异常


### xrange() 内建函数
xrange() 类似 range()，不过当你有一个很大范围的列表时，xrange() 可能更为适合，因为它不会在内存里创建列表的完整拷贝。它只被用在 for 循环中，在 for 循环外使用它没有意义。它的性能远高出 range()，因为它不生成整个列表。

## 迭代器和 iter() 函数
迭代器为类序列对象提供了一个类序列的接口，python 的迭代无缝地支持序列对象，而且它还允许程序员迭代非序列类型，包括用户定义的对象。

### 如何迭代？
根本上说，迭代器就是有一个 next() 方法的对象，而不是通过索引来计数。当你或是一个循环机制需要下一个项时，调用迭代器的 next() 方法就可以获得它。条目全部取出后，会引发一个 StopIteration 异常，这并不代表错误发生，只是告诉外部调用者，迭代完成。

reversed() 内建函数将返回一个反序访问的迭代器. enumerate() 内建函数同样也返回迭代器. any() 和 all() , 如果迭代器中某个/所有条目的值都为布尔真时,则它们返回值为真. 本章先前部分我们展示了如何在 for 循环中通过索引或是可迭代对象来遍历条目. 同时 Python 还提供了一整个 itertools 模块, 它包含各种有用的迭代器.

### 使用迭代器

    >>> myTuple = (123, 'xyz', 45.67)
    >>> i = iter(myTuple)
    >>> i.next()
    123
    >>> i.next()
    'xyz'
    >>> i.next()
    45.67
    >>> i.next()
    Traceback (most recent call last):
    File "", line 1, in ?
    StopIteration

文件对象生成的迭代器会自动调用 readline() 方法. 这样, 循环就可以访问文本文件的所有行. 程序员可以使用 更简单的 for eachLine in myFile 替换 for eachLine in myFile.readlines()

## 列表解析
列表解析( List comprehensions, 或缩略为 list comps  ) 来自函数式编程语言 Haskell . 它 是一个非常有用, 简单, 而且灵活的工具, 可以用来动态地创建列表

列表解析的语法：

    [expr for iter_var in iterable]

这个语句的核心是 for 循环，它迭代 iterable 对象的所有条目。前边的 expr 应用于序列的每个成员，最后的结果值是该表达式的列表。迭代变量并不需要是表达式的一部分。

结合 if 语句，列表还提供了一种扩展语法：

    [expr for iter_var in iterable if cond_expr]

===矩阵样例===

    >>> [(x+1,y+1) for x in range(3) for y in range(5)]
    [(1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (2, 1), (2, 2), (2,
    3), (2, 4), (2, 5), (3, 1), (3, 2), (3, 3), (3, 4), (3, 5)]

## 生成器表达式
列表解析的一个不足就是必要生成所有的数据, 用以创建整个列表. 这可能对有大量数据的迭 代器有负面效应. 生成器表达式通过结合列表解析和生成器解决了这个问题.

生成器表达式与列表解析非常相似,而且它们的基本语法基本相同; 不过它并不真正创建数字列表, 而是返回一个生成器,这个生成器在每次计算出一个条目后,把这 个条目“产生”(yield)出来. 生成器表达式使用了"延迟计算"(lazy evaluation), 所以它在使用内存上更有效.

列表解析:

    [expr for iter_var in iterable if cond_expr]

生成器表达式:

    (expr for iter_var in iterable if cond_expr)
