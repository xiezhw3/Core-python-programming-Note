# 执行环境
## 可调用对象
### 函数
python 有三种不同类型的函数对象。

####内建函数（BIFs）
BIF 是用 c/c++写的,编译过后放入 python 解释器,然后把它们作为第一(内建)名字空间的一部分加载进系统。如前面章节所提到的,这些函数在\_bulitin\_模块里,并作为\_\_builtins\_\_模 块导入到解释器中。

#### 用户定义的函数（UDF）
UDF(User-Defined Function,用户定义的函数)通常是用 python 写的,定义在模块的最高级, 因此会作为全局名字空间的一部分(一旦创建好内建名字空间)装载到系统中。函数也可在其他的函 数体内定义,并且由于在 2.2 中嵌套作用域的改进,我们现在可以对多重嵌套作用域中的属性进行访问。可以用 func_closure 属性来钩住在其他地方定义的属性。

用户自定义函数属性：

|UDF 属性             |描述
|:--                 |:--                                           
|udf.\_\_doc\_\_         |文档字符串(也可以用 udf.func\_doc)
|udf.\_\_name\_\_        |字符串类型的函数名字(也可以用 udf.func\_name) 
|udf.func\_code       |字节编译的代码对象  
|udf.func\_defaults   |默认的参数元组      
|udf.func\_globals    |全局名字空间字典; 和从函数内部调用 globals(x)一样     
|udf.func\_dict       |函数属性的名字空间   
|udf.func\_doc        |(见上面的 udf.\_\_doc\_\_) 
|udf.func\_name       |(见上面的 udf.\_\_name\_\_)   
|udf.func\_closure    |包含了自由变量的引用的单元对象元组(自用变量在 UDF 中使用,但在别处定义;参见 python[语言]参考手册)     

从内部机制来看,用户自定义的函数是“函数“类型的

lambda 表达式和用户自定义对函数相比,略有不同。虽然它们也是返回一个函数对象,但是 lambda 表达式不是用 def 语句创建的,而是用 lambda 关键字



#### 内建方法（BIMs）
BIM 和 BIF 两者也都享有相同属性。不同之处在于 BIM 的__self__属性指向一个 Python 对象,而 BIF 指向 None。


