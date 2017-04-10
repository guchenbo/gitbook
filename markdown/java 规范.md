

##### 1. 类名属性名采用驼峰形式，不能使用中文拼音；

```
UserService	✅
Userservice	❌
```

##### 2. 常量名全部大写，多个单词用下划线分隔，用`statis final`修饰如：

```
public static final String CACHE_KEY	
```

##### 3. core和behavior中的RPC接口采用`RpcService`后缀，接口的实现类命名采用Impl后缀，枚举类型一律采用Enum后缀，如：

```
ContentRpcService 表示RPC接口
AlbumService	表示普通接口
```

##### 4. 接口内方法不要public修饰符，如：

```
void login()	✅
public void login()	❌
```
##### 5. 类和接口中的方法，将同名的重载方法放在一起，方便查找；

##### 6. 接口方法返回一个对象的用`getXxx`命名方式，多个对象的用`getXxxList`命名方式，分页参数`Page`必须放在参数列的最后一个；

##### 7. 代码必须进行格式化，使用IDEA快键键

##### 8. 接口方法内不得超过50行，私有的方法允许超过50行，但不建议；

##### 9. 代码行超过一屏幕的必须换行，并且参数规范：

```

User user = new User().id(id).title(title)
				.info(info);	✅
				

User user = new User().id(id).title(title).
            info(info);		❌
User user = new User().id(id).title(title).info
            (info);		❌
            

void login(String user, String password, 
          String remeberMe)	✅

void login(String user, String password
          , String remeberMe)  ❌     
```

##### 10. 一个DAO只能调用一个Mapper，一个Service允许调用多个Dao

##### 11. 有关版本判断的都调用VersionUtils类的两个工具方法；

##### 12. if条件判断，多于两个条件组合，必须用单独的变量表示

```

if (startupPageList.size() == 1 && (city.equals(startupPageList.get(0).getCity())) || "全省".equals(startupPageList.get(0).getCity())) {
    //...
}	❌

boolean flag = startupPageList.size() == 1 && (city.equals(startupPageList.get(0).getCity())) || "全省".equals(startupPageList.get(0).getCity());
if (flag) {
    //...
}	✅
```

##### 13. 数据库自动生成的`Mapper`和`mapper.xml`文件不得修改

##### 14. 建表必须加注释

##### 15. 表字段有表示状态的，如`type`，新增了一个状态，必须相应完善注释

##### 16. 数据库表字段表示布尔类型的，java类型为Integer
