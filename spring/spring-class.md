# Spring中重要的类
### BeanWrapper
bean的包装器，利用反射完成bean的属性设置和方法调用。
### ApplicationContextAware
一个bean实现了这个接口，在ioc容器创建该bean的时候，会自动调用方法`setApplicationContext(ApplicationContext)`，将当前的ioc容器的实例set到该bean中。


