# Spring MVC之视图解析过程
HandlerAdapter执行请求方法返回值为ModelAndView，spring 解析ModelAndView，指定指定的View

### ModelAndView


```
private Object view; 
 /** Model Map */
 private ModelMap model;

```

view可以是具体指定的View对象，也可以是String对象，表示视图名称

### ViewResolver
根据viewName，解析出View对象


```
View resolveViewName(String viewName, Locale locale) throws Exception;

```

### View
渲染数据返回指定的页面，不管是jsp、Freemarker、Velocity，支持不同的视图的类型

