> 文章每周持续更新，各位的「三连」是对我最大的肯定。可以微信搜索公众号「 后端技术学堂 」第一时间阅读（一般比博客早更新一到两篇）
## 单体式应用程序

与微服务相对的另一个概念是传统的**单体式应用程序**( Monolithic application )，单体式应用内部包含了所有需要的服务。而且各个服务功能模块有很强的耦合性，也就是相互依赖彼此，很难拆分和扩容。

说在做的各位都写过单体程序，大家都没意见吧？给大家举个栗子，刚开始写代码你写的helloworld程序就是单体程序，一个程序包含所有功能，虽然helloworld功能很简单。

#### 单体应用程序的优点

- 开发简洁，功能都在单个程序内部，便于软件设计和开发规划。
- 容易部署，程序单一不存在分布式集群的复杂部署环境，降低了部署难度。
- 容易测试，没有各种复杂的服务调用关系，都是内部调用方便测试。

### 单体应用程序的缺点

单体程序的缺点一开始不是特别明显，项目刚开始需求少，业务逻辑简单，写代码一时爽，一直爽。噩梦从业务迭代更新，系统日益庞大开始，前期的爽没有了，取而代之的是软件维护和迭代更新的无尽痛苦。

![单体架构](https://upload-images.jianshu.io/upload_images/7842464-a3829e92d3f8b90d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

由于单体式应用程序就像一个大型容器一样，里面放置了许多服务，且他们都是密不可分的，这导致应用程序在扩展时必须以「应用程序」为单位。

当里面有个业务模块负载过高时，并不能够单独扩展该服务，必须扩展整个应用程序（就是这么霸道），这可能导致额外的资源浪费。

此外，单体式应用程序由于服务之间的紧密度、相依性过高，这将导致测试、升级有所困难，且开发曲线有可能会在后期大幅度地上升，令开发不易。相较之下「微服务架构」能够解决这个问题。 

## 微服务

微服务 (Microservices) 就是一些协同工作小而自治的服务。

> 2014年，[Martin Fowler](https://zh.wikipedia.org/wiki/Martin_Fowler) 与 [James Lewis](https://zh.wikipedia.org/w/index.php?title=James_Lewis&action=edit&redlink=1) 共同提出了微服务的概念，定义了微服务是由以单一应用程序构成的小服务，自己拥有自己的行程与轻量化处理，服务依业务功能设计，以全自动的方式部署，与其他服务使用 HTTP API 通信。同时服务会使用最小的规模的集中管理 (例如 [Docker](https://zh.wikipedia.org/wiki/Docker)) 能力，服务可以用不同的编程语言与数据库等组件实现 。「维基百科」

### 举例

![](http://ww2.sinaimg.cn/large/9150e4e5ly1fswbux3qi6j206y06cmx4.jpg)

还是拿前面的 helloworld 程序来举栗子，想象一下你是 helloworld 公司的 CTO（老板还缺人吗？会写代码的那种），假设你们公司的 helloworld 业务遍布全球，需要编写不同语种的 helloworld 版本，分别输出英语、日语、法语、俄语...现在世界有6000多种语言（奇怪的知识又增加了）。

有人会说这还不简单我用`switch case`语句就完事了，同学，不要较真我就是举个例子，现实中的业务比 helloworld 复杂多了。好了，我们姑且认为按语言输出是个庞大复杂的工作，这时候就可以用微服务架构了，架构图如下：

![微服务架构](https://upload-images.jianshu.io/upload_images/7842464-fb70f0681d8bdf16.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 微服务与SOA

**面向服务的体系结构** `SOA (Service-Oriented Architecture)` 听起来和微服务很像，但 `SOA` 早期均使用了总线模式，这种总线模式是与某种技术栈强绑定的，比如：`J2EE`。这导致很多企业的遗留系统很难对接，切换时间太长，成本太高，新系统稳定性的收敛也需要一些时间，最终 `SOA` 看起来很美，但却成为了企业级奢侈品，中小公司都望而生畏。 

此外，实施`SOA`时会遇到很多问题，比如通信协议（例如SOAP)的选择、第三方中间件如何选择、服务粒度如何确定等，目前也存在一些关于如何划分系统的指导性原则，但其中有很多都是错误的。`SOA`并没有告诉你如何划分单体应用成微服务，所以在实施`SOA`时会遇到很多问题。

这些问题再微服务框架中得到很好的解决，你可以认为微服务架构是`SOA`的一种特定方法。

## 微服务架构

合久必分，鉴于「单体应用程序」有上述的缺点，单个应用程序被划分成各种小的、互相连接的微服务，一个微服务完成一个比较单一的功能，相互之间保持独立和解耦合，这就是微服务架构。

### 微服务优点

相对于单体服务，微服务有很多优点，这里列举几个主要的好处

#### 技术异构性

不同服务内部的开发技术可以不一致，你可以用java来开发helloworld服务A，用golang来开发helloworld服务B，大家再也不用为哪种语言是世界上最好的语言而争论不休。
![微服务架构-多技术](https://upload-images.jianshu.io/upload_images/7842464-cb50824fae547f82.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


为不同的服务选择最适合该服务的技术，系统中不同部分也可以使用不同的存储技术，比如A服务可以选择redis存储，B服务你可以选择用MySQL存储，这都是允许的，你的服务你做主。



#### 隔离性

一个服务不可用不会导致另一个服务也瘫痪，因为各个服务是相互独立和自治的系统。这在单体应用程序中是做不到的，单体应用程序中某个模块瘫痪，必将导致整个系统不可用，当然，单体程序也可以在不同机器上部署同样的程序来实现备份，不过，同样存在上面说的资源浪费问题。

#### 可扩展性

庞大的单体服务如果出现性能瓶颈只能对软件整体进行扩展，可能真正影响性能的只是其中一个很小的模块，我们也不得不付出升级整个应用的代价。这在微服务架构中得到了改善，你可以只对那些影响性能的服务做扩展升级，这样对症下药的效果是很好的。

#### 简化部署

如果你的服务是一个超大的单体服务，有几百万行代码，即使修改了几行代码也要重新编译整个应用，这显然是非常繁琐的，而且软件变更带来的不确定性非常高，软件部署的影响也非常大。在微服务架构中，各个服务的部署是独立的，如果真出了问题也只是影响单个服务，可以快速回滚版本解决。

#### 易优化

微服务架构中单个服务的代码量不会很大，这样当你需要重构或者优化这部分服务的时候，就会容易很多，毕竟，代码量越少意味着代码改动带来的影响越可控。



### 微服务缺点

我们上面一直在强调微服务的好处，但是，微服务架构不是万能的，并不能解决所有问题，其实这也是微服务把单体应用拆分成很多小的分布式服务导致的，所谓人多手杂，服务多起来管理的不好各种问题就来了。

为了解决微服务的缺点，前辈们提出了下面这些概念。

#### 服务注册与发现

微服务之间相互调用完成整体业务功能，如何在众多微服务中找到正确的目标服务地址，这就是所谓「服务发现」功能。

常用的做法是服务提供方启动的时候把自己的地址上报给「服务注册中心」，这就是「服务注册」。服务调用方「订阅」服务变更「通知」，动态的接收服务注册中心推送的服务地址列表，以后想找哪个服务直接发给他就可以。

![服务发现](https://upload-images.jianshu.io/upload_images/7842464-db86dceac215e2fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 服务监控

单体程序的监控运维还好说，大型微服务架构的服务运维是一大挑战。服务运维人员需要实时的掌握服务运行中的各种状态，最好有个控制面板能看到服务的内存使用率、调用次数、健康状况等信息。

这就需要我们有一套完备的服务监控体系，包括拓扑关系、监控（Metrics）、日志监控（Logging）、调用追踪（Trace）、告警通知、健康检查等，防患于未然。

#### 服务容错

任何服务都不能保证100%不出问题，生产环境复杂多变，服务运行过程中不可避免的发生各种故障（宕机、过载等等），工程师能够做的是在故障发生时尽可能降低影响范围、尽快恢复正常服务。

程序员为此避免被祭天，需要引入「熔断、隔离、限流和降级、超时机制」等「服务容错」机制来保证服务持续可用性。

#### 服务安全

有些服务的敏感数据存在安全问题，「服务安全」就是对敏感服务采用安全鉴权机制，对服务的访问需要进行相应的身份验证和授权，防止数据泄露的风险，安全是一个长久的话题，在微服务中也有很多工作要做。


## 服务治理

说到「治理」一般都是有问题才需要治理，我们平常说环境治理、污染治理一个意思，微服务架构中的微服务越来越多，上面说的那些问题就更加显现，为了解决上面微服务架构缺陷「服务治理」就出现了。

![](http://ww2.sinaimg.cn/large/9150e4e5gy1fx4lsf0onmj20dw0dwwes.jpg)

微服务的那些问题都要公司技术团队自己解决的话，如果不是大型公司有成熟的技术团队，估计会很头大。幸好，有巨人的肩膀可以借给我们站上去，通过引入「微服务框架」来帮助我们完成服务治理。

## 微服务框架

介绍一些业界比较成熟的微服务框架。

### Dubbo

是阿里巴巴公司开源的一个Java高性能优秀的服务框架，使得应用可通过高性能的 RPC 实现服务的输出和输入功能，可以和 Spring框架无缝集成。 Apache Dubbo |ˈdʌbəʊ| 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现 。2011 年末对外开源，仅支持 Java 语言。

官网：` http://dubbo.apache.org/zh-cn/ `

![Dubbo架构图|图片来源dubbo.apache.org](http://dubbo.apache.org/img/architecture.png)  



### Tars

腾讯内部使用的微服务架构 TAF（Total Application Framework）多年的实践成果总结而成的开源项目。 仅支持 C++ 语言，目前在腾讯内部应用也非常广泛。2017 年对外开源，仅支持 C++ 语言。

源码： `https://github.com/TarsCloud/Tars/ `

![TARS架构图|来源github.com/TarsCloud](https://upload-images.jianshu.io/upload_images/7842464-66f3c1a50c8518f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**本命鹅厂 TARS 框架介绍 PPT 已下载，不想自己麻烦去找的同学，在我公众号「后端技术学堂」回复「tars」获取。**

### Motan

是新浪微博开源的一个Java 框架。Motan 在微博平台中已经广泛应用，每天为数百个服务完成近千亿次的调用。于 2016 年对外开源，仅支持 Java 语言。

官方指南： `https://github.com/weibocom/motan/wiki/zh_userguide`

 ![Motan框架|图片来源github.com/weibocom/motan](https://github.com/weibocom/motan/wiki/media/14612352579675.jpg)



### gRPC

是Google开发的高性能、通用的开源RPC框架，其由Google主要面向移动应用开发并基于HTTP/2协议标准而设计，基于ProtoBuf(Protocol Buffers)序列化协议开发。本身它不是分布式的，所以要实现上面的框架的功能需要进一步的开发。2015 年对外开源的跨语言 RPC 框架，支持多种语言。

中文教程：` https://doc.oschina.net/grpc?t=58008 `

 ![gRPC架构图|图片来源www.grpc.io](http://www.grpc.io/img/grpc_concept_diagram_00.png) 

### thrift

最初是由 Facebook 开发的内部系统跨语言的高性能 RPC 框架，2007 年贡献给了 Apache 基金，成为 Apache 开源项目之一， 跟 gRPC 一样，Thrift 也有一套自己的接口定义语言 IDL，可以通过代码生成器，生成各种编程语言的 Client 端和 Server 端的 SDK 代码，支持多种语言。

 ![thrift架构 | 图片来源wikimedia](https://upload.wikimedia.org/wikipedia/commons/d/df/Apache_Thrift_architecture.png) 



## 微服务框架和RPC

很多人对这两个概念有点混淆，微服务框架上面我们说过了，我们再来看下RPC的概念。

### 什么是RPC

`RPC (Remote Procedure Call)`远程过程调用是一个计算机通信协议。我们一般的程序调用是本地程序内部的调用，`RPC`允许你像调用本地函数一样去调用另一个程序的函数，这中间会涉及网络通信和进程间通信，但你无需知道实现细节，`RPC`框架为你屏蔽了底层实现。RPC是一种服务器-客户端（Client/Server）模式，经典实现是一个通过**发送请求-接受回应**进行信息交互的系统。 

### 两者关系

`RPC`和微服务框架的关系我的理解，微服务框架一般都包含了`RPC`的实现和一系列「服务治理」能力，是一套软件开发框架。我们可以基于这个框架之上实现自己的微服务，方便的利用微服务框架提供的「服务治理」能力和`RPC能力`，所以微服务框架也被有些人称作`RPC框架`。



## 下一代微服务架构

`Service Mesh`（服务网格）被认为是下一代微服务架构，`Service Mesh`并没有给我们带来新的功能，它是用于解决其他工具已经解决过的服务网络调用、限流、熔断和监控等问题，只不过这次是在`Cloud Native` 的 `kubernetes` 环境下的实现。 

### 特点

Service Mesh 有如下几个特点：

- 应用程序间通讯的中间层
- 轻量级网络代理
- 应用程序无感知
- 解耦应用程序的重试/超时、监控、追踪和服务发现

目前两款流行的 `Service Mesh` 开源软件 `[Istio](https://istio.io/)` 和 `[Linkerd](https://linkerd.io/) `都可以直接在` kubernetes` 中集成，其中` Linkerd `已经成为`云原生计算基金会 CNCF (Cloud Native Computing Foundation)` 成员。

### Why Service Mesh

为什么现有微服务架构已经解决的问题还要用`Service Mesh`呢？这个问题问的好。

![](http://wx3.sinaimg.cn/large/006ARE9vgy1fy0s455zzxj303c02pjrb.jpg)

回答问题之前，先看下`istio.io`上对`service mesh`的解释，我觉得挺好的，摘抄出来：

> As a service mesh grows in size and complexity, it can become harder to understand and manage. Its requirements can include discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh also often has more complex operational requirements, like A/B testing, canary rollouts, rate limiting, access control, and end-to-end authentication. 
>
> makes it easy to create a network of deployed services with load balancing, service-to-service authentication, monitoring, and more, **with few or no code changes in service code.  **

试着总结一下：随着微服务的增多复杂程度也增加，管理变得更加困难，微服务架构虽然解决了「网络调用、限流、熔断和监控」等问题，但大多数框架和开源软件对原有业务是`侵入式`的，也就是需要在业务服务程序中集成相关的「服务治理」组件。

`Service Mesh`之于微服务，就像`TCP/IP`之于互联网，`TCP/IP`为网络通信提供了面向连接的、可靠的、基于字节流的基础通信功能，你不再需要关心底层的重传、校验、流量控制、拥塞控制。

用了`Service Mesh`你也不必去操心「服务治理」的细节，不需要对服务做特殊的改造，所有业务之外的功能都由`Service Mesh`帮你去做了。它就像一个`轻量级网络代理` 对应用程序来说是透明，所有应用程序间的流量都会通过它，所以对应用程序流量的控制都可以在 `serivce mesh` 中实现 。

 ![ Service Mesh架构|图片来自：[Pattern: Service Mesh](http://philcalcado.com/2017/08/03/pattern_service_mesh.html) ](https://jimmysong.io/blog/what-is-a-service-mesh/service-mesh-arch.png) 

## 写在最后
在IT世界没有什么技术是永不过时的，微服务架构的演进就是一个例子，从单体程序到微服务架构，再到`service mesh`架构，我不知道下一个技术迭代点是什么时候，但我知道微服务架构肯定还会更新，IT人更应该建立终身学习习惯。   
当然更重要的是拥有对技术的热情，热于拥抱变化、接受新技术，当我看到新技术我是兴奋的，内心os是`厉害了，还能这么玩！`，希望你也有这般热情，而不仅仅是面向工资编程，生活会有趣很多。   
老规矩。感谢各位的阅读，文章的目的是分享对知识的理解，技术类文章我都会反复求证以求最大程度保证准确性，若文中出现明显纰漏也欢迎指出，我们一起在探讨中学习。

**原创不易，看到这里动动手指，各位的「三连」是对我持续创作的最大支持。**

> 可以微信搜索公众号「 后端技术学堂 」回复「资料」有我给你准备的各种编程学习资料。文章每周持续更新，我们下期见！

## reference

 https://www.cnblogs.com/Zachary-Fan/p/service_manage_discovery.html 

 https://www.zhihu.com/question/56125281 

 http://dockone.io/article/3687 

 https://www.infoq.cn/article/micro-service-technology-stack 

 https://segmentfault.com/a/1190000010224335 

 https://book.douban.com/subject/26772677/ 

 https://jimmysong.io/blog/what-is-a-service-mesh/ 

https://github.com/weibocom/motan/wiki/zh_userguide