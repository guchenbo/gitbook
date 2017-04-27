# Schema机制
spring加载xml配置文件时，如果配置中有namespace前缀的，（如`<context:/> 、<mvc:/>`），会从读取`META-INF/`下的两个文件：
spring.schemas、spring.handlers来处理bean。
使用spring的namespace可以简化配置，我们可以自定义属于自己的namespace。


