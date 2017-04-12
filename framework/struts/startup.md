# Struts2之启动过程
> 1、web容器启动加载web.xml，初始化Struts2的filter，这个是Struts2的入口；
> 2、filter的`init()`方法初始化`Dispatcher`类
> 3、`Dispatcher`初始化一系列配置
> ![](http://i.imgur.com/KAid7xB.png)


> 4、这个方法先加入所有的配置文件提供者（ContainerProvider），然后reload分别初始化这几个提供者（ContainerProvider.init()）
> 5、其中的加载xml的ContainerProvider：加载struts-default.xml,struts-plugin.xml,struts.xml，会根据这几个名字取查询路径加载，完成这个后加载过程之后，不会再根据这个名字取查找了。加载过程是把xml读取解析成Document
>

