#映射和集合类型
映射类型中的数据是无序排列的

### 删除地点元素和字典

    del dict2['name'] # 删除键为“name”的条目 
    ict2.clear() # 删除 dict2 中所有的条目
    del dict2 # 删除整个 dict2 字典
    dict2.pop('name') # 删除并返回键为“name”的条目

### 映射类型操作符
字典的键查找操作符([  ])

键查找操作符是唯一仅用于字典类型的操作符,它和序列类型里单一元素的切片(slice)操作符 很相象。对序列类型来说,用索引做唯一参数或下标(subscript)以获取一个序列中某个元素的值。对字典类型来说,是用键(key)查询(字典中的元素),所以键是参数(argument), 而不是一个索引 (index)。键查找操作符既可以用于给字典赋值,也可以用于从字典中取值。


####字典比较操作符的比较顺序
#####1. 比较字典长度
如果字典的长度不同,那么用 cmp(dict1, dict2) 比较大小时,如果字典 dict1 比 dict2 长, cmp()返回正值,如果 dict2 比 dict1 长,则返回负值。也就是说,字典中的键的个数越多,这个 字典就越大,即:

    len(dict1) > len(dict2) ==> dict1 > dict2

##### 2. 比较字典的键
如果两个字典的长度相同,那就按字典的键比较;键比较的顺序和 keys()方法返回键的顺序相
同。 (注意: 相同的键会映射到哈希表的同一位置,这保证了对字典键的检查的一致性。) 这时, 如果两个字典的键不匹配时,对这两个(不匹配的键)直接进行比较。当 dict1 中第一个不同的键大 于 dict2 中第一个不同的键,cmp()会返回正值。

##### 3. 比较字典的值
如果两个字典的长度相同而且它们的键也完全匹配,则用字典中每个相同的键所对应的值进行 比较。一旦出现不匹配的值,就对这两个值进行直接比较。若 dict1 比 dict2 中相同的键所对应的 值大,cmp()会返回正值。

##### 4. Exact Match
到此为止,即,每个字典有相同的长度、相同的键、每个键也对应相同的值,则字典完全匹配, 返回0值。

### 字典内建方法

|方法名字|操作
|:--|:--
|dict.fromkeys(seq,val=None)| 创建并返回一个新字典,以 seq 中的元素做该字典的键,val 做该字 典中所有键对应的初始值(如果不提供此值,则默认为 None)
|dict.items()|返回一个包含字典中（键，值）对元组的列表
|dict.iter\*()|方法 iteritems()，iterkeys(), itervalues() 与它们对应的非迭代方法一样，不同的是它们返回一个迭代子，而不是一个列表
|dict.pop(key[, default])| 如果字典中 key 存在，删除并返回 dict[key]，如果 key 键不存在，且没有给出 default 的值，引发 KeyError 异常
|dict.setdefault(key, default=None)|和 set 方法相似，如果字典中不存在 key 键，由 dict[key]=default 为它赋值
|dict.update(dict2)|将字典 dict2 的键-值对添加到字典 dict，字典中原有的键如果与新添 加的键重复,那么重复键所对应的原有条目的值将被新键所对应的值所覆盖
|dict.values()|返回一个包含字典中所有值的列表

内建函数 sorted 对 dict 进行操作时返回一个有序的迭代子

etdefault()是自 2.0 才有的内建方法, 使得代码更加简洁,它实现了常用的语法: 检查字典 中是否含有某键。 如果字典中这个键存在,你可以取到它的值。 如果所找的键在字典中不存在, 你可以给这个键赋默认值并返回此值


## 集合类型
集合对象是一组无序排列的可哈希的值。

set 用 python 的比较操作符检查某集合是否是其他集合的超集或子集。“小于”符号( \<,\<=) 用来判断子集,“大于”符号( \>, \>=  )用来判断超集. )

###集合类型操作符（所有的集合类型）
#### 联合（|）
联合(union)操作和集合的 OR(又称可兼析取(inclusive disjunction))其实是等价的,两个集 合的联合是一个新集合,该集合中的每个元素都至少是其中一个集合的成员,即,属于两个集合其 中之一的成员。联合符号有一个等价的方法,union().

#### 交集（&）
你可以把交集操作比做集合的 AND(或合取)操作。两个集合的交集是一个新集合,该集合中的每 个元素同时是两个集合中的成员,即,属于两个集合的成员。交集符号有一个等价的方法, intersection().

#### 差补/相对补集（-）
两个集合(s 和 t)的差补或相对补集是指一个集合 C,该集合中的元素,只属于集合 s,而不属 于集合 t。差符号有一个等价的方法,difference().

#### 对称差分（^）
和其他的布尔集合操作相似,对称差分是集合的 XOR(又称”异或“ (exclusive disjunction)). 两个集合(s 和 t)的对称差分是指另外一个集合 C,该集合中的元素,只能是属于集合 s 或者集合 t 的成员,不能同时属于两个集合。对称差分有一个等价的方法,symmetric_difference().

#### 混合集合类型操作

    >>> t | s
    frozenset(['c', 'b', 'e', 'h', 'k', 'o', 'p', 's'])
    >>> t ^ s
    frozenset(['c', 'b', 'e', 'k'])
    >>> t - s
    frozenset(['k', 'b'])


如果左右两个操作数的类型相同,既都是可变集合或不可变集合, 则所产生的结果类型是相同 的,但如果左右两个操作数的类型不相同(左操作数是 set,右操作数是 frozenset,或相反情况),则所产生的结果类型与左操作数的类型相同,上例中可以证明这一点。还要注意,加号不是集合类型的运算符.

### 方法（所有的集合方法）

|方法名称|操作
|:--|:--
|s.issubset(t)|如果 s 是 t 的子集，则返回 True，否则返回 False
|s.superset(t)|如果 s 是 t 的超集，则返回 True，否则返回 False

add(), remove(), discard(), pop(), clear(). 这些接受对象的方法,参数必须是可哈希的。

### 操作符和内建方法的比较
很多内建方法几乎和操作符等价，这里说“几乎等价”是因为它们间有一个重要区别：当用操作符时，操作符两边的操作数必须是集合。在使用内建方法时，对象也可以是迭代类型的。


