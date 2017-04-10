# dubbo之客户端引用服务

客户端配置信息，一个`<dubbo:reference />`对应一个`ReferenceBean`，调用`refer()`方法引用指定的服务。

### 概述
我们知道，dubbo服务端将每个服务都封装成本地执行的`Invoker`对象，然后暴露了出来。那么客户端的目的就是要发送一些信息到服务端，让服务端找到指定的`Invoker`对象，进而调用里面的服务的方法。

### 过程
引用服务的入口：`ReferenceBean.get()`，返回的是一个代理对象，伪代码如下：

```java
private T createProxy(Map<String, String> map) {
	Invoker invoker = refprotocol.refer(interfaceClass, urls.get(0));
	return (T) proxyFactory.getProxy(invoker);
}
```
url对象格式为：
```
registry://127.0.0.1:6379/com.alibaba.dubbo.registry.RegistryService?application=hello-world-app&dubbo=2.5.3&pid=41137&refer=application%3Dhello-world-app%26dubbo%3D2.5.3%26interface%3Dcre.dubbo.demo.DemoService%26methods%3DsayHello%26pid%3D41137%26side%3Dconsumer%26timestamp%3D1487324912402&registry=redis&timestamp=1487324912662
```

和服务端一样，分为两步：

1. url信息封装成`Invoker`对象
2. `Invoker`对象封装成代理对象

客户端获取的其实是这个代理对象

### 几个相关的接口

#### Protocol

```java
@Adaptive
<T> Invoker<T> refer(Class<T> type, URL url) throws RpcException;

```
引用服务，创建出一个远程通信的`Invoker`对象。根据url的协议名称获取特定的`Protocol`实现。

##### InjvmProtocol

获取`InjvmInvoker`对象，属性`exportMap`里包含了服务端的本地`Invoker`

##### DubboProtocol

获取`DubboInvoker`对象，并且建立到服务端的远程连接

#### ProxyFactory

```java
@Adaptive({Constants.PROXY_KEY})
<T> T getProxy(Invoker<T> invoker) throws RpcException;
```
创建`Invoker`对象的代理，实现有两个：

> 
* JdkProxyFactory
* JavassistProxyFactory



##### JdkProxyFactory
使用jdk动态代理，创建interface的代理

```java
public <T> T getProxy(Invoker<T> invoker, Class<?>[] interfaces) {
    return (T) Proxy.newProxyInstance(Thread.currentThread()
    .getContextClassLoader(), interfaces, 
    new InvokerInvocationHandler(invoker));
}

```

##### JavassistProxyFactory
使用jboss的javassist字节码框架，创建interface的代理

### 客户端调用过程

1. 获得服务引用的代理对象
2. 执行`Invoker`对象的`invoker()`方法
3. 根据`Invoker`具体实现,完成调用

#### InjvmInvoker
从属性`exportMap`里，获取服务端的本地`Invoker`，直接调用这个本地的`Invoker`对象的`invoker()`方法，完成调用，伪代码：

```java
public Result doInvoke(Invocation invocation) throws Throwable {
    Exporter<?> exporter = InjvmProtocol.getExporter(exporterMap, getUrl());
    return exporter.getInvoker().invoke(invocation);
}

```

#### DubboInvoker
向服务端的连接里面，发送请求等待服务端响应，完成调用，伪代码：

```java
public Result doInvoke(Invocation invocation) throws Throwable {
	boolean isAsync = RpcUtils.isAsync(getUrl(), invocation);
    boolean isOneway = RpcUtils.isOneway(getUrl(), invocation);
    int timeout = getUrl().getMethodParameter(methodName, Constants.TIMEOUT_KEY,Constants.DEFAULT_TIMEOUT);
    if (isOneway) {
    	boolean isSent = getUrl().getMethodParameter(methodName, Constants.SENT_KEY, false);
        currentClient.send(inv, isSent);
        RpcContext.getContext().setFuture(null);
        return new RpcResult();
    } else if (isAsync) {
    	ResponseFuture future = currentClient.request(inv, timeout) ;
        RpcContext.getContext().setFuture(new FutureAdapter<Object>(future));
        return new RpcResult();
    } else {
    	RpcContext.getContext().setFuture(null);
        return (Result) currentClient.request(inv, timeout).get();
    }
}

```

 



