rpc称为远程调用协议，多用于微服务之间用于数据交换。既然是协议，就可以把这个协议看成是一组规范。然而到目前为止对于rpc这个概念，业界还没有很明确的定义。

rpc这个概念从诞生到现在，已经发展出了很多成熟并且性能卓著的框架。比如支持HTTP/2并且跨语言的gRPC。直接基于传输层的TCP协议的Thrift等等。

现代rpc框架普遍具有的基本特性：

- 服务治理能力，服务发现，负载均衡

- 高性能，微服务之间调用非常频繁。rpc协议中传输信息密度和序列化速度的提升，都会带来应用性能整体的提升。


rpc入门教程：

- [gRPC教程 | 李文周的博客 (liwenzhou.com)](https://www.liwenzhou.com/posts/Go/gRPC/)
- [远程服务调用 | 凤凰架构 (icyfenix.cn)](http://icyfenix.cn/architect-perspective/general-architecture/api-style/rpc.html)
- [字节跳动开源Volo：国内首个基于Rust语言的RPC框架_语言 & 开发_字节跳动技术团队_InfoQ精选文章](https://www.infoq.cn/article/NR3Rd5YlUkarAhKyrZUe)

各种rpc框架的对比：

- [分布式RPC框架性能大比拼 (colobu.com)](https://colobu.com/2016/09/05/benchmarks-of-popular-rpc-frameworks/)
- [RPC 框架 Kitex 实践入门：性能测试指南 | CloudWeGo](https://www.cloudwego.io/zh/blog/2021/11/24/rpc-框架-kitex-实践入门性能测试指南/)

rpc框架使用到的二进制协议：

- [Protobuf 终极教程 (colobu.com)](https://colobu.com/2019/10/03/protobuf-ultimate-tutorial-in-go/)
- [Protocol Buffers V3中文语法指南[翻译\] | 李文周的博客 (liwenzhou.com)](https://www.liwenzhou.com/posts/Go/Protobuf3-language-guide-zh/)
- [Protobuf3 语言指南 - protobuf3中文指南 (gitbook.io)](https://lixiangyun.gitbook.io/protobuf3/)

grpc是如何跨语言的：

- 通过Protobuf协议实现





