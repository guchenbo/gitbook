# Spring MVC重要的接口和类解析
### ContextLoaderListener
spring mvc启动的第一步，启动根IOC容器并且放入`ServletContext`。

1. 实例化`XmlWebApplicationContext`类（默认的，可以自定义）；
2. 加载`WEB-INF/applicationContext.xml`（默认的，可以自定义），(`applicationContext.setConfigLocation()`)加载bean配置，来启动Spring IOC容器；
3. 把这个作为根IOC容器放入`ServletContext`中；

### DispacherServlet
spring mvc启动第二步，启动IOC容器，并且将根IOC容器作为父容器。

1. 实例化`XmlWebApplicationContext`类（默认的，可以自定义）；
2. 加载`contextConfigLocation`配置的`applicationContext.xml`文件，(`applicationContext.setConfigLocation()`)加载bean配置，来启动Spring IOC容器；
3. `onRefresh()`初始化各个组件，如果没有配置组件，就用默认实现，在`DispatcherServlet.properties`文件中定义了组件的默认实现；

### HandlerMapping
Spring MVC默认有`BeanNameUrlHandlerMapping、DefaultAnnotationHandlerMapping`

`AbstractHandlerMapping`实现`HandlerMapping`，间接实现`ApplicationContextAware`，是所有HandlerMapping的抽象父类

`DispatcherServlet`在创建`HandlerMapping`实例的等同于创建一个`HandlerMapping`的bean

创建`HandlerMapping`bean的时候，会入口`setApplicationContext()`，子类会初始化拦截器列表，方法是将`HandlerInterceptor`列表，使用适配器模式封装成`HandlerInterceptorAdapter`列表

getHandler()，从handlerMap中根据url获取handler，也就是Controller的bean，通过Controller对象，找到具体执行的方法，封装成`ServletHandlerMethodInvoker`
创建`HandlerMapping`的bean时，会注册handlerMap
#### 模板模式
父类空方法，交由子类实现
#### 适配器模式
HandlerInterceptorAdapter


