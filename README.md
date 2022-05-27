
Nacos核心功能点 

**服务注册：** Nacos Client会通过发送REST请求的方式向Nacos Server注册自己的服务，提供自身的元数据，比如ip地址、端口等信息。 Nacos Server接收到注册请求后，就会把这些元数据信息存储在一个双层的内存Map中。

**服务心跳：** 在服务注册后，Nacos Client会维护一个定时心跳来持续通知Nacos Server，说明服务一直处于可用状态，防止被剔除。默认 5s发送一次心跳。 

**服务同步：** Nacos Server集群之间会互相同步服务实例，用来保证服务信息的一致性。 

**服务发现：** 服务消费者（Nacos Client）在调用服务提供者的服务时，会发送一个REST请求给Nacos Server，获取上面注册的服务清 单，并且缓存在Nacos Client本地，同时会在Nacos Client本地开启一个定时任务定时拉取服务端最新的注册表信息更新到本地缓存 

**服务健康检查：** Nacos Server会开启一个定时任务用来检查注册服务实例的健康情况，对于超过15s没有收到客户端心跳的实例会将它的 healthy属性置为false(客户端服务发现时不会发现)，如果某个实例超过30秒没有收到心跳，直接剔除该实例(被剔除的实例如果恢复发送 心跳则会重新注册)

![](http://cg-mall.oss-cn-shanghai.aliyuncs.com/blog/Nacos%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90-%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%8E%E5%8F%91%E7%8E%B0%28%E4%B8%B4%E6%97%B6%E5%AE%9E%E4%BE%8BAP%E6%A8%A1%E5%BC%8F%29.png)

文档地址：https://note.youdao.com/ynoteshare/index.html?id=17c68958637d60582e9c473f69f04aa5&type=note&_time=1653636060948
