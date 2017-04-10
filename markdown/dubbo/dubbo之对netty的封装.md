# dubbo之对netty的封装
netty框架说基于事件驱动的，自己的业务逻辑都是要写在自己的`ChannelHandler`中，用于处理各种事件，而`Channel`对象包含了全局的信息。可以这么说`ChannelHandler`就是对`Channel`的各种操作。
dubbo中定义了自己的`ChannelHandler`和`Channel`，它是如何封装netty中的呢

### 自己实现 todo
使用`NettyHandler`操作`NettyChannel`，准备工作需要将netty自己的`Channel`封装成`NettyChannel`交由`NettyHandler`。`NettyHandler`继承netty的`SimpleChannelHandler`



