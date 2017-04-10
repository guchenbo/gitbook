# linux命令之sed
### 概述
sed，会从输入流处理数据，每次处理一行，会把一行缓冲起来，称为*pattern space*，然后通过命令脚步处理这个*pattern space*，最终会打印出经过处理的*pattern space*，然后处理下一行。
**==sed是循环处理每一行==**
-n  就不会自动打印经过处理的*pattern space*

### Pattern Space
sed处理文本的伪代码，了解一下Pattern Space的概念：

```
foreach line in file {
    //放入把行Pattern_Space
    Pattern_Space <= line;
 
    // 对每个pattern space执行sed命令
    Pattern_Space <= EXEC(sed_cmd, Pattern_Space);
 
    // 如果没有指定 -n 则输出处理后的Pattern_Space
    if (sed option hasn't "-n")  {
       print Pattern_Space
    }
}
```


### 命令格式：

`sed OPTIONS... [SCRIPT] [INPUTFILE...]`

### 注意：
mac的sed
使用`a、i`这些命令要`\`
```
sed '1a\
hello\
' pets.txt
```



