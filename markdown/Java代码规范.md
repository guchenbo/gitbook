# Java代码规范
### 提高代码可读性
对整体代码进行统一格式化，对函数和变量命名符合规范且富有意义

* 自己写的代码格式化，使用IDEA快捷键，`⌥ ⌘ L`
* 命名采用驼峰形式 
	* 类名首字母大写，如：`AlbumService`
	* 变量名、参数、方法名首字母小写，如：`getAllUsers()`
	
* 常量名，全部用大写，单词间用`_`分割，如：`USER_KEY`
* 方法名富有意义，能从方法名称上看出方法的作用
	* Service接口方法，增删改查以 add，get，modify，remove 开头
	* DAO接口方法，insert，query，update，delete, count开头
	
### 提高代码美观度

* 新建的类，加上文件头
![](/Users/penglai/Documents/ADD35D23-E686-4F08-90F3-83DA2EF299E9.png)

* 方法尽量加注释，接口方法必须要注释
* 方法内代码不超过50行，超过的用子方法进行重构，如果不能，必须加上必要的注释加以间隔，增加代码可维护性
* 对于过长的代码块，加入少量的空行
* 对于过长的行代码，采用分行编辑

### 其他

* 增加必要的单元测试
* API接口，增加接口文档（RAP）
* 项目包路径参照现有的结构
* mybatis相关的，使用自动构建，需要自己修改Mapper.java和mapper.xml的，写在MapperExt.java和mapperExt.xml中
	
	



