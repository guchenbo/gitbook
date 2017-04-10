# mysql之索引
最好选用数据类型小的字段
### 单列索引
* = 可以用到
* in 可以用到
* like int类型索引不能用，varchar类型满足最左前缀可以用，`%`写在后面可以用
	* `2%`，`2`可以用
	* `%2`不能用


### 组合索引
满足最左前缀原则能用到索引，或者一部分索引
[索引背后的密码](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)这篇文章讲得很清楚！



