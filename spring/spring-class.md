# Spring中重要的类
### BeanWrapper
bean的包装器，利用反射完成bean的属性设置和方法调用。
### ApplicationContextAware
一个bean实现了这个接口，在ioc容器创建该bean的时候，会自动调用方法`setApplicationContext(ApplicationContext)`，将当前的ioc容器的实例set到该bean中。
### InitializingBean
一个bean实现了这个接口，在BeanFactory设置完该bean的属性之后，会调用方法`afterPropertiesSet()`，bean可以在这里自定义操作或者初始化。
==注：初始化也可以通过配置init-method方式实现==
### BeanPostProcessor


