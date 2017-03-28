# Tomcat之请求处理流程
## Tomcat Connector初始化和启动准备
#### init
* connector.init()
	* protocolHandler.init()
		* endpoint.init()
			* endpoint.bind()
				* 创建serverSocket
	* mapperListener.init()

### start
* connector.start()
	* protocolHandler.start()
		* endpoint.start()
			* endpoint.bind()
			* endpoint.startInternal()
				* 创建线程池和任务队列，==ThreadPoolExecutor==
				* 初始化最大连接数计数器
				* 循环创建接受请求的线程，==Acceptor== 
				* 创建异步请求超时检测线程
	* mapperListener.start()
		* ==connector必须关联一个Engine==
		* 查找Engine的默认Host
		* Engine以及子容器都添加ContainerListener、LifecycleListener
		* Engine以及子容器都注册到MapperListener的Mapper对象中

## HTTP/1.1接收请求流程
* JIoEndpoint.Acceptor接受请求
* 循环从ServerSocket中获取Socket
* 将Socket封装为SocketWrapper
* 将SocketWrapper构造JIoEndpoint.SocketProcessor线程
* 将JIoEndpoint.SocketProcessor线程放入线程池==ThreadPoolExecutor==中执行
* Http11Protocol.Http11ConnectionHandler的process()，交给Http11Processor
* Http11Processor中处理交给CoyoteAdapter
* CoyoteAdapter交给Container的Pipline处理

## CoyoteAdapter处理请求流程
* 解析Request
* 调用StandardEngin的Pipline处理
* 调用StandardHost的Pipline处理
* 调用StandardContext的Pipline处理
* 调用StandardWrapper的Pipline处理
* 每个Pipeline都逐一调用其中的Valve
* 最后一个Valve是StandardWrapperValve

## 调用Servlet
* StandardWrapperValve里加载Servlet，创建FilterChain，调用FilterChain的doFilter()
* FilterChain.doFilter()，逐一调用其中的Filter的doFilter()
* Filter都执行完之后，最后调用Servlet.service(request, response)
* Servlet.service()，这里衔接Servlet容器，进入Servlet的编程流程

