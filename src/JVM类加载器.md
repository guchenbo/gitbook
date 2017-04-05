# JVM类加载器 #

JVM使用Java类的时候需要先加载，是通过类加载器来加载的。

类加载器是JVM用来加载类的类，加载的过程是通过Java字节代码文件（.class）生成java.lang.Class的实例。

当JVM启动的时候默认加载三个类加载器：

- 启动类加载器（Bootstrap Classloader）：加载java核心库，位于%JAVA_HOME%/jre/lib下的jar和classes，具体可通过sun.boot.class.path系统变量获取


- 扩展类加载器（Extention CLassloader）：加载java扩展库，位于%JAVA_HOME%/jre/lib/ext下的jar和classes，具体可通过java.ext.dirs系统变量获取


- 系统类加载器（System Classloader）：加载java应用的类，根据应用的CLASSPATH加载类

三个加载器的关系是Bootstrap > Extention > System，（`>`代表是父类）。

清单1，三个类加载器的完整树结构：
    
    ClassLoader loader = Test.class.getClassLoader();
	while (loader != null) {
		System.out.println("the parent of " + loader.toString() + " is " + loader.getParent());
		loader = loader.getParent();
	}

清单1的运行结果：

    the parent of sun.misc.Launcher$AppClassLoader@3dcc0a0f is sun.misc.Launcher$ExtClassLoader@1ea87e7b
	the parent of sun.misc.Launcher$ExtClassLoader@1ea87e7b is null

因为Bootstrap Classloader是用C++写的，所以JVM返回为null。

Java自带的类加载器采用`双亲委派模式`进行类的加载，即子的类加载器加
载的时候会委派给父类去加载，它的父类加载器也会委派给父类去加载，以此类推，如果能够加载则返回java.lang.Class的实例，否则回退到子类加载器加载，都不不能加载，则报`java.lang.ClassNotFoundException`异常。

同时一个类加载器，只能加载一个类一次，如果已经加载过就直接返回，不用重新加载。

同一个类，由两个不同的类加载器加载，也是不同的。所谓的类加载器的命名空间。

线程上下文类加载器，双亲委派模式能解决大部分类的加载情况。但是在JNDI、JDBC、JAXP这些SPI的类的实现的时候却不能满足，因为这些SPI的实现都是由第三方的开发商来实现的，Java只定义了规范，所以Java推出了线程上下文类加载器。通过`Thread.setContextClassLoader(Classloader)`，指定线程上下文类加载器来解决这个问题。