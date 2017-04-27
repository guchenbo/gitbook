# Spring MVC之返回值处理过程
spring mvc是基于方法处理的，处理请求的过程中会将Controller的方法封装为ServletInvocableHandlerMethod，进行反射处理。里面有两个重要的步骤：

* 对方法参数的解析
* 对方法返回值的处理

### HandlerMethodReturnValueHandler
spring使用HandlerMethodReturnValueHandler接口处理请求方法的返回值，spring会加入默认的实现，用户也可以加入自定义的实现（==配置bean RequestMappingHandlerAdapter的customReturnValueHandlers属性==）。spring会根据条件选择合适的处理器进行处理返回值。

HandlerMethodReturnValueHandler声明了两个方法：


```
boolean supportsReturnType(MethodParameter returnType);

void handleReturnValue(Object returnValue, MethodParameter returnType, 		ModelAndViewContainer mavContainer, NativeWebRequest webRequest) throws Exception; 
```

* supportsReturnType：是否支持
* handleReturnValue：处理返回值


#### 默认实现类
RequestMappingHandlerAdapter#getDefaultReturnValueHandlers()

#### ViewNameMethodReturnValueHandler
##### 支持的类型
返回值类型为void或者CharSequence

##### 处理过程
设置View的名称

#### RequestResponseBodyMethodProcessor
##### 支持的类型
请求方法有注解@ResponseBody

##### 处理过程
1. 不需要返回View
2. 使用HttpMessageConverter将返回值写入Response的body中



