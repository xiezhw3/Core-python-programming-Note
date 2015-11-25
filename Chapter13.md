# 面向对象编程

#### 创建一个类

\_\_init\_\_ 方法是在类实例化时被调用的。可以认为实例化是对__init__()的一种隐 式的调用。

#### 创建子类
如果需要,每个子类最好定义它自己的构造器,不然,基类的构造器会被调用。然而,如果子 类重写基类的构造器,基类的构造器就不会被自动调用了--这样,基类的构造器就必须显式写出 才会被执行。

    FatherClass.__init__()

**核心笔记:命名类、属性和方法**

类名通常由大写字母打头。这是标准惯例,可以帮助你识别类,特别是在实例化过程中(有时看 起来像函数调用)。还有,数据属性(译者注:变量或常量)听起来应当是数据值的名字,方法名应 当指出对应对象或值的行为。另一种表达方式是:数据值应该使用名词作为名字,方法使用谓词(动 词加对象)。数据项是操作的对象、方法应当表明程序员想要在对象进行什么操作。在上面我们定义的类中,遵循了这样的方针,数据值像“name”,“phone”和“email”,行为如“updatePhone”, “updateEmail”。这就是常说的“混合记法(mixedCase)”或“骆驼记法(camelCase)”。Python 规 范推荐使用骆驼记法的下划线方式,比如,“update\_phone”,“update\_email”。类也要细致命名, 像“AddrBookEntry”,“RepairShop”等等就是很好的名字。

#### 绑定
为与 OOP 惯例保持一致,Python 严格要求,没有实例,方法是不能被调用的。这种限制即 Python所􏰁述的绑定概念(binding),在此,方法必须绑定(到一个实例)才能直接被调用。非绑定的方法 可能可以被调用,但实例对象一定要明确给出,才能确保调用成功。

### 决定类的属性

要知道一个类有哪些属性,有两种方法。最简单的是使用 dir()内建函数。另外是通过访问类的 字典属性__dict__,这是所有类都具备的特殊属性之一

    >>> print MyClass.__dict__
    >>> dir(MyClass)

### 特殊的类属性

|名称|作用
|:--|:--
|C.\_\_name\_\_|类 C 的名字（字符串）
|C.\_\_doc\_\_|类 C 的文档字符串
|C.\_\_bases\_\_|类 C 的所有父类构成的元组
|C.\_\_dict\_\_|类 C 的属性
|C.\_\_module\_\_|类 C 的所有模块
|C.\_\_class\_\_|实例 C 对应的类

## 实例
### \_\_init\_\_() "构造器"方法
当类被调用,实例化的第一步是创建实例对象。一旦对象创建了,Python 检查是否实现了 \_\_init\_\_()方法。默认情况下,如果没有定义(或覆盖)特殊方法\_\_init\_\_(),对实例不会施加任 何特别的操作.任何所需的特定操作,都需要程序员实现\_\_init\_\_(),覆盖它的默认行为。如果 \_\_init\_\_()没有实现,则返回它的对象,实例化过程完毕。

\_\_init\_\_() 应当返回 None


**核心笔记:实例属性**:

能够在“运行时”创建实例属性,是 Python 类的优秀特性之一.

Python 不仅是动态类型,而且在运行时,允许这些对象属性的动态创建。这种特性让人爱不释 手。当然,我们必须􏰀醒读者,创建这样的属性时,必须谨慎。

一个缺陷是,属性在条件语句中创建,如果该条件语句块并未被执行,属性也就不存在,而你 在后面的代码中试着去访问这些属性,就会有错误发生。故事的精髓是告诉我们,Python 让你体验 从未用过的特性,但如果你使用它了,你还是要小心为好。

### 实例属性 vs 类属性
类属性仅是与类相关的数据值,和 实例属性不同,类属性和实例无关。这些值像静态成员那样被引用,即使在多次实例化中调用类, 它们的值都保持不变

我们只有当使用类引用 version 时,才能更新它的值,像上面的 C.version 递增语句。 如果尝试在实例中设定或更新类属性会创建一个实例属性 c.version,后者会阻止对类属性 C.versioin 的访问,因为第一个访问的就是 c.version,这样可以对实例有效地“遮蔽”类属性C.version,直到 c.version 被清除掉。

	>>> class C(object): # define class 定义类
	... version = 1.2 # static member 静态成员
	...
	>>> c = C() # instantiation 实例化
	>>> C.version # access via class 通过类来访问
	1.2
	>>> c.version # access via instance 通过实例来访问
	1.2
	>>> C.version += 0.1 # update (only) via class 通过类(只能这样)来更新
	>>> C.version # class access 类访问
	1.3
	>>> c.version # instance access, which 实例访问它,其值已被改变
	1.3 # also reflected change

#### 从实例中访问类属性需谨慎
当我们从实例访问类属性的时候，如果我们对其进行赋值，那么会创建一个实例属性，那么对实例属性进行任何修改都不会影响到类属性本身。就算 del 实例属性。也就是说，这时的类属性其实是给实例属性隐藏了。
**但是在类属性可变**的情况下，一切都不同了，此时对"实例属性"进行修改会影响到类属性本身，也不能 del "实例属性"，也就是说，此时并没有生成一个实例属性，还是原来的类属性。

#### 类属性持久性
如果想要对类属性进行修改并对所有实例都有影响，那么通过类名进行调用

### 特殊的实例属性
|名称|作用
|:--|:--
|I.\_\_class\_\_|实例化 I 的类
|I.\_\_dict\_\_|I的属性

__dict__属性由一个字典组成,包含一个实例的所有属性。键是属性名,值是属性相应的数据 值。字典中仅有实例属性,没有类属性或特殊属性。

## 绑定和方法调用
**核心笔记:self 是什么?**

self 变量用于在类实例方法中引用方法所绑定的实例。因为方法的实例在任何方法调用中总是 作为第一个参数传递的,self 被选中用来代表实例。你必须在方法声明中放上 self(你可能已经注 意到了这点),但可以在方法中不使用实例(self)。如果你的方法中没有用到 self , 那么请考虑创建 一个常规函数,除非你有特别的原因。毕竟,你的方法代码没有使用实例,没有与类关联其功能, 这使得它看起来更像一个常规函数。在其它面向对象语言中,self 可能被称为 this。

### 调用非绑定方法
调用非绑定方法并不经常用到。需要调用一个还没有任何实例的类中的方法的一个主要的场景 是:你在派生一个子类,而且你要覆盖父类的方法,这时你需要调用那个父类中想要覆盖掉的构造方 法。如：

	class EmplAddrBookEntry(AddrBookEntry):
	'Employee Address Book Entry class' # 员工地址记录条目
	     def __init__(self, nm, ph, em):
	         AddrBookEntry.__init__(self, nm, ph)
	         self.empid = id
	         self.email = em

## 静态方法和类方法
对于类方法而言，需要类而不是实例作为第一个参数，它是有解释器传给这个方法的。类不需要特别地命名，类似 self，不过很多人使用 cls 作为变量名字

### staticmethod()和 classmethod()内建函数
对应的内建函数被转换成它们相应的类型,并且重新赋值给了相同的变量名

	class TestStaticMethod:
	    def foo():
	    	print 'calling static method foo()'
	    foo = staticmethod(foo)

	class TestClassMethod:
	    def foo(cls):
	    	print 'calling class method foo()'
	     	print 'foo() is part of class:', cls.__name__
		foo = classmethod(foo)

### 使用函数修饰符

	class TestStaticMethod:
	    @staticmethod
	    def foo():
	     	print 'calling static method foo()'

	class TestClassMethod:
	    @classmethod
	    def foo(cls):
	        print 'calling class method foo()'
	        print 'foo() is part of class:', cls.__name__


## 继承
### \_\_bases\_\_ 类属性
对任何(子)类,它是一个包含其父类 (parent)的集合的元组。注意,我们明确指出“父类”是相对所有基类(它包括了所有祖先类) 而言的。那些没有父类的类,它们的\_\_bases\_\_属性为空

子类可以通过 super() 来调用基类方法，而且能传递参数

class C(P):
	def __init__(self):
		super(C, self).__init__()
		print "calling C's constructor"

**核心笔记:重写\_\_init\_\_不会自动调用基类的\_\_init\_\_**

类似于上面的覆盖非特殊方法,当从一个带构造器 \_\_init()\_\_的类派生,如果你不去覆盖 \_\_init\_\_(),它将会被继承并自动调用。但如果你在子类中覆盖了\_\_init\_\_(),子类被实例化时, 基类的\_\_init\_\_()就不会被自动调用


### 从标准类型派生
随着类型(types)和类(class)的统一和新式类的引入，可以对标准类型进行子类化了。


### 多重继承
在使用了新型的类之后，经典的深度优先的 MRO 不再适合，因此使用了新的 MRO 方法

## 类、实例和其他对象的内建函数
### isdubclass()
issubclass() 布尔函数判断一个类是另一个类的子类或子孙类。它有如下语法

    issubclass(sub, sup)

从 Python 2.3 开始,issubclass()的第二个参数可以是可能的父类组成的 tuple(元组),这时, 只要第一个参数是给定元组中任何一个候选类的子类时,就会返回 True。

### isinstance()
isinstance() 布尔函数在判定一个对象是否是另一个给定类的实例时,非常有用。它有如下 语法:

    isinstance(obj1, obj2)

注意:第二个参数应当是类;不然,你会得到一个 TypeError。但如果第二个参数是一个类型对 象,则不会出现异常。这是允许的,因为你也可以使用 isinstance()来检查一个对象 obj1 是否是 obj2 的类型,比如:

	>>> isinstance(4, int)
	True
	>>> isinstance(4, str)
	False
	>>> isinstance('4', str)
	True

同 issubclass()一样,isinstance()也可以使用一个元组(tuple)作为第二个参数。这个特 性是从 Python 2.2 版本中引进的。如果第一个参数是第二个参数中给定元组的任何一个候选类型 或类的实例时,就会返回 True

### hasattr(), getattr(),setattr(), delattr()
\*attr()系列函数可以在各种对象下工作,不限于类(class)和实例(instances)


hasattr()函数是 Boolean 型的,它的目的就是为了决定一个对象是否有一个特定的属性,一 般用于访问某属性前先作一下检查。getattr()和 setattr()函数相应地取得和赋值给对象的属性, getattr()会在你试图读取一个不存在的属性时,引发 AttributeError 异常,除非给出那个可选的 默认参数。setattr()将要么加入一个新的属性,要么取代一个已存在的属性。而 delattr()函数会 从一个对象中删除属性。

example:

	>>> class myClass(object):
	... 	def __init__(self):
	... 		self.foo = 100 ...
	>>> myInst = myClass()
	>>> hasattr(myInst, 'foo')
	True
	>>> getattr(myInst, 'foo')
	100
	>>> hasattr(myInst, 'bar')
	False
	>>> getattr(myInst, 'bar')
	Traceback (most recent call last):
	File "<stdin>", line 1, in ?
	getattr(myInst, 'bar')
	AttributeError: myClass instance has no attribute 'bar'
	>>> setattr(myInst, 'bar', 'my attr')
	>>> dir(myInst)
	['__doc__', '__module__', 'bar', 'foo']
	>>> getattr(myInst, 'bar') # same as myInst.bar
	'my attr'
	>>> delattr(myInst, 'foo')
	>>> dir(myInst)
	['__doc__', '__module__', 'bar']
	>>> hasattr(myInst, 'foo')
	False

### dir()

- dir()作用在实例上(经典类或新式类)时,显示实例变量,还有在实例所在的类及所有它的基类中定义的方法和类属性。
- dir()作用在类上(经典类或新式类)时,则显示类以及它的所有基类的\_\_dict\_\_中的内容。 但它不会显示定义在元类(metaclass)中的类属性。
- dir()作用在模块上时,则显示模块的\_\_dict\_\_的内容。(这没改动)。
- dir()不带参数时,则显示调用者的局部变量。(也没改动)。
- 关于更多细节:对于那些覆盖了\_\_dict\_\_或\_\_class\_\_属性的对象,就使用它们;出于向后兼容的考虑,如果已定义了\_\_members\_\_和\_\_methods\_\_,则使用它们。

### super()
这个函数的目的就是帮助程序员找出相应的父类, 然后方便调用相关的属性。语法为：

    super(type[, obj])

给出 type,super()“返回此 type 的父类”。如果你希望父类被绑定,你可以传入 obj 参数(obj 必须是 type 类型的).否则父类不会被绑定。obj 参数也可以是一个类型,但它应当是 type 的一个子 类。通常,当给出 obj 时:

- 如果obj是一个实例,isinstance(obj,type)就必须返回True
- 如果obj是一个类或类型,issubclass(obj,type)就必须返回True

uper()是一个工厂函数,它创造了一个 super object,为一个给定的类使用__mro__ 去查找相应的父类

## 用特殊方法定制类
方法的两个重要方面:首先,方法必须在调用前被绑定(到它们 相应类的某个实例中);其次,有两个特殊方法可以分别作为构造器和析够器的功能,分别名为 __init__()和__del__()。

可定制类的特殊方法：

|基本定制型                     |  描述          
|:--|:--
|C.\_\_init\_\_(self[, arg1, ...])|  构造器(带一些可选的参数)                               
|C.\_\_new\_\_(self[, arg1, ...]) |  构造器(带一些可选的参数)，通常用在设置不变数据类型的子类。                        
|C.\_\_del\_\_(self)              |  解构器                 
|C.\_\_str\_\_(self)              |  可打印的字符输出，内建 str()及 print 语句                 
|C.\_\_repr\_\_(self)             |  运行时的字符串输出;内建 repr() 和‘ 操作符                  
|C.\_\_unicode\_\_(self)          |  Unicode 字符串输出;内建 unicode(                     
|C.\_\_call\_\_(self, \*args)      |  表示可调用的实例                 
|C.\_\_nonzero\_\_(self)          |  为 object 定义 False 值，内建 bool()             
|C.\_\_len\_\_(self)              |  “长度”（可用于类），内建len()         


## 私有化
双下划线(\_\_)：

    Python 为类元素(属性和方法)的私有性供初步的形式。由双下划线开始的属性在运行时被“混淆”,所以直接访问是不允许的。实际上,会在名字前面加上下划线和类名。比如,以例 13.6(numstr.py)中的 self.__num 属性为例,被“混淆”后,用于访问这个数据值的标识就变成了 self._NumStr__num。把类名加上后形成的新的“混淆”结果将可以防止在祖先类或子孙类中的同名冲突。这更多的是一种对导入源代码无法获得的模块或对同一模块中的其他代码的保护机制.

    这种名字混淆的另一个目的,是为了保护__XXX 变量不与父类名字空间相冲突。如果在类中有一 个__XXX 属性,它将不会被其子类中的__XXX 属性覆盖

单下划线(\_)：

    简单的模块级私有化只需要在属性名前使用一个单下划线字符。 这就防止模块的属性用“from mymodule import *”来加载。这是严格基于作用域的,所以这同样 适合于函数。


##授权
“包装”在 Python 编程世界中经常会被到的一个术语。它是一个通用的名字,意思是对一 个已存在的对象进行包装,不管它是数据类型,还是一段代码,可以是对一个已存在的对象,增加 新的,删除不要的,或者修改其它已存在的功能。

授权是包装的一种特性，可用于简化处理有关 dictating 功能,采用已存在的功能以达到最大 限度的代码重用。

实现授权的关键点就是覆盖\_\_getattr\_\_()方法,在代码中包含一个对 getattr()内建函数的调 用.


## 新式类的高级特性
在新式类中，python 内建的 “casting”或转换函数现在都是工厂函数。当这些函数被调用时，实际上是对相应的类型进行实例化。比如如下的函数：

- int(), long(), float(), complex()
- str(), unicode()
- list(), tuple()
- type()
- basestring()
- dict()
- bool()
- set(), frozenset()
- object()
- classmethod()
- staticmethod()
- super()
- property()
- file()

这些类名及工厂函数用起来很灵活，不仅能够创建这些类型的新对象，它们还可以用来作为基类，去子类化类型。现在还可以用于isinstance() 内建函数：

OLD (not as good):

- if type(obj) == type(0)...
- if type(obj) == types.IntType...

BETTER:

- if type(obj) is type(0)...

EVEN BETTER:

- if isinstance(obj, int)...
- if isinstance(obj, (int, long))...
- if type(obj) is int...

>
记住:尽管 isinstance()很灵活,但它没有执行“严格匹配”比较----如果 obj 是一个给定类 型的实例或其子类的实例,也会返回 True。但如果想进行严格匹配,你仍然需要使用 is 操作符。

### \_\_slots\_\_ 类属性
字典位于实例的“心脏”。\_\_dict\_\_属性跟踪所有实例属性。举例来说,你有一个实例 inst.它有一个属性 foo,那使用 inst.foo 来访问它与使用 inst.\_\_dict\_\_['foo']来访问是一致的。

字典会占据大量内存,如果你有一个属性数量很少的类,但有很多实例,那么正好是这种情况。为内存上的考虑,用户现在可以使用\_\_slots\_\_属性来替代\_\_dict\_\_。
基本上,\_\_slots\_\_是一个类变量,由一序列型对象组成,由所有合法标识构成的实例属性的集合来表示。它可以是一个列表,元组或可迭代对象。也可以是标识实例能拥有的唯一的属性的简单 字符串。任何试图创建一个其名不在\_\_slots\_\_中的名字的实例属性都将导致 AttributeError 异常:

    class SlottedClass(object):
        \_\_slots\_\_ = ('foo', 'bar')
    >>> c = SlottedClass()
    >>>
    >>> c.foo = 42
    >>> c.xxx = "don't think so"
    Traceback (most recent call last):
    File "<stdin>", line 1, in ?
    AttributeError: 'SlottedClass' object has no attribute 'xxx'

这种特性的主要目的是节约内存。其副作用是某种类型的"安全",它能防止用户随心所欲的动态增加实例属性。带\_\_slots\_\_属性的类定义不会存在\_\_dict\_\_了(除非你在\_\_slots\_\_中增加 '\_\_dict\_\_'元素)。

### 描述符
你可以认为􏰁述符是 表示对象属性的一个代理。当需要属性时,可根据你遇到的情况,通过􏰁述符(如果有)或者采用 常规方式(句点属性标识法)来访问它。

#### \_\_get\_\_(),\_\_set\_\_(),\_\_delete\_\_()特殊方法
严格来说，述符实际上可以是任何(新式)类，这种类至少实现了三个特殊方法 \_\_get\_\_()，\_\_set\_\_()及\_\_delete\_\_()中的一个，这三个特殊方法充当描述符协议的作用。\_\_get\_\_()可用于得到一个属性的值，\_\_set\_\_()是为一个属性进行赋值的，在采用 del 语句(或 其它，其引用计数递减)明确删除掉某个属性时会调\_\_delete\_\_()方法。\_\_delete\_\_() 很少被实现

#### \_\_getattribute\_\_ 特殊方法
使用描述符的顺序很重要,有一些描述符的级别要高于其它的。整个描述符系统的心脏是\_\_getattribute\_\_(),因为对每个属性的实例都会调用到这个特殊的方法。这个方法被用来查找类的属性,同时也是你的一个代理,调用它可以进行属性的访问等操作。

当引用一个属性时,Python 解释器将试着在局部名称空间中查找那个名字,比如一个 自定义的方法或局部实例属性。如果没有在局部字典中找到,则搜索类名称空间,以防一个类属性 被访问。最后,如果两类搜索都失败了,搜索则对原对象开始授权请求,此时,__getattr__()会被 调用。

很多用户碰到的问题是,他们想要一个适当的函数来执行每一个属性访问,不光是当属性不能 找到的情况。这就是__getattribute__()用武之处了。它使用起来,类似__getattr__(),不同之处 在于,当属性被访问时,它就一直都可以被调用,而不局限于不能找到的情况。

#### 优先级别
由于\_\_getattribute\_\_()的实现方式很特别,我们在此对\_\_getattribute\_\_()方法的执行方式 做一个介绍。因此了解以下优先级别的排序就非常重要了:

- 类属性
- 数据描述符：实现了 \_\_get\_\_() 和 \_\_set\_\_() 的描述符
- 实例属性
- 非数据描述符：比如方法
- 默认为\_\_getattr\_\_()

#### 属性和 property() 内建函数
属性是一种有用的特殊类型的描述符。它们是用来处理所有对实例属性的访问，其工作方式和 我们前面说过的描述符相似。“一般”情况下,当你使用点属性符号来处理一个实例属性时,其实 你是在修改这个实例的\_\_dict\_\_属性。

property()内建函数有四个参数,它们是:

    property(fget=None, fset=None, fdel=None, doc=None)









