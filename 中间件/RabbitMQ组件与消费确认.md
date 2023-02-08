#### Message acknowledgment

Doing a task can take a few seconds, you may wonder what happens if a consumer starts a long task and it terminates before it completes. With our current code, once RabbitMQ delivers a message to the consumer, it immediately marks it for deletion. In this case, if you terminate a worker, the message it was just processing is lost. The messages that were dispatched to this particular worker but were not yet handled are also lost.

But we don't want to lose any tasks. If a worker dies, we'd like the task to be delivered to another worker.

In order to make sure a message is never lost, RabbitMQ supports message acknowledgments. An ack(nowledgement) is sent back by the consumer to tell RabbitMQ that a particular message has been received, processed and that RabbitMQ is free to delete it.

If a consumer dies (its channel is closed, connection is closed, or TCP connection is lost) without sending an ack, RabbitMQ will understand that a message wasn't processed fully and will re-queue it. If there are other consumers online at the same time, it will then quickly redeliver it to another consumer. That way you can be sure that no message is lost, even if the workers occasionally die.

A timeout (30 minutes by default) is enforced on consumer delivery acknowledgement. This helps detect buggy (stuck) consumers that never acknowledge deliveries. You can increase this timeout as described in Delivery Acknowledgement Timeout.

In this tutorial we will use manual message acknowledgements by passing a false for the "auto-ack" argument and then send a proper acknowledgment from the worker with d.Ack(false) (this acknowledges a single delivery), once we're done with a task.



#### Forgotten acknowledgment

It's a common mistake to miss the ack. It's an easy error, but the consequences are serious. Messages will be redelivered when your client quits (which may look like random redelivery), but RabbitMQ will eat more and more memory as it won't be able to release any unacked messages.

In order to debug this kind of mistake you can use rabbitmqctl to print the messages_unacknowledged field:

sudo rabbitmqctl list_queues name messages_ready messages_unacknowledged
On Windows, drop the sudo:

rabbitmqctl.bat list_queues name messages_ready messages_unacknowledged

[RabbitMQ tutorial - Work Queues — RabbitMQ](https://www.rabbitmq.com/tutorials/tutorial-two-go.html)



RabbitMQ主要组件

生产者组件conn、channel、Exchange、Publish

 消费者组件conn、channel、Exchange、Queue、Consume

工作模式

发布/订阅，Exchange类型为fanout

路由模式，Exchange类型为direct，将各种等级的日志路由到各个队列

主题模式，Exchange类型为topic，支持细粒度的消息分类，在消费端进行订阅

rpc模式，Exchang类型为空

[RabbitMQ Tutorials — RabbitMQ](https://www.rabbitmq.com/getstarted.html)