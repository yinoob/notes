

####  anonymous functions

declaring anonymous functions without assigning them to variables is useful: defer statements and launching goroutines.

#### closures

 This  is  a  computer science word that means that functions declared inside of functions are able to access and modify variables declared in the outer function.



#### Interfaces are implemented implicitly

If the method set for a concrete type contains all of the methods in the method set for an interface, the concrete type implements the interface.

[A Tour of Go](https://go.dev/tour/methods/10)

#### Empty Interface

interface{} could store a value of any type.



#### read channel

read from a channel using a for-range loop.



#### use channels or mutexes

If you are coordinating goroutines or tracking a value as it is transformed by a series of goroutines,use channels.

If you are sharing access to field a struct,use mutexes.



#### context

If you know the maximum amount of time that a request can run, you can enforce it using the context.



[Amazon.com: Learning Go: An Idiomatic Approach to Real-World Go Programming: 9781492077213: Bodner, Jon: Books](https://www.amazon.com/Learning-Go-Idiomatic-Real-World-Programming/dp/1492077216/ref=sr_1_1?crid=3UHAO6XOGHUD9&keywords=learning+go&qid=1673825785&s=books&sprefix=learning+%2Cstripbooks-intl-ship%2C468&sr=1-1)



#### Amdahl‘s law

[Amdahl's law - Wikipedia](https://en.wikipedia.org/wiki/Amdahl's_law)

#### starvations

Keep in mind that starvation can also apply to CPU, memory, file handles, database connections: any resource that must be shared is a candidate for starvation.



#### Communicating Sequential Processes

[Communicating sequential processes (acm.org)](https://dl.acm.org/doi/pdf/10.1145/359576.359585)

#### Cond

a rendzvous points for goroutines waiting for or announcing the occurence of an event.

[5.4 条件变量 | Go 语言原本 (golang.design)](https://golang.design/under-the-hood/zh-cn/part1basic/ch05sync/cond/)

#### Once

Once is a type that utilizes some sync primitives internally to ensure that only call to Do ever calls the functions passed in-even on different goroutines.

#### Pool

Pool is a concurrent-safe implementation of the object pool pattern.

[sync.Pool — 深入Go语言之旅 (cyub.vip)](https://go.cyub.vip/concurrency/sync-pool.html)

#### channel ownership

a goroutine that instantiates, writes, and closes a channel. Much like memory in languages without garbage collection, it’s important to clarify which goroutine owns a channel in order to reason about our programs logically.   

[Channels in Go -Go 101](https://go101.org/article/channel.html)



[Amazon.com: Concurrency in Go: Tools and Techniques for Developers: 9781491941195: Cox-Buday, Katherine: Books](https://www.amazon.com/Concurrency-Go-Tools-Techniques-Developers/dp/1491941197/ref=sr_1_2?crid=7PIL0V7RI7C2&keywords=concurrent+in+go&qid=1673828135&s=books&sprefix=concurrent+in+go%2Cstripbooks-intl-ship%2C312&sr=1-2)





#### concurrency and parallelism

concurrency enables parallelism. Indeed, concurrency provides a structure to solve a problem with parts that may be parallelized.

Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once. -Rob Pike

#### Go scheduling

whereas an OS thread is context-switched on and off a CPU core by the OS，a goroutine is context-switched on and off an OS thread by the Go runtime.

[深度解密 Go 语言之 scheduler | qcrao 的博客](https://qcrao.com/post/dive-into-go-scheduler/)

#### channels or mutexes

we should use channels to signal that a specific resource is ready and handle the ownership transfer.

In general, we need mutexes for parallel goroutines and channels for concurrent ones.

#### race condition

A race condition occurs when the behavior depends on the sequence or the timing of events that can't be controlled.

#### happens-before 

- A send on a channel happens before the corresponding receive from that channel completes.
- Closing a channel happens before a receive of this closure.
- A receive from an unbuffered channel happens before the send on that channel completes.

#### nil channel

Receiving from a nil channel will block forever.

nil channels are useful in some conditions and should be part of the Go developer's toolset when dealing with concurrent with concurrent code.

#### sync.WaitGroup

sync.WaitGroup enables a happens-before relationship between wg.Add and wg.Wait.

When using a sync.WaitGroup, the Add operation must be done before sinning up a goroutine in the parent goroutine, whereas the Done operation must be done within the goroutine.

#### sync.Cond

Using sync.Cond, we can broadcast signals that wake all the goroutines waiting on a condition.



[100 Go Mistakes and How to Avoid Them: Harsanyi, Teiva: 9781617299599: Amazon.com: Books](https://www.amazon.com/100-Mistakes-How-Avoid-Them/dp/1617299596/ref=sr_1_1?crid=3UPG64MX09U8D&keywords=100+go+mistakes+and+how+to+avoid+them&qid=1673830292&s=books&sprefix=100+mistake%2Cstripbooks-intl-ship%2C429&sr=1-1)



Go 语言中只要是可比较的类型都可以作为 key。除开 slice，map，functions 这几种类型，其他类型都是 OK 的。具体包括：布尔值、数字、字符串、指针、通道、接口类型、结构体、只包含上述类型的数组。这些类型的共同特征是支持 == 和 != 操作符，k1 == k2 时，可认为 k1 和 k2 是同一个 key。如果是结构体，只有 hash 后的值相等以及字面值相等，才被认为是相同的 key。很多字面值相等的，hash出来的值不一定相等，比如引用。

顺便说一句，任何类型都可以作为 value，包括 map 类型。

[float 类型可以作为 map 的 key 吗 | Go 程序员面试笔试宝典 (golang.design)](https://golang.design/go-questions/map/float-as-key/)