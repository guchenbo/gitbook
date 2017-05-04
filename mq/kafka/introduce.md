# 入门
kafka是apache的一个消息中间件。
### 名词解释

* producer：生产者，生产消息的
* consumer：消费者，消费消息的
* topic：消息的分类
* broker：kafka集群中的某个服务器
* partition：一个topic可以有多个分区，分布在不同的broker上，每个分区保证消息的顺序

### 生产者
每个Producer生产消息时，选择发布到一个topic上的哪个分区

### 消费者
每个Consumer都隶属于一个或者多个ConsumerGroup消费者组。一个消息被多个消费组中的一个消费者消费，就是说，一个消息分发到多个消费组，发布-订阅模式，而每个消费者组中消息只能被其中一个消费者消费，变成了queue模式。==**这个是kafka的消费模型。**==


