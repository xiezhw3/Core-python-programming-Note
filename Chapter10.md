# 错误和异常
###异常
对异常最好的描述是：它是因为程序出现了错误而在正常控制流以外采取的行为。这个行为又分为两个阶段：首先是引起异常发生的错误，然后是检测（和采取可能的措施）阶段

## python 中的异常
SyntaxError 异常是唯一不是在运行时发生的异常

AttributeError: 尝试访问未知的对象属性

## 检测和处理异常

异常可以通过 try 语句来检测. 任何在 try 语句块里的代码都会被监测, 检查有无异常发 生.

try 语句有两种主要形式: try-except 和 try-finally . 这两个语句是互斥的, 也就是说你 只能使用其中的一种. 一个 try 语句可以对应一个或多个 except 子句, 但只能对应一个 finally 子句, 或是一个 try-except-finally 复合语句.

except 语句可以处理任意多个异常, 前提只是它们被放入一个元组里 , 如下所示:

    except (Exc1[, Exc2[, ... ExcN]])[, reason]:
        suite_for_exceptions_Exc1_to_ExcN

比如：

    def safe_float(obj):
        try:
            retval = float(obj)
        except (ValueError, TypeError):
            retval = 'argument must be a number or numeric string'
            return retval

### 捕获所有异常

如果查询异常继承的树结构, 我们会发现 Exception 是在最顶层的, 所以我们的代码可能看 起来会是这样:

    try:
        ...
    except Exception, e:
        # error occurred, log 'e', etc.

另一个我们不太推荐的方法是使用 裸 except 子句:

    try:
        ...
    except:
        # error occurred, etc.


**核心风格: 遵循异常参数规范**

当你在自己的代码中引发内建(built-in)的异常时, 尽量遵循规范, 用和已有 Python 代码 一致错误信息作为传给异常的参数元组的一部分. 简单地说, 如果你引发一个 ValueError , 那么 最好提供和解释器引发 ValueError 时一致的参数信息, 如此类推. 这样可以在保证代码一致性,同时也能避免其他应用程序在使用你的模块时发生错误.

### else 子句
else 在 try-except 语句段, 它的功能和你所见过的其他 else 没有太多的不同:在 try 范围中没有异常被检测到时,执行 else 子 句.

在 else 范围中的任何代码运行前,try 范围中的所有代码必须完全成功(也就是,结束前没有引发 异常)


### finally 子句
finally 子句是无论异常是否发生,是否捕捉都会执行的一段代码.你可以将 finally 仅仅配合 try 一起使用,也可以和 try-except(else 也是可选的)一起使用

## 上下文管理
### with 语句
另一个隐藏低层次抽象的例子是 with 语句。with 语法的基本用法如下：

    with context_expr [as var]:
        with_suite

它仅能工作于支持上下文管理协议（context management protocol）的对象。这意味着只有内建了“上下文管理”的对象可以和 with 一起工作。

## 触发异常
python 提供了一种机制让程序员明确的触发异常：raise 语句

### raise 语句
raise 语句对所支持是参数十分灵活,对应到语法上就是支持许多不同的格式.rasie 一般的用法是:

    raise [SomeException [, args [, traceback]]]


第一个参数,SomeExcpetion,是触发异常的名字.如果有,它必须是一个字符串,类或实例(详见 下文).如果有其他参数(arg 或 traceback),就必须提供



