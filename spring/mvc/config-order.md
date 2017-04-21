# Spring MVC之配置顺序
我们知道DispatcherServlet在初始化的时候，会初始化各种组件，比如HandlerMapping，HandlerAdapter等。

spring 使用 `<mvc:annotation-driven />` 会自动配置RequestMappingHandlerAdapter和RequestMappingHandlerMapping，我们也可以自己定义这两个bean，那么Spring mvc怎么确定这些配置的先后顺序呢。

我们以initHandlerMappings为例，发现源代码有

```
AnnotationAwareOrderComparator.sort(this.handlerMappings);
```
片段，会将handlerMappings进行排序，排序规则是handlerMappings元素的order属性进行比较，order越小，优先级越高，如果order相同，则先定义的优先级越高。



