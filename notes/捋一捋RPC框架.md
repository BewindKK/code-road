## 本文章结构

![image-20220321163908854](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/205/image-20220321163908854.png)



## 何为RPC

**RPC（Remote Procedure Call）** 即远程过程调用，通过名字我们就能看出 RPC 关注的是远程调用而非本地调用。

## 为什么需要RPC

两个不同的服务器上的服务提供的方法不在一个内存空间，所以，需要通过网络编程才能传递方法调用所需要的参数。

通过 RPC 可以帮助我们调用远程计算机上某个服务的方法，这个过程就像调用本地方法一样简单。并且！我们不需要了解底层网络编程的具体细节。

**RPC 的出现就是为了让你调用远程方法像调用本地方法一样简单**

## RPC原理

![image-20220321133741997](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/205/image-20220321133741997.png)

1. **客户端（服务消费端）** ：调用远程方法的一端。
2. **服务端（服务提供端）** ：提供远程方法的一端。
3. **客户端 Stub（桩）**：代理类，把调用方法、类、方法参数传递到服务端
4. **服务端 Stub（桩）**：接收到客户端执行方法的请求，返回给客户端的类
5. **网络传输**：提供两端的数据传输服务
   1. 实现：Socket、Netty



1. 服务消费端（client）以本地调用的方式调用远程服务；
2. 客户端 Stub（client stub） 接收到调用后负责将方法、参数等组装成能够进行网络传输的消息体（序列化）：`RpcRequest`；
3. 客户端 Stub（client stub） 找到远程服务的地址，并将消息发送到服务提供端；
4. 服务端 Stub（桩）收到消息将消息反序列化为Java对象: `RpcRequest`；
5. 服务端 Stub（桩）根据`RpcRequest`中的类、方法、方法参数等信息调用本地的方法；
6. 服务端 Stub（桩）得到方法执行结果并将组装成能够进行网络传输的消息体：`RpcResponse`（序列化）发送至消费方；
7. 客户端 Stub（client stub）接收到消息并将消息反序列化为Java对象:`RpcResponse` ，这样也就得到了最终结果。

![image-20220321160715901](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/205/image-20220321160715901.png)

## 应用场景

随着我们的业务越来越多，应用也越来越多，应用与应用相互关联调用，发现有些功能已经不能简单划分开，此时可能就需要用到 RPC。

比如，我们开发电商系统，需要拆分出用户服务、商品服务、优惠券服务、支付服务、订单服务、物流服务、售后服务等等，这些服务之间都相互调用，这时内部调用最好使用 RPC ，同时每个服务都可以独立部署，独立上线。

也就说当我们的项目太大，需要解耦服务，扩展性强、部署灵活，这时就要用到 RPC ，主要解决了分布式系统中，服务与服务之间的调用问题。

## 现有RPC框架

### **RMI（JDK自带）**

 JDK自带的RPC，有很多局限性，不推荐使用。

### **Dubbo**

Dubbo是 阿里巴巴公司开源的一个高性能优秀的服务框架，使得应用可通过高性能的 RPC 实现服务的输出和输入功能，可以和 Spring框架无缝集成。目前 Dubbo 已经成为 Spring Cloud Alibaba 中的官方组件。

1. 面向接口代理的高性能RPC调用。
2. 智能容错和负载均衡。
3. 服务自动注册和发现。
4. 高度可扩展能力。
5. 运行期流量调度。
6. 可视化的服务治理与运维。

### gRPC

gRPC是可以在任何环境中运行的现代开源高性能RPC框架。它可以通过**可插拔**的支持来有效地连接数据中心内和跨数据中心的服务，以实现负载平衡，跟踪，运行状况检查和身份验证。它也适用于分布式计算的最后一英里，以将设备，移动应用程序和浏览器连接到后端服务。

### Hessian

Hessian是一个轻量级的remoting on http工具，使用简单的方法提供了RMI的功能。 相比WebService，Hessian更简单、快捷。采用的是二进制RPC协议，因为采用的是二进制协议，所以它很适合于发送**二进制数据**。

### Thrift

Apache Thrift是Facebook开源的跨语言的RPC通信框架，目前已经捐献给Apache基金会管理，由于其跨语言特性和出色的性能，在很多互联网公司得到应用，有能力的公司甚至会基于thrift研发一套分布式服务框架，增加诸如服务注册、服务发现等功能。

## 序列化

### 什么是序列化

**序列化就是将对象转换成二进制数据的过程，而反序列就是反过来将二进制转换为对象的过程**。

### 序列化方式

**JDK自带**

序列化具体的实现是由 ObjectOutputStream 完成的，而反序列化的具体实现是由 ObjectInputStream 完成的。

**JSON**

JSON 是典型的 Key-Value 方式，没有数据类型，是一种文本型序列化框架

无论是前台 Web 用 Ajax 调用、用磁盘存储文本类型的数据，还是基于 HTTP 协议的 RPC 框架通信，都会选择 JSON 格式。

**问题：**

- JSON 进行序列化的额外空间开销比较大，对于大数据量服务这意味着需要巨大的内存和磁盘开销；
- JSON 没有类型，但像 Java 这种强类型语言，需要通过反射统一解决，所以性能不会太好。

所以如果 RPC 框架选用 JSON 序列化，**服务提供者与服务调用者之间传输的数据量要相对较小，否则将严重影响性能**。

**Hessian** 

- /ˈhesiən/ 

Hessian 是动态类型、二进制、紧凑的，并且可**跨语言移植**的一种序列化框架。Hessian 协议要比 JDK、JSON 更加紧凑，性能上要比 JDK、JSON 序列化**高效**很多，而且生成的字节数也更小。

```java
Student student = new Student();
student.setNo(101);
student.setName("HESSIAN");
//把student对象转化为byte数组
ByteArrayOutputStream bos = new ByteArrayOutputStream();
Hessian2Output output = new Hessian2Output(bos);
output.writeObject(student);
output.flushBuffer();
byte[] data = bos.toByteArray();
bos.close();
//把刚才序列化出来的byte数组转化为student对象
ByteArrayInputStream bis = new ByteArrayInputStream(data);
Hessian2Input input = new Hessian2Input(bis);
Student deStudent = (Student) input.readObject();
input.close();
System.out.println(deStudent);
```

Hessian 更加适合作为 RPC 框架远程通信的序列化协议。

**问题**

Linked 系列，LinkedHashMap、LinkedHashSet 等，但是可以通过扩展CollectionDeserializer 类修复；
Locale 类，可以通过扩展 ContextSerializerFactory 类修复；
Byte/Short 反序列化的时候变成 Integer。

**Protobuf**

Protobuf 是 Google 公司内部的混合语言数据标准，是一种轻便、高效的结构化数据存储格式，可以用于结构化数据序列化，支持 Java、Python、C++、Go 等语言。Protobuf使用的时候需要定义 IDL（Interface description language），然后使用不同语言的 IDL编译器，生成序列化工具类，它的优点是：

序列化后体积相比 JSON、Hessian 小很多；--体积小
IDL 能清晰地描述语义，所以足以帮助并保证应用程序之间的类型不会丢失，无需类似XML 解析器；
序列化反序列化**速度很快**，不需要通过反射获取类型；
**消息格式升级和兼容性不错**，可以做到向后兼容。

### 序列化核心思想

**核心思想就是设计一种序列化协议，将对象的类型、属性类型、属性值一一按照固定的格式写到二进制字节流中来完成序列化，再按照固定的格式一一读出对象的类型、属性类型、属性值，通过这些信息重新创建出一个新的对象，来完成反序列化。**

### 如何选择序列化机制

**性能和效率**

序列化的效率影响到RPC调用的效率

**空间开销**

序列化后的字节数据体积越小，网络传输的数据量就越小，传输数据的速度也就越快，由于 RPC 是远程调用，那么网络传输的速度将直接关系到请求响应的耗时。

**序列化协议的通用性和兼容性**

影响到服务调用的稳定性和可用率

**序列化协议的安全性**

如果序列化存在安全漏洞，那么线上的服务就很可能被入侵。

首选的还是 Hessian 与 Protobuf，因为他们在性能、时间开销、空间开销、通用性、兼容性和安全性上，都满足了我们的要求。其中 Hessian 在使用上更加方便，在对象的兼容性上更好；Protobuf 则更加高效，通用性上更有优势。

## 网络传输

基于HTTP协议的（例如基于文本的SOAP（XML）、Rest（JSON），基于二进制Hessian（Binary））

基于TCP协议的（通常会借助Mina、Netty等高性能网络框架）

## 拓展

### 既有 HTTP ,为啥用 RPC 进行服务调用？

**RPC 只是一种设计而已**

RPC 只是一种概念、一种设计，就是为了解决 **不同服务之间的调用问题**, 它一般会包含有 **传输协议** 和 **序列化协议** 这两个。

但是，HTTP 是一种协议，RPC框架可以使用 HTTP协议作为传输协议或者直接使用TCP作为传输协议，使用不同的协议一般也是为了适应不同的场景。

 **RPC框架功能更齐全**

成熟的 RPC框架还提供好了“服务自动注册与发现”、"智能负载均衡"、“可视化的服务治理和运维”、“运行期流量调度”等等功能

## 参考

https://blog.csdn.net/fangmeng1997/article/details/108667250

https://javaguide.cn/distributed-system/rpc/why-use-rpc.html