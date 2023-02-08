##### event

An **event** records the fact that "something happened" in the world or in your business. It is also called record or message in the documentation. When you read or write data to Kafka, you do this in the form of events. Conceptually, an event has a key, value, timestamp, and optional metadata headers.

##### exactly-once

So effectively Kafka supports exactly-once delivery in [Kafka Streams](https://kafka.apache.org/documentation/streams), and the transactional producer/consumer can be used generally to provide exactly-once delivery when transferring and processing data between Kafka topics. Exactly-once delivery for other destination systems generally requires cooperation with such systems, but Kafka provides the offset which makes implementing this feasible (see also [Kafka Connect](https://kafka.apache.org/documentation/#connect)). Otherwise, Kafka guarantees at-least-once delivery by default, and allows the user to implement at-most-once delivery by disabling retries on the producer and committing offsets in the consumer prior to processing a batch of messages.

[Apache Kafka](https://kafka.apache.org/documentation/#semantics)



##### 生产者和消费者

在默认情况下，生产者会把消息均衡地分布到主题的所有分区中。不过，在某些情况下，生产者会把消息直接写入指定的分区，这通常是通过消息键和分区器来实现的。分区器会为键生成一个哈希值，并将其映射到指定的分区，这样可以保证包含同一个键的消息被写入同一个分区。

##### broker和集群

一台单独的Kafka服务器被称为broker。broker会接收来自生产者的消息，为其设置偏移量，并提交到磁盘保存。broker会为消费者提供服务，对读取分区的请求做出响应，并返回已经发布的消息。

Kafka使用Avro作为消息序列化框架，每天可以高效处理数十亿级别的指标和用户活动跟踪信息。

##### Kafka生产者

当幂等生产者被启用时，生产者将给发送的每一条消息都加上一个序列号。如果broker收到具有相同序列号的消息，那么它就会拒绝第二个副本，而生产者则会收到DuplicateSequenceException，这个异常对生产者来说是无害的。

##### KRaft

在新架构中，控制器节点形成了一个Raft仲裁，管理着元数据事件日志。这个日志中包含了集群元数据的每一个变更。原先保存在ZooKeeper中的所有东西（比如主题、分区、ISR、配置等）都将被保存在这个日志中。因为使用了Raft算法，所以控制器节点可以在不依赖外部系统的情况下选举首领。首领节点被称为主控制器，负责处理所有来自broker的RPC调用。跟随者控制器会从主控制器那里复制数据，并会作为主控制器的热备。因为控制器会跟踪最新的状态，所以当发生控制器故障转移时（在此期间，所有的状态都将被转移给新控制器），很快就可以完成状态的重新加载。



Kafka提供了一种二进制协议（基于TCP），指定了请求消息的格式以及broker如何对请求做出响应——既包括成功处理请求，也包括在处理请求过程中出现错误。

Kafka使用零复制技术向客户端发送消息，也就是说，Kafka会直接把消息从文件（或者更确切地说是Linux文件系统缓存）里发送到网络通道，不需要经过任何中间缓冲区。这是Kafka与其他大部分数据库系统不一样的地方，其他数据库在将数据发送给客户端之前会先把它们保存在本地缓存中。这项技术避免了字节复制，也不需要管理内存缓冲区，从而能够获得更好的性能。

[Kafka权威指南（第2版）-格温·沙皮拉 托德·帕利诺 拉吉尼·西瓦拉姆 克里特·佩蒂-微信读书 (qq.com)](https://weread.qq.com/web/bookDetail/106329e0813ab77cfg010f2e)