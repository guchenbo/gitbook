# dubbo之服务端暴露服务
dubbo中一个重要的接口是：`Protocol`，定义了暴露服务和引用服务两个方法，其中服务端调用暴露服务，客户端调用引用服务。
`Protocol`有多个实现，默认是`DubboProtocol`，当然也可以使用dubbo的扩展机制（`ExtensionLoader`）自定义实现。

服务端配置信息，一个`<dubbo:service />`对应一个`ServiceBean`，调用`export()`方法暴露该服务。

dubbo是基于URL总线的，`Protocol$Adpative`根据url的protocol参数指定具体协议实现，这里介绍两个协议：`DubboProtocol`和`InjvmProtocol`。

* `InjvmProtocol`：本地协议，如果服务端和客户端在同一个jvm虚拟机可以使用
* `DubboProtocol`：默认协议

暴露服务的入口：`ServiceBean.export()`，一个服务可以配置多个注册中心，多个协议，
注册信息转换成URL：
```
registry://127.0.0.1:6379/com.alibaba.dubbo.registry.RegistryService?application=hello-world-app&dubbo=2.5.3&export=dubbo%3A%2F%2F192.168.20.243%3A20882%2Fcre.dubbo.demo.DemoService%3Fanyhost%3Dtrue%26application%3Dhello-world-app%26dubbo%3D2.5.3%26interface%3Dcre.dubbo.demo.DemoService%26methods%3DsayHello%26pid%3D75489%26proxy%3Djdk%26side%3Dprovider%26timestamp%3D1487209440579&pid=75489&registry=redis&timestamp=1487209440499
```
协议信息转换成URL：

```
dubbo://192.168.20.243:20882/cre.dubbo.demo.DemoService?anyhost=true&application=hello-world-app&dubbo=2.5.3&interface=cre.dubbo.demo.DemoService&methods=sayHello&pid=40636&proxy=jdk&side=provider&timestamp=1487323119105
```
暴露服务的伪代码为：

```java
List<URL> registryURLs = loadRegistries(true);
for (ProtocolConfig protocolConfig : protocols) {

	Invoker<?> invoker = proxyFactory.getInvoker(ref, (Class) interfaceClass, registryURL.addParameterAndEncoded(Constants.EXPORT_KEY, url.toFullString()));
    Exporter<?> exporter = protocol.export(invoker);
}
```
这里分成两步

* 将具体实现封装成`Invoker`
* 将`Invoker`对象封装成`Exporter`

这里涉及到几个接口：

* ProxyFactory
* Protocol
* Invoker
* Exporter

#### ProxyFactory
```java
<T> T getProxy(Invoker<T> invoker) throws RpcException;

<T> Invoker<T> getInvoker(T proxy, Class<T> type, URL url) throws RpcException;
```
`getInvoker `给服务端调用，将具体实现封装成本地`Invoker`，`getProxy `给客户端调用，todo
#### Protocol
```java
<T> Exporter<T> export(Invoker<T> invoker) throws RpcException;

<T> Invoker<T> refer(Class<T> type, URL url) throws RpcException;
```
`export `给服务端调用，暴露远程服务，`refer `给客户端调用，引用远程服务
#### Invoker

* 本地Invoker
* 远程Invoker
* 远程Invoker的集群Invoker


##### 本地Invoker
使用反射调用具体实现的方法
##### 远程Invoker
远程通信，客户端调用，将方法名等信息发送给服务端，服务端通过这些找到对应的本地Invoker，通过反思执行服务的方法
##### Exporter
```java
Invoker<T> getInvoker();

void unexport();
```
对`Invoker`的封装

### 不同协议对Invoker的封装
#### InjvmProtocol

1. `Invoker`对象封装为`Exporter`对象
2. `Exporter`对象放入`exportMap`
3. 等待同一个jvm的客户端
4. 从`exportMap`中获取`Exporter`对象
5. 从`Exporter`对象中获取`Invoker`对象


#### DubboProtocol

1. `Invoker`对象封装为`Exporter`对象
2. `Exporter`对象放入`exportMap`
3. 等待远程通信，dubbo的通信方式
4. 从`exportMap`中获取`Exporter`对象
5. 从`Exporter`对象中获取`Invoker`对象

#### 总结
我们可以看到，不同协议的差距在第3步