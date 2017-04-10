# Python lesson 1
### 基础
python是解释性语言，使用缩进表示代码块，（这是很严格的）。一行表示一个语句结束，而java是分号（;）表示语句结束。
### 变量
python是动态语言，变量不需要声明类型，如：

```
a = 1
a = "abc"
```
* 普通的变量和函数都是public的，如：`ab，xy1`等
* `__a__,__name__`这样的都是特殊变量，python自带的，我们不要取这样的名字
* `_a,_x,__a,__x`这样的都是private的
* python的空值是`None`

### 布尔类型
`True`和`False`
逻辑运算有：
* 与 and
* 或 or
* 非 not，not True # --> False

python可以把布尔类型与其他数据类型做逻辑运算，为什么呢？
因为，**python中把数字`0`，空字符串`‘’`，`None`看成`False`，其他数字，非空字符串看成True**
==使用代码演示：==

```
a = True
print a and 'a=T' or 'a=F'
# 计算结果是'a=T'，而不是布尔类型
# a and 'a=T'，结果为'a=T'，
# 'a=T' or 'a=F'，结果为'a=T'
```
==and or 有一条规则：短路法则==

1. 在计算 a and b 时，如果 a 是 False，则根据与运算法则，整个结果必定为 False，因此返回 a；如果 a 是 True，则整个计算结果必定取决与 b，因此返回 b。
2. 在计算 a or b 时，如果 a 是 True，则根据或运算法则，整个计算结果必定为 True，因此返回 a；如果 a 是 False，则整个计算结果必定取决于 b，因此返回 b。

*a and b and c 三个逻辑运算都会走完的，不要以为前面是False了就不走了，牢记*

```
print False and '2' or '' and 'dd'
# 打印 空字符串，流程是：
# False and '2' -> False
# False or '' -> ''
# '' and 'dd' -> ''
```

### list tuple
list是有序集合，tuple是有序列表
定义list：
`l = [1,2,3]`
list里包含的元素，可以多种数据类型，如：

```
l = [1,'a',True]
l = [1,'a',['a','b','c']]
```
定义tuple：

```
l = (1,2,3)
// 定义一个
l = (1,)
```
取值方式相同：

```
//取值，0从前开始，-1从后面开始
l[0]
l[-1]
```
### dict和set
dict就是map，dict和set的key是不可变的。不能用list，但是能用tuple。dict用大括号定义：

```
d = {'a':1,'b':2}
//取值
d['a']
```
### 模块
一个`.py`文件就是一个模块，如abc.py的模块名是abc，如果两个模块名重复，可以使用包来分开，包就是一个目录，如`package1`，一个目录下面包含`__init__.py`，python就把这个目录当作包处理，包可以有多个层级，`package1`下的`abc.py`的模块名就是`package1.abc`
#### 使用模块

```
import abc
```
#### 安装第三发模块
使用`pip`命令安装，pip的python的包管理工具
```
pip install 模块名
```
第三发模块可以在[pypi.python.org]()，查找名称，如图片模块

```
pip install PIL
```


