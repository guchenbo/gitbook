# Spring MVC之参数处理过程
spring mvc是基于方法处理的，处理请求的过程中会将Controller的方法封装为ServletInvocableHandlerMethod，进行反射处理。里面有两个重要的步骤：

* 对方法参数的解析
* 对方法返回值的处理

