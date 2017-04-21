# 对象排序
java处理对象排序的，可以使用排序器接口：

* Comparable
* Comparator

### Comparable和Comparator比较

* Comparable是排序接口，实现该接口表示类可以排序
* Comparator是比较接口，实现该接口是定义一个比较器，用来比较两个对象
* Comparable相当于”内部比较器“，Comparator相当于”外部比较器“

示例：

* Comparable

```
Arrays.sort(); //数组排序
Collections.sort(); //集合排序
```
==注：如果list的元素实现了Comparable就排序，否则不排序==

* Comparator

```
Arrays.sort(comparator); //数组排序
Collections.sort(comparator); //集合排序
```
==注：这里会使用比较器comparator去排序list的元素==

### compare方法
不管是实现Comparable还是实现Comparator，都要实现排序方法：compareTo或者compare（方法名不同，功能相同），compare方法是比较两个对象x和y，这里解释下这个方法的返回值代表什么意思

* <=0，表示排序：x排在y前面，即x、y
* >0，表示排序：x排在y后面，即y、x


