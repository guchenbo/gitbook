# dubbo的ExtensionLoader解析过程

### 使用示例

```
ExtensionLoader<Protocol> protocolLoader=ExtensionLoader.getExtensionLoader(Protocol.class);
Protocol  protocol=protocolLoader.getAdaptiveExtension();
```
#### 1、ExtensionLoader.getExtensionLoader(Protocol.class)
只会设置`ExtensionLoader`实例的一个静态属性：

```
ConcurrentMap<Class<?>, ExtensionLoader<?>> EXTENSION_LOADERS = new ConcurrentHashMap<Class<?>, ExtensionLoader<?>>();
```
用于缓存已经加载的扩展实例，并不会触发任何加载动作

#### 2、getAdaptiveExtension()
触发加载动作`loadExtensionClasses()`，加载扩展接口的实现类，`loadExtensionClasses()`步骤分为（以`Protocol`为例子）：

* 1、获取接口`Protocol`的`@SPI`注解的name属性（只能有一个），设置`ExtensionLoader`实例的`cacheDefaultName`，作为默认实现；
* 2、读取三个目录（`META-INF/dubbo/internal/,META-INF/dubbo/,META-INF/services`）下的`com.alibaba.dubbo.rpc.Protocol`文件，内容为：

	```
	![]()
	```
* 3、读取文件，分别加载对应的class，分三种情况存储到三个属性（`Class<?> cachedAdaptiveClass,Set<Class<?>> cachedWrapperClasses,Holder<Map<String, Class<?>>> cachedClasses`）中

	* 3.1、如果有`@Adaptive`注解，则设置`cachedAdaptiveClass`
	* 3.2、如果有对应接口参数的构造函数，说明是个装饰器，存储至`cachedWrapperClasses`
	* 3.3、如果没有上述构造函数，存储至`cachedClasses`

