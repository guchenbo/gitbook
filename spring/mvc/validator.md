# Spring MVC之校验机制
spring 可以对提交方法的参数进行检验操作，比如必填项，长度等

### 1、Validator接口方式

1. 实现Validator接口
2. WebDataBinder设置Validator属性
3. 需要检验的参数前面加注解@Valid或@validated

#### Validator
声明了两个方法


```
boolean supports(Class<?> clazz);

void validate(Object target, Errors errors);

```

WebDataBinder设置Validator属性，可以通过两种方式：

* @InitBinder方法设置局部Validator
* xml配置全局的Validator

==注：局部覆盖全局==

	
### 2、JSR-303方式
主要是直接在属性上，加@NotNull等注解
略

