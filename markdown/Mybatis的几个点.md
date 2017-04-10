# Mybatis的几个点
### in 查询
Java

```
method(@Param("ids") List<Integer> list)
```
```
<if test="ids != null and ids.size() > 0">
<foreach item="item" index="index" collection="ids" open="(" separator="," close=")">
	#{item}  
</foreach>
</if>

```

