# 《自己动手写Java虚拟机》读书总结
### 4、运行时数据区
Java运行时，jvm需要把各种数据存放到内存中，这些内存就叫做**运行时数据区**。包括：

* 多线程共享区域
	* 类数据，放在方法区（MethodArea）
	* 类对象，放在堆（Heap）
	* 等等
* 线程私有区域
	* pc寄存器，正在执行的jvm指令的地址
	* 虚拟机栈
		*  栈桢
			*  局部变量表
			*  操作数栈	

### 5、jvm指令集
java中的方法被编译成字节码，存放在method_info结构中的Code属性，其中存放了一系列编码之后jvm指令，包括操作码和操作数，都是一个个字节。
**指令**：每一条指令都是由一个字节的操作码开始的，后面跟着0个或者多个字节的操作数。
最多有256个，到jdk8已经有205个，每个指令都有一个助记符。
**助记符**：有些助记符的首字母表示操作的数据类型

#### 5.1常用指令
* 常量指令：把常量推入操作数栈顶，常量来自操作码、操作数、运行时常量池。如：`lconst_0,iconst_0,bipush`
* 加载指令：从局部变量表中获取变量，推入操作数栈顶，操作码可以包含局部变量表的索引。如：`iload_0`
* 存储指令：从操作数栈顶弹出变量，存入局部变量表，操作码可以包含局部变量表的索引。如：`lstore_1`
* 栈指令：直接对操作数栈进行操作。如：`dup,swap,pop`
* 数学指令：
	* 算数指令：`add`、`sub`、`mul`，`div`，`rem`，`neg`，分别对应加，减，乘，除，求余，取反
	* 位移指令：左移、算术右移（有符号右移）、逻辑右移（无符号右移）。`shl`、`shr`、`ushr`
	* 布尔运算指令：只能操作int和long。分位`and`（按位与）、`or`（按位或）、`xor`（按位异或）
* 类型转换指令：如：`i2f,l2d,d2f`等
* 比较指令：
	* lcmp：弹出栈顶两个long，把比较结果（int 类型的0、1、-1）推入栈顶
	* fcmpg、fcmpl：弹出栈顶两个float，把比较结果推入栈顶，无法比较时，fcmpg返回1，fcmpl返回-1
	* dcmpg、dcmpl：弹出栈顶两个double，把比较结果推入栈顶，无法比较时，dcmpg返回1，dcmpl返回-1
	* if\<cond>：弹出栈顶的int，然后跟0比较，满足条件就跳转。分为：`ifeq`、`ifne`、`iflt`、`ifle`、`ifgt`、`ifge`
	* if_icmp\<cond>：弹出栈顶的两个int，满足比较则跳转，分为：`if_icmpeq`、`if_icmpne`、`if_icmplt`、`if_icmple`、`if_icmpgt`、`if_icmpge`
	* if_acmp\<cond>：弹出栈顶的两个引用，满足条件就跳转。分为：`if_acmpeq`、`if_acmpne`

* 控制指令：`goto`、`tableswitch`、`lookupswitch`，其中`tableswitch`和`lookupswitch`是实现*switch-case*语句的
* new指令：根据字节码中的操作数（一个2个字节的索引）从当前类的运行时常量池中获取一个类符号引用，解析并创建对象，把对象引用放入栈顶（操作数栈顶？？）
* 返回指令：`return areturn ireturn freturn lreturn dreturn`
	* `return`指令将当前桢（方法的桢）从jvm栈中弹出
	* `ireturn`：将当前桢（方法的桢）从jvm栈中弹出，方法的桢的操作数栈弹出一个int变量（这个是方法的返回值），推入调用者的桢的操作数栈顶
	* 其他的以此类推

### 6、类和对象
#### 6.1 方法区
存放类信息，类信息包括基本信息，运行时常量池，字段信息，方法信息和其他相关信息。

1、 类信息，go结构体

```
type Class struct {
	accessFlags       uint16
	name              string
	superClassName    string
	interfaceName     []string
	constantPool      *ConstantPool //运行时常量池
	fields            []*Field      //字符信息
	methods           []*Method     //方法信息
	loader            *ClassLoader  //类加载器
	superClass        *Class
	interfaces        []*Class
	instanceSlotCount uint   //实例变量数量大小
	staticSlotCount   uint   //静态变量数量大小
	staticVars        *Slots //静态变量
}
```

2、 字段信息

```
type Field struct {
	accessFlags uint16
	name        string
	descriptor  string
	class       *Class //字段所属类
}
```

3、 方法信息

```
type Method struct {
	accessFlags uint16
	name        string
	descriptor  string
	class       *Class
	maxStack    uint
	maxLocals   uint
	code        []byte
}
```

#### 6.2 运行时常量池
运行时常量池：字面量和符号引用
* 字面量：数字和字符串字面量
* 符号引用：类、字段、方法、接口方法符号引用

***符号引用***：是一个字符串，它给出了**被引用项**的名字，并且可能包含一些其他的关于这个**被引用项**的信息，这些信息足以唯一的识别一个类、字段、方法。

* 	对于其他类的符号引用，必须给出类的全名
*  对于其他类的字段的符号引用，必须给出类名、字段的名称和描述符
*  对于其他类的方法的符号引用，必须给出类名、方法的名称和描述符

