# 函数和函数式编程
传统意义上的函数或者“黑盒”, 可能不带任何输入参数,经过一定的处理,最后向调用者传回返回值

而过程是简单,特殊, 没有返回值的函数

## 函数调用
### 函数操作符
同大多数语言相同,我们用一对圆括号调用函数。在 python 中,函 数的操作符同样用于类的实例化。

### 关键字参数
关键字参数的概念仅仅针对函数的调用。这种理念是让调用者通过函数调用中的参数名字来区 分参数。这样规范允许参数缺失或者不按顺序,因为解释器能通过给出的关键字来匹配参数的值。

### 前向引用
和其他高级语言类似,Python 也不允许在函数未声明之前,对其进行引用或者调用.

    def foo():
        print 'in foo()'
        bar()
        def bar():
        print 'in bar()'

这段代码可以非常好的运行,不会有前向引用的问题:

    >>> foo()
    in foo() in bar()

这段代码是正确的因为即使(在 foo()中)对 bar()进行的调用出现在 bar()的定义之前,但 foo() 本身不是在 bar()声明之前被调用的。换句话说,我们声明 foo(),然后再声明 bar(),接着调用 foo(), 但是到那时,bar()已经存在了,所以调用成功。

### 内部/内嵌函数
在函数体内创建另外一个函数(对象)是完全合法的。这种函数叫做内部/内嵌函数


### 函数（与方法）装饰器
装饰器背后的主要动机源自 python 面向对象编程。装饰器是在函数调用之上的装饰。这些装饰仅是当声明一个函数或方法的时候，才会被用户额外调用


装饰器的语法以 @ 开头，接着是装饰器函数的名字和可选的参数。紧跟着装饰器声明的是被修饰的函数，和装饰函数的可选参数。如下：

    @decorator(dec_opt_args)
    def func2Bdecorated(func_opt_args):
        ...

装饰器可以如函数调用一样"堆叠"起来

    @deco2
    @deco1
    def func(arg1, arg2, ...):
        pass

**
有参数和无参数的装饰器**：

没有参数的情况下，一个装饰器如：

    @deco
    def foo():
        pass

非常的直接：

    foo = deco(foo)

然而，带参数的装饰器 decomaker()

    @decomaker(deco_args)
    def foo(): pass

需要自己返回以函数作为参数的装饰器。换句话说，decomaker() 用 deco_args 做了写事并返回函数对象，而该函数对象正是以 foo 作为其参数的装饰器。

    foo = decomaker(deco_args)(foo)

那么，如下的例子：

    @deco1(deco_arg)
    @deco2
    def func(): pass

就等价于：

    func = deco1(deco_arg)(deco2(func))

#### 什么是装饰器
现在我们知道装饰器实际就是函数。我们也知道他们接受函数对象。

## 传递函数
在 python 中，函数就像其他对象一样，因此函数是可以被引用的（访问或者以其他变量作为其别名），也作为参数传入函数，以及作为列表和字典等容器对象的元素。

函数有一个独一无二的特征将它同其他对象区分开来，那就是函数是可调用的。


## 可变长的参数
变长的参数 在函数声明中不是显式命名的,因为参数的数目在运行时之前是未知的(甚至在运行的期间,每次 函数调用的参数的数目也可能是不同的),这和常规参数(位置和默认)明显不同。由于函数调用提供了关键字以及非关键字两种参数类型,python 用两种方法来 支持变长参数。

### 非关键字可变长参数
当函数被调用的时候,所有的形参(必须的和默认的)都将值赋给了在函数声明中相对应的局部变量。

可变长的参数元组必须在位置和默认参数之后,带元组(或者非关键字可变长参数)的函数普 遍的语法如下:

    def function_name([formal_args,] *vargs_tuple):
    "function_documentation_string"
    function_body_suite

星号操作符之后的形参将作为元组传递给函数,元组保存了所有传递给函数的"额外"的参数(匹 配了所有位置和具名参数后剩余的)。如果没有给出额外的参数,元组为空。

    >>> def fun(x1, x2, *x3):
    ...     print x1
    ...     print x2
    ...     for i in x3:
    ...             print 'more', i

### 关键字变量参数（Dictionary）

在我们有不定数目的或者额外集合的关键字的情况中, 参数被放入一个字典中,字典中键为参 数名,值为相应的参数值。

使用了变量参数字典来应对额外关键字参数的函数定义的语法:

    def function_name([formal_args,][*vargst,] **vargsd):
        function_documentation_string
        function_body_suite

为了区分关键字参数和非关键字非正式参数,使用了双星号(\*\*)。\*\*是被重载了的以便不与 幂运算发生混淆

注意，此时的 vargsd 是一个字典

## 函数式编程
### 匿名函数与 lambda
python 允许用 lambda 关键字创造匿名函数。匿名是因为不需要以标准的方式来声明

一个完整的 lambda“语句”代表了一个表达式,这个表达式的定义体 必须和声明放在同一行

    lambda [arg1[, arg2, ... argN]]: expression


### 内建函数 apply()、filter()、map()、reduce()

函数式编程内建函数

|内建函数|描述
|:--|:--
|apply(func[, nkw][, kw])|用可选的参数来调用 func，nkw 为非关键字参数，kw 关键字参数；返回值是函数调用的返回值
|filter(func, seq)|调用一个布尔函数 func 来迭代遍历每个 seq 中的元素；返回一个使 func 返回值为 true 的元素的序列
|map(func, seq1[, seq2...])|将函数 func 作用域给定序列（s）的每个元素，并用一个列表来提供返回值；如果 func 为 None，func 表现为一个身份函数，返回一个含有每个序列中元素集合的 n 个元组的列表
|reduce(func, seq[, init])|将二元函数作用于 seq 序列的元素，每次携带一对（先前的结果以及下一个序列元素），连续的将现有的结果和下一个值作用在获得的随后的结果上，最后减少我们的序列为一个单一的返回值；如果初始 init 给定第一个比较会是 init 和第一个序列元素而不是序列的头两个元素

### 偏函数应用
currying 的概念将函数式编程的概念和默认参数以及可变参数结合在一起。一个带 n 个参数, curried 的函数固化第一个参数为固定参数,并返回另一个带 n-1 个参数函数对象。Currying 能泛化成为偏函数应用(PFA), 这种函数将任意数量(顺 序)的参数的函数转化成另一个带剩余参数的函数对象。

在某种程度上,这似乎和不􏰀供参数,就会使用默认参数情形相似，在 PFA 的例子中, 参数 不需要调用函数的默认值,只需明确的调用集合。你可以有很多的偏函数调用,每个都能用不同的 参数传给函数,这便是不能使用默认参数的原因。

    >>> from operator import add, mul
    >>> from functools import partial
    >>> add1 = partial(add, 1) # add1(x) == add(1, x)
    >>> mul100 = partial(mul, 100) # mul100(x) == mul(100, x) >>>
    >>> add1(10)
    11
    >>> add1(1)
    2
    >>> mul100(10)
    1000
    >>> mul100(500)
    50000

    eg2:
    >>> baseTwo = partial(int, base=2)
    >>> baseTwo.__doc__ = 'Convert base 2 string to an int.'
    >>> baseTwo('10010')
    18

在第二个例子中，要注意这里需要关键字参数 base，否则传入的 2 可能不是想要的关键字。

## 变量作用域
在使用全局变量的时候，局部变量会覆盖全局变量。为了明确地引用一个已命名的全局变量，必须使用 global 语句。global 的语法如下：

    global var1[, var2[, ... varN]]]

### 闭包
闭包将内部函数自己的代码和作用域以及外部函数的作用结合起来。闭包的词法变量不属于全局名字空间域或者局部的--而属于其他的名字空间,带着“流浪"的作用域。

Closurs 对于安装计算,隐藏状态,以及在函数对象和作用域中随意地切换是很有用的

## 生成器
协同程序是可以运行的独立函数调 用,可以暂停或者挂起,并从程序离开的地方继续或者重新开始

从句法上讲,生成器是一个带 yield 语句的函数

### 简单的生成器特性
与迭代器相似,生成器以另外的方式来运作:当到达一个真正的返回或者函数结束没有更多的 值返回(当调用 next()),一个 StopIteration 异常就会抛出








