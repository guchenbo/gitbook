# Spring MVC之DispatcherServlet处理请求的过程
DispatcherServlet类处理请求的过程主要集中在几个步骤：

1. 获取HandlerExecutionChain对象
2. 执行HandlerExecutionChain关联的拦截器的`preHandle`方法
3. 执行HandlerAdapter的`handle`方法
4. 执行HandlerExecutionChain关联的拦截器的`postHandle`方法

### HandlerAdapter的handle方法
大体分为以下几个步骤：

1. 封装HandlerMethod为ServletInvocableHandlerMethod
2. 使用HandlerMethodArgumentResolver对象处理request的请求参数
3. 反射执行Controller对象的具体方法
4. 将返回的对象用HandlerMethodReturnValueHandler进行处理


