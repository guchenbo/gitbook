# Java之IO几点
### 写入文件

```
String fileName = sth;
File file = new File(fileName);
FileWriter writer = new FileWriter(file);
writer.write(sth);
```

