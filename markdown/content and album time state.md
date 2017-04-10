# content and album time state
## 节目
### 能修改时间的地方
ContentMapper.xml
	insert
	insertSelective
	updateByExampleSelective
	updateByExample
	updateByPrimaryKeySelective
	updateByPrimaryKey

UpdateInterceptor??

设置时间的地方，手动或者拦截器


```
if (method.getName().startsWith("insert")) {     domain.setCreatedAt(new Date());     domain.setUpdatedAt(new Date()); } else if (method.getName().startsWith("update")) {     domain.setUpdatedAt(new Date()); }

```

created_at，只在insert开头的方法时保存，并且由`MapperInterceptor`里设置
updated_at，只在update开头的方法时保存，并且由`MapperInterceptor`里设置
online_time，在insert和update都有可能设置

`ContentMapper.insert`没人调用
`ContentMapper.insertSelective`的调用者：

 * `ContentDao.insert`
 	* `ContentPoolRpcService.publishContent`
 * `ContentDao.insertByMergerAlbum`



```flow
st=>start: Start:>http://www.google.com[blank]
e=>end:>http://www.google.com
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes
or No?:>http://www.google.com
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```


