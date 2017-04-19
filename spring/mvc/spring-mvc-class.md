# Spring MVC重要的接口和类解析
### ContextLoaderListener
spring mvc启动的第一步，启动ROOT IOC容器并且放入`ServletContext`。

1. 实例化`WebApplicationContext`的实现类；
2. 加载`contextConfigLocation`配置的`applicationContext.xml`文件(`applicationContext.setConfigLocation()`)加载bean配置，来启动Spring IOC容器；
3. 把这个作为ROOT IOC容器放入`ServletContext`中；

==注：
1. WebApplicationContext的实现类，可以通过配置contextClass进行指定，ContextLoader.properties文件指定了默认实现，为XmlWebApplicationContext
2. XmlWebApplicationContext里定义了默认路径，为WEB-INF/applicationContext.xml==


### DispacherServlet
spring mvc启动第二步，启动WEB IOC容器，并且将ROOT IOC容器作为父容器。

1. 实例化`WebApplicationContext`的实现类；
2. 加载`contextConfigLocation`配置的`applicationContext.xml`文件，(`applicationContext.setConfigLocation()`)加载bean配置，来启动Spring IOC容器；
3. `onRefresh()`初始化各个组件，如果没有配置组件，就用默认实现，在`DispatcherServlet.properties`文件中定义了组件的默认实现；

==注：
1.WebApplicationContext的实现类，可以通过配置contextClass进行指定，FrameworkServlet类指定了默认实现，为XmlWebApplicationContext
2. XmlWebApplicationContext指定了默认路径为方法getDefaultConfigLocations()==


### HandlerMapping
Spring MVC默认有`BeanNameUrlHandlerMapping、DefaultAnnotationHandlerMapping（过期）`，配置`<mvc:annotation-driven />`注册`RequestMappingHandlerMapping`、`RequestMappingHandlerAdapter
`对应`@RequestMapping`。
#### AbstractHandlerMapping
`AbstractHandlerMapping`实现`HandlerMapping`，间接实现`ApplicationContextAware`，是所有HandlerMapping的抽象父类，有两个重要的方法：

* initApplicationContext()
* getHandler(HttpServletRequest)

==注：DispatcherServlet在创建HandlerMapping实例的等同于创建一个HandlerMapping类型的bean==
==注：这里ApplicationContextAware设置的ioc是web的ioc，不是root的ioc==

##### initApplicationContext
创建`HandlerMapping`类型的bean的时候，会入口`setApplicationContext()`，该方法里面会调用`initApplicationContext()`

* 初始化拦截器列表，将`HandlerInterceptor`列表，使用适配器模式封装成`HandlerInterceptorAdapter`列表
* 或者注册handlerMap或者其他自定义行为

##### getHandler
从handlerMap中根据url获取handler，也就是Controller的bean，通过Controller对象，找到具体执行的方法，封装成`ServletHandlerMethodInvoker`
创建`HandlerMapping`的bean时，会注册handlerMap

### RequestMappingHandlerMapping
Spring3.1之后主要的HandlerMapping，替换过期的`DefaultAnnotationHandlerMapping`，间接实现`InitializingBean`，主要的方法是：

* initHandlerMethods
* getHandler

#### initHandlerMethods

1. 扫描ioc容器的所有bean，对有`@RequestMapping`或者`@Controller`的bean做处理
2. 对有`@RequestMapping`的方法，封装为`HandlerMethod`，注册到相应Map中

#### getHandler
根据url，获取HandlerMethod封装成

1. 根据url，到相应的Map中查找HandlerMethod
2. 将HandlerMethod封装成HandlerExecutionChain对象，并且加入适配的拦截器

==注：查找HandlerMethod过程，会根据`@RequestMapping`注解的各个属性有优先级的查询，详见RequestCondition==

#### 模板模式
父类空方法，交由子类实现
#### 适配器模式
HandlerInterceptorAdapter



