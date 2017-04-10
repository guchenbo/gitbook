# Python 几个点
### .py 文件头

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

' comment '

__author__ = 'Cre Gu'
```
### 文件操作
#### 读文件
按行读取文件

```
# 使用with，保证文件操作完会关闭，代码简洁
with open('$filePath', 'r') as f:
	for l in f.readlines():
		print l.strip() # 去掉换行符
```
#### 写文件
按行写入文件

```
with open($filePath, 'r') as f:
	for l in li:
		f.write(l)
```

