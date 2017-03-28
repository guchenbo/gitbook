# Tomcat之容器生命周期
Tomcat生命周期接口`Lifecycle`，定义了一系列的周期，如初始化、启动、关闭等；`LifecycleBase`实现`Lifecycle`，使用模板模式实现每个方法，规范了具体容器的状态改变的行为；
Tomcat中的容器都直接或者间接的继承了`LifecycleBase`，每个容器都会包含一个监听器列表，每个周期都会触发监听事件，由指定的监听器列表接受并且执行操作。

### 容器生命周期改变
#### LifecycleBase
`LifecycleBase`，实现了`init()、start()、stop()`等方法。

#### 初始化
1. 具体容器的`init()`，实际是调用`LifecycleBase`的`init()`，目的做一些状态检查等公共操作；
2. 具体容器的`initInternal()`；
3. 调用`LifecycleMBeanBase`的`initInternal()`，目的是为了注册JMX；
4. 具体容器初始化操作；
5. 调用子容器的`init()`；

#### 启动
1. 具体容器的`start()`，实际是调用`LifecycleBase`的`start()`，目的做一些状态检查等公共操作；
2. 具体容器的`startInternal()`；
3. 具体容器启动操作；
4. 调用子容器的`start()`；

#### 关闭
1. 具体容器的`stop()`，实际是调用`LifecycleBase`的`stop()`，目的做一些状态检查等公共操作；
2. 具体容器的`stopInternal()`；
3. 具体容器启动操作；
4. 调用子容器的`stop()`；

#### 其他
其他周期流程类似，都是由父容器到子容器依次进行；



