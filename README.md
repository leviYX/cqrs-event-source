# 1、简介
使用pg作为write_source,使用es作为read_source，通过kafka作为事件驱动来实现cqrs+event_source的内容。


# 2、组件启动
## 2.1、启动kafka集群
~~~markdown
# 1、项目的docker-compose目录下有一个[docker-compose.yml](docker-compose/docker-compose.yml)文件
可以用来启动kafka集群。docker-compose -f docker-compose.yml  up -d
~~~


# 3、序列化
    对于和kafka交互，消息最好使用序列化发送，这样可以减少不必要的内存占用，并且可以方便的进行消息的压缩。
    而业内序列化比较好的是protobuf，但是protobuf的缺点是生成的代码要和语言绑定。
    这里我们使用avro来做序列化，他和json很多相似，而且格式紧凑，非常方便。
    github地址为：https://github.com/apache/avro
    文档地址为:https://avro.apache.org/docs/1.12.0/getting-started-java/
    在本项目中我们在kafka-modle中操作kafka消息的序列化，集成了avro依赖和插件，当我们用mvn打包的时候会自动生成avro的schema文件。
    具体操作为我在resourse目录下创建了一个avro的schema文件twitter.avsc文件，然后在pom.xml中配置了插件。你clean install之后会发现target目录下生成了
    对应的实体文件，后续我们就通过这个实体文件来序列化和反序列化消息。