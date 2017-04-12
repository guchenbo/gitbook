# Mysql几点
### 不锁表，加索引
```
ALTER TABLE duotin_user_device_token ADD INDEX idx_user_id (user_id), ALGORITHM=INPLACE, LOCK=NONE;
```
### 改变表的引擎

```
ALTER TABLE tableName ENGINE = InnoDB;
```
### 子查询之exists
exists和not exists作为子查询时，只返回**true**或者**false**

### 查询保持IN中的顺序
sql in 查询会默认使用id进行排序，想要保持in里的顺序，要用`order by field` 关键字，如：

```
select * from duotin_album where id in (13,10) order by field(id,13,10);
```
这样会按照id为13，10的顺序；

### 增加唯一约束

```
ALTER TABLE duotin_position_map
ADD CONSTRAINT un_key UNIQUE KEY(real_position_id,app_id,open_single_app_id);
```


